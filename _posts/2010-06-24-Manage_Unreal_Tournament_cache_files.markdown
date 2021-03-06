---
layout: post
title: Manage Unreal Tournament cache files
archive: true
---

This is a little Python script to manage cache files for Unreal Tournament, been
using it for years, figured I’d put it here. I only used/tested this with the
original UT on Windows and FreeBSD, should work for Linux and MacOS X.

This script will only rename the files to the correct name in the `Cache/`
directory, it doesn’t put them in the correct UT Directory (`System/`,
`Textures/`, etc.).
This is a feature and not a bug because when you’re using mods you often don’t
want to use the standard UT directories, there’s no way to figuring out which
files belongs to which mod (or even if it belongs to any mod).

A few simple commands can move the files:

	$ utdir=/usr/local/share/linux-ut
	$ mv *.u "$utdir/System/"
	$ mv *.utx "$utdir/Textures/"

etc…

The actual code
---------------

	#!/usr/bin/env python
	#
	# Martin Tournoij <martin@arp242.net>
	# http://arp242.net/weblog/Manage_Unreal_Tournament_cache_files.php
	# Free to use for whatever purpose. There are no restrictions.
	# Version 20100624
	#
	# This is a simple script to manage unreal tournament cache files.
	# Works on Windows, FreeBSD, Linux.
	#

	import os
	import re
	import shutil
	import sys

	if sys.platform[:3] == 'win':
		cachefile = '%s\\UnrealTournament\\Cache\\cache.ini' % os.getenv('SYSTEMDRIVE')
	else:
		cachefile = os.path.expanduser('~/.loki/ut/Cache/cache.ini')

	if len(sys.argv) > 1:
		cachefile = sys.argv[1]

	def ReadFile(file):
		newfile = []
		move = []
		f = open(file, 'r')
		for line in f:
			if line[0] == ';' or line[0] == '[':
				continue

			line = line.strip()
			if line == '':
				continue

			l = line.split('=')
			# There are multiple versions of these files active on servers, so skip
			# them and keep them in cache!
			if l[1] == 'INF_AimedPistols.u' or l[1] == 'UTCompass.u':
				newfile.append(l)
				continue
			move.append(l)

		f.close()
		return move, newfile

	if not os.path.exists(cachefile):
		print 'Error: cache.ini file "%s" does not exists.' % cachefile
		print 'Please specify the cache.ini file as the first argument'
		print 'Example: %s C:/games/UnrealTournament/Cache/cache.ini' % sys.argv[0]
		sys.exit(1)

	shutil.copy(cachefile, cachefile + '.bak')
	move, newfile = ReadFile(cachefile)
	dirname = os.path.dirname(cachefile)

	for file in move:
		if os.path.exists('%s/%s.uxx' % (dirname, file[0])):
			os.rename('%s/%s.uxx' % (dirname, file[0]), '%s/%s' % (dirname, file[1]))
			print file
		else:
			print "Warning, cache file `%s/%s.uxx' doesn't exist." % (dirname, file[0])

	f = open(cachefile, 'w')
	f.write('[Cache]\n')
	for n in newfile:
		f.write(n[0] + '=' + n[1] + '\n')
	f.close()
