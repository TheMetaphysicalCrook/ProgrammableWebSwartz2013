---
title: "Building for Users"
date: 2018-04-06T23:23:23+02:00
draft: true
---

Chapter 2

# Building for Users: Designing URLs

From billboards, buses, and boxes they peer out at us like alien symbols (except
hopefully less threatening): URLs are everywhere. Most obviously, they appear at
the top of the browser window while people are using your website, but they also
appear in a myriad of other contexts: in the status bar when someone has the mouse
over a link, in search results, in emails, in blogs, read over the phone, written down
on napkins, listed in bibliographies, printed on business cards and t-shirts and
mousepads and bumper stickers. They’re versatile little symbols.

Furthermore, URLs have to last. Those t-shirts and links and blogs will
not disappear simply because you decided to reorganize your server, or move to a
different operating system, or got promoted and replaced by a subordinate (or voted
out of office). They will last for years and years to come, so your URLs must last
with them.

Moreover, URLs do not just exist as isolated entities (like “http://
example.org/lunch/bacon.html”). They combine to form patterns
(“bacon.html”, “lettuce.html”, “tomato.html”). And each of these
patterns finds its place in a larger path of interaction (“/”, “/lunch/”,
“/lunch/bacon.html”).

Because of all this, URLs cannot be some side-effect or afterthought, as
many seem to wish. Designing URLs is the most important part of building a web
application and has to be done first. Encoded in their design are a whole series of
implicit assumptions about what your site is about, how it is structured, and how it
should be used; all important and largely-unavoidable questions.

Unfortunately, many tools for building web applications try to hide such questions
from you, preventing you from designing URLs at all. Instead, they present
their own interface to the programmer, from which they generate URLs by making
up random numbers or storing cookies or worse. (Nowadays, with Ajax and Flash,
some don’t provide URLs at all, making a site hell for anyone who wants to send
something cool they found to their friends.)

And when people who use such software find themselves having to write a
URL on a t-shirt or link to something from an email, they create a redirect—a
special URL who’s only purpose is to introduce people to the nightmarish randomnumber
system used by their actual website. This solves their immediate problem
of figuring out what to write on the t-shirt, but it doesn’t solve any of the more
fundamental problems, and it doesn’t make it possible for everyone else to make
their own t-shirts or send out their own emails.

