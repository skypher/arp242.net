---
layout: post
title: "The Art of Unix Programming, reformatted"
archive: true
---

tl;dr: I reformatted Eric S. Raymond's *The Art of Unix Programming* for
readability; [read it here][taoup-mine].

---

I recently wanted to look up a quote for an article I was writing, and I was
fairly sure I had read it in *The Art of Unix Programming*. Eric S. Raymond
(esr) has [kindly published it online][taoup], but it's difficult to search as
it's distributed over many different pages, and the formatting is not exactly
conducive for readability.

I `wget --mirror`’d it to my drive, and started out with a simple [script][fix]
to join everything to a single page, but eventually ended up rewriting a lot of
the HTML from crappy 2003 docbook-generated tagsoup to more modern standards,
and I slapped on some CSS to make it more readable.

The results are fairly nice, and it should work well in any version of any
browser (I haven't tested Internet Explorer and Edge, lacking access to a
Windows computer, but I'm reasonably confident it should work without issues; if
not, see the bottom of this page on how to get in touch).

The HTML could be simplified further (so rms can read it too[^1]), but dealing
with 360k lines of ill-formatted HTML is not exactly my idea of fun, so this
will have to do for now.

The entire page is self-contained. You can save it to your laptop or mobile
phone and read it on a plane or whatnot.

---

Why spend so much work on an IT book from 2003? I think a substantial part of
the book still applies very much today, for *all* programmers (not just Unix
programmers). For example the [Basics of the Unix Philosophy][phil] was good
advice in 1972, is still good advice in 2019, and will continue to be good
advice well in to the future.

Other parts have aged less gracefully; for example *"since 2000, practice has
been moving toward use of XML-DocBook as a documentation interchange format"*
doesn't really represent the current state of things, and the [Data File
Metaformats][data] section mentions XML and INI, but not JSON or YAML (as they
weren't invented until after the book was written)

I find this *adds*, rather than detracts. It makes for an interesting window in
to past. The downside is that the uninitiated will have a bit of a hard time
distinguishing between the good and outdated parts; as a rule of thumb: if it
talks about abstract concepts, it probably still applies today. If it talks
about specific software, it may be outdated.

I toyed with the idea of updating or annotating the text, but the license
doesn't allow derivative works, so that's not going to happen. Perhaps I'll
email esr and ask nicely. Another project, for another weekend :-)

[^1]: From [How I use the Internet](https://stallman.org/stallman-computing.html):
	  *"I usually fetch web pages from other sites by sending mail to a program
	  that fetches them, much like wget, and then mails them back to me. Then I
	  look at them using a web browser, unless it is easy to see the text in the
	  HTML page directly. I usually try lynx first, then a graphical browser if
	  the page needs it"*

[data]: /the-art-of-unix-programming/#ch05s02
[phil]: /the-art-of-unix-programming#ch01s06
[taoup]: http://catb.org/~esr/writings/taoup/html/
[taoup-mine]: /the-art-of-unix-programming/
[fix]: /the-art-of-unix-programming/fix-taoup.py