If your tools don’t let you design your URLs, you need to get better tools.
Nobody would dare do graphic design with software that didn’t let them change
the font or paint with a brush that could only make squares. Yet some people think
it’s perfectly fine to sacrifice control over their URLs, the most fundamentally
important part of your website. It’s not. Get better tools. (If you need a place to start, there’s of course my own toolkit, web.py (http://webpy.org/) as well as the
Python web framework Django (http://djangoproject.com/).)

Once you have decent tools, it’s time to start designing. Let’s start with the
biggest constraints first. URLs shouldn’t change (and if they do change, the old ones
should redirect to the new ones) so they should only contain information about the
page that never changes. This leads to some obvious requirements.

These were most famously pointed out by the Web’s inventor, Sir Timothy
John Berners-Lee OM KBE FRS FREng FRSA (b. 8 June 1955, London, England).
During a miraculous Christmas break in 1990 that reminds one of Einstein’s
annus mirabilis, Tim not only invented the URL, the HTML format, and the HTTP
protocol, but also wrote the first web browser, WYSIWYG web editor, and web
server. (Makes you want to give the guy more Christmas breaks.) Although, in fact,
this is slightly redundant, since the first web browser (named WorldWideWeb),
not only let you read web pages, but let you write them as well. The idea was that
the Web should be an interactive medium, with everybody keeping their own notebooks
of interesting things they found and collaborating on documents with people
and posting stuff they’d done or wanted to share.

Editing a web page was as easy as clicking on it—you could just switch
into editing mode and select and correct typos right on the page, just like in a
word processor. (You’d hit save and it would automatically upload them to the
server.) You could create new pages just by opening a new window and instead of
bookmarks, you were expected to build web pages keeping track of the sites you
found interesting. (The original browser didn’t have a URL bar, in part to force you
to keep track of pages this way.)

It was a brilliant idea, but unfortunately it was written for the obscure NeXT
operating system (which later became Mac OS X) and as a result few have ever
gotten to use it. Instead, they used the clone created by a team at the University
of Illinois Urbana-Champaign (UIUC), which never supported editing because
programmer Marc Andreesen was too dumb to figure out how to do page editing
with inline pictures, something Tim Berners-Lee’s version had no problem with.
Marc Andreesen made half a billion dollars as UIUC’s browser became Netscape
while Berners-Lee continued doing technical support for a team of physicists in
Switzerland. (He later became a Research Scientist at MIT.)

![CERN Screenshot](http://www.w3.org/History/1994/WWW/Journals/CACM/screensnap2_24c.gif)

The result is that we’re only reacquiring these marvelous features a couple
decades later, through things like weblogs and Wikipedia. And even then, they’re
far more limited than the wide-reaching interactivity that Berners-Lee imagined.

But let’s turn away from the past and back to the future. Sir Tim argued that
to protect your URLs into the future, you needed to follow some basic principles. In
his 1998 statement “Cool URIs don’t change”, (Available at http://www.w3.org/Provider/Style/URI.) described as “an attempt to redirect
the energy behind the quest for coolness... toward usefulness [and] longevity,” he
laid them out:

However, I go on to disagree with Tim’s proposed solution for generating
Cool URIs. He recommends thoroughly date-based schemes, like
“http://www.w3.org/1998/12/01/chairs”. As far as I’ve noticed, only the
W3C has really thoroughly adopted this strategy and when I’ve tried it, it’s only
led to ugliness and confusion.

(You may notice that Tim says URI, while I say URL. URL, the original
term, stands for Uniform Resource Locator. It was developed, along with the Web,
to provide a consistent way for referring to web pages and other Internet resources.
Since then, however, it has been expanded to provide a way for referring to all sorts
of things, many of which are not web pages, and some of which cannot even be
“located” in any automated sense (e.g., abstract concepts like “Time magazine”).
Thus, the term was changed to URI, Uniform Resource Identifier, to encompass
this wider set. I stick with the term URL here since it’s more familiar, but we’ll end
up discussing abstract concepts in later chapters.)

First, URLs shouldn’t include technical details of the software you used
to build your website, since that could change at any moment. Thus, things
like “.php” and “.cgi” are straight out. For similar reasons, you can drop “.html”,
“PHP_SESS_ID” and their ilk. You’ll also want to make sure that the names of
your servers (e.g., “www7.example.org” or “plato.example.net”) aren’t seen in your
URLs. Moving from one programming language, one format, or one server to another
is fairly common; there’s no reason your URLs should depend upon your
current decision.

Second, you’ll want to leave out any facts about the page that might change.
This is just about everything (its author, its category, who can read it, whether it’s
official or a draft, etc.), so your URLs are really limited to just the essential concept
of a page, the page’s essence. What’s the one thing that can’t be changed, that makes
this page this page?

Third, you’ll want to be really careful about classification. Many people like to
divide their websites up by topic, putting their very favorite recipes into the ‘/food/‘
directory and their stories about the trips they take into ‘/travel/‘ and the stuff they’re
reading into ‘/books/‘. But inevitably they end up having a recipe that requires a
trip or a book that’s about food and they think it belongs in both categories. Or
they decide that drink should really be broken out and get its own section. Or they
decide to just reorganize the whole thing altogether.

Whatever the reason, they end up rearranging their files and changing their
directory structure, breaking all their URLs. Even if you’re just rearranging the site’s
look, it takes a lot of discipline not to move the actual files around, probably more
than you’re going to have. And setting up redirects for everything is so difficult that
you’re just not going to bother.

Much better to plan ahead so that the problem never comes up in the first
place, by leaving categories out of the URL altogether.

So that’s a lot of don’ts, what about some do’s?

Well one easy way to have safe URLs is to just pick numbers. So, for example,
your blogging system might just assign each post with a sequential ID and give them
URLs like:

```
http://posterous.com/p/234
http://posterous.com/p/235
http://posterous.com/p/236
```

Nothing wrong with that. However, if your site is a little more popular, the
IDs can get quite long and confusing:

```
http://books.example.org/b/30283833
```

In a situation like this, you might want to encode numbers using base 36
instead of base 10. Base 36 means you get to use all the letters in addition to just
numbers,but only one case,so there’s no confusion about how to capitalize numbers.
(Imagine someone reading the URL over the phone. It’s a lot easier to say “gee,
five, enn, four” than “lower-case gee, the number five, upper case enn, the number
four.”)

To be super-careful, you might want to go a step further and skip any numbers
that end up having zero, O, one, L, or I in them, since those letters can often be
confused.

The result is that you have URLs that look like:

http://books.example.org/b/3j7is

and end up being a lot shorter. While four base 10 digits can only go up to
9999, in base 36 zzzz is actually 1,679,615. Not bad.

One problem with numerical identifiers, however, is that they’re not “optimized”
for search engines. Search engines don’t just look at the content of a page
to decide whether it’s a good result for someone’s search, they also look at the URL
which, because it’s so limited, is given special weight. But if your URLs are just
numbers, they’re unlikely to have anything that matches people’s search engine
queries, making them less likely to be found in search results. To fix this, people are
appending some text after the number, as in:

http://www.hulu.com/watch/17003/saturday-night-liveweekend-update-judy-grimes

The text at the end is part of the URL, but it’s not used to identify the right
page. Instead, the system looks only at the number. Once it gets there, it looks at
the current title it has for the number, sees if it matches the URL, and if it doesn’t,
redirects users to the correct one. That way they can type in:

http://www.hulu.com/watch/17003/this-is-where-i-got-thejoke-above

or even:

http://www.hulu.com/watch/17003/

(Isn’t interesting how even though we typically read books as series of pieces of paper stacked from left to right,
we still refer to things that come earlier as “above” the others (or supra if you want to be all Latin about it), as
if we were all reading the raw scroll of paper that Kerouac emitted from his typewriter. See, e.g., http://www.npr.org/templates/story/story.php?storyId=11709924 for details. Of course, unlike my typewriter- or
notebook-bound predecessors, I’m writing this in a wordprocessor whose simulated form of up-down perfectly
mimics Kerouac’s physical scroll. Coming full circle, I suppose.)

and still get the right page. This isn’t perfect, since many users will still think they
have to type in the long text “saturday-night-live-weekend-update-judy-grimes,”
but it’s probably outweighed by the number of additional users who will find you
more easily on search engines. (Ideally, there would be some way in the URL
to indicate to humans that the remaining text is optional, but I haven’t seen any
conventions here yet. I guess the hope is that they’ll notice the number and just get
the idea.)

(You’ll note that all these URLs are within directories, not at the top-level.
This just feels cleaner to me—I don’t like imagining the entire site’s files are sprawled
across the root directory randomly;it’s much nicer to think of them stacked up inside
‘/watch/‘ or ‘/b/‘. But if your main nouns are subdirectories themselves, as with the
user pages on Twitter and Delicious, it might make sense to break this rule. (More
on this in a bit.))

Numbers work well in cases where pages get created automatically (maybe
you’re importing a lot of stuff, or you generate pages in response to emails or
incidentally for other actions) or their titles tend to change, but in other cases you
might prefer what’s called a slug. A slug is just a little bit of text that looks good
in a URL, like “wrt/dfw” or “beyond-flash”. When a user creates a page, you have
them create the slug at the same time (perhaps including an auto-generated one
from the title by default), and then you force them to stick with it (or else make
sure to redirect all the old ones whenever it changes).

On sites like Wikipedia, slugs are basically generated incidentally. When you
include text like “Jackson was hardly a fan of the late [[Robert Davidson]]‘ the site
automatically links you to a new page with the slug “Robert/Davidson”. Especially
with the numerous conventions about titles Wikipedia has built over the years
(along with the endless back-up redirects), the result is surprisingly convenient.

You’ll note that all this discussion has basically been about nouns—the main
things that make up your site, whatever those are (videos, blog posts, books). There
are typically three other types of pages: subpages (which drill down into some aspect
of the nouns), site pages (like about and help and so on), and verbs (which let you
do things with the nouns).

Subpages are some of the easiest, and some of the most difficult. In the easy
cases, you just indicate the subpage by adding a slash and a slug for the subpage.
So, if your page for Nancy Pelosi is at:

http://watchdog.net/p/nancy_pelosi

it seems pretty obvious that your page on her finances should be at:

http://watchdog.net/p/nancy_pelosi/finances

Sometimes the majority of your site is subpages. So with Twitter, a user’s page
is at:

http://twitter.com/aaronsw

while their status messages get URLs like:

http://twitter.com/aaronsw/statuses/918239758

(Notes: The “statuses” bit is redundant and the number way too long.)
But things get more complicated when your nouns have more complex relationships.
Take Delicious, where users post links under various tags. How should
things be structured? user/link/tag? tag/user/link?

Delicious, which for a long time used its URL scheme as a primary navigation
interface, is so brilliant at its URL choices that it should be carefully studied. They
decided that users were the primary object and gave them the whole space in ‘/‘
(like Twitter). And underneath each user, you could filter by tags, so you have:

http://delicious.com/aaronsw (links from me)

http://delicious.com/aaronsw/video (links from me tagged “video”)

http://delicious.com/aaronsw/video+tech (links from me tagged
“video” and “tech”)

And then they created a special pseudo-user called tag that lets you see all
links with a tag:

http://delicious.com/tag/tech (all links tagged “tech”)

(The URLs for links aren’t as smart, but let’s not dwell on that.) It’s hard to
give general rules for how to solve such inter-linking problems; you basically have
to do what “feels right” for your app. for social sites, like Delicious and Twitter, this
means putting the focus on the users, since that’s primarily what users care about.
But for other apps that might make less sense.

It’s tempting to just not decide and support all of them. So, in place of
Delicious, you’d have:

http://del.example.org/u/aaronsw (links from me)

http://del.example.org/t/tech (links about tech)

http://del.example.org/u/aaronsw/t:tech (links from about tech)

http://del.example.org/t/tech/u:aaronsw (links about tech from
me)

The problem here is that the last two are duplicates. You really want to pick
one form and stay with it, otherwise you end up confusing search engines and
browser histories and all the other tools that try to keep track of whether they’ve
already visited a page or not. If you do have multiple ways of getting to the same
page, you should pick one as the official one and make sure all the others redirect.
(In an extreme case, you’d take the “video+tech” example above and redirect it to
“tech+video”, making the official URL be the one where the tags are in alphabetical
order.)

Next up: site pages. Looking at Twitter and Delicious basically give away
the store above (you mean I can have “twitter.com/contact” if my username is
“contact”?!), you might wonder where they can possibly put their help and login
pages. One trick might be to reserve a subdirectory like ‘/meta/‘ and put everything
in there. But Delicious and Twitter seem to get by just by reserving all the important
potential-page-names and putting stuff there. So, as you’d expect, Twitter’s login
page is at:

http://twitter.com/login

And, if you’re not expecting to have a lot of site pages, this will get you thru.
(Be sure to reserve “help” and “about”, though.)

And, of course, if you’re not giving away the store, you don’t have any of these
problems. So just pick the sensible URLs for the pages that users come to expect.
And, of course, be sure to follow all the noun-principles above.

That was easy, so we’re left with just verbs. There are two ways you might
imagine verbs working:

pass the noun to the verb: /share?v=1234

pass the verb to the noun: /v/1234?m=share

After spending a lot of time experimenting with this, I’m convinced the latter
is the right way. It takes up less of the “URL-space,” it sorts nicer in people’s address
bars, and it makes it visually clear that you’re doing something to an object.

It’s tempting to just use subpages, like:

/v/1234/share

but I prefer the “?m=share” formulation for two reasons: first, it works even when
your nouns already have subpages, and second, it makes it clear that the page is
meant to do something, not just convey more information. But the converse is true
as well. Don’t do:

/p/nancy_pelosi?m=finances

making it look like the page is supposed to do something when it really just conveys
more information.

Alright, that’s enough about picking URLs. Let’s move on to actually doing
something with them!

