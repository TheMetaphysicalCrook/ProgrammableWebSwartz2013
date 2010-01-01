---
title: "Building for Search Engines"
date: 2018-04-06T23:23:23+02:00
draft: true
---

Chapter 3

# Building for Search Engines: Following REST

Let’s talk about vacuum cleaners. It’s an all-too-common story. You’ve got a nice shiny new apartment, but it doesn’t stay that way for long. Dust falls on the floor, crumbs roll off your plate, flotsam, jetsam, and the little pieces from Jetsons’ toys begin to clutter your path. It’s time to clean.

Sweeping is fun at first—it gives you a little time to get lost in thought about your web application while you’re doing an ostensibly-useful repetitive-motion activity—but soon you grow tired of it. But liberal guilt and those Barbara Ehren- reich articles you read make you resistant to hiring a maid. So instead of importing a hard-up girl from a foreign country to do your housework, you hire a robot.

Now here’s the thing about robots (and some maids, for that matter): it’s not at all clear to them what is trash and what is valuable. They (the robots) wander around your house trying to suck things up, but on their way they might leave tire-treads on your manuscript, knock over your priceless vase, or slurp up your collection of antique coins. And sometimes it gets caught on the pull-cord for the blinds, causing the robot to go in circles while pulling the shutters open.

So you take precautions—before you run the robot, you pick the cords off the floor and move your manuscript to your desk and take care not to leave your pile of rare coins in the corner. You make sure the place is set up so that the robot can do its job without doing any real damage.

It’s exactly the same on the Web. (Except without the dust, crumbs, Jetsons, maids, tire treads, vases, coins, or blinds.) Robots (largely from search engines, but others come from spammers, offline readers, and who knows what else) are always crawling your site, leaving no nook or cranny unexplored, vacuuming up anything they can find. And unlike the household variety, you cannot simply unplug them— you really have to be sure to keep things clean. (Although see http://ftrain.com/robot_exclusion_protocol.html.)

Some people think they can just box robots out. “Oh, you need a login to get in; that’ll keep out the robots.” That’s what David Heinemeier-Hansson, creator of Rails, said. He was wrong. Google software that ran on users computers ended up exploring even pages behind the log-in requirement, meaning the robots clicked on all the “Delete” links, meaning robots deleted all the content. (Hansson, for his part, responded by whining about the injustice of it all.) Don’t let this happen to you.

Luckily, that genius Tim Berners-Lee (see previous chapter) anticipated all this and set precautions. You see, when you visit a website, you don’t just ask the server for the URL, you also tell it what kind of request you’re making. Here’s a typical HTTP/1.0 request:

GET /about/ HTTP/1.0

The first part (“GET”) is called the method, the second (‘/about/‘) is the path, and the third (“HTTP/1.0”) is obviously the version. GET is the method we’re probably all familiar with—it’s the normal method used whenever you want to get (GET it?) a page. But there’s another method as well: POST.

If you think of URLs as little programs sitting inside a server somewhere, GET can be thought of as just running the program and getting a copy of its output, whereas POST is more like sending it a message. Indeed, POST requests, unlike GET requests, come with a payload. A message is attached at the bottom, for the URL to do with as it wishes.

It’s intended for requests that actually do something that messes the order of the universe (or, in the jargon, “changes state”), instead of just trying to figure out what’s what. So, for example, reading an old news story is a GET, since you’re just trying to figure stuff out, but adding to your blog is a POST, since you’re actually changing the state of your blog.

(Now, if you want to be a real jerk about it, you can say that all requests mess with the state of the universe. Every time you request an old news story, it uses up electricity, and moves the heads around on disk drives, and adds a line to the server’s log, and puts a note in your NSA file, and so on. Which is all true, but pretty obviously not the sort of thing we had in mind, so let’s not mention it again. (Please, NSA?))

The end result is pretty clear. It’s fine if Google goes and reads old news stories, but it’s not OK if it goes around posting to your blog. (Or worse, deleting things from it.) Which means that reading the news story has to be a GET and blog deleting has to be a POST.

Actually, that’s not quite true. There are other verbs besides GET and POST (although those are by far the most common). There’s GET, HEAD, POST, PUT, DELETE, CONNECT, OPTIONS, PATCH, PROPFIND, PROPPATCH, MKCOL, COPY, MOVE, LOCK, UNLOCK, TRACE (and probably others). GET and POST we’ve already seen. HEAD is like GET but only requests the head- ers or a page and not the actual content. PUT is there if you want to replace the contents of the page with something entirely new—TimBL’s original web browser used PUT whenever you tried to save a change you made to a page. PATCH is like PUT but only changes part of a page. DELETE, MOVE, COPY, LOCK, and UNLOCK should be pretty self-explanatory. CONNECT is used for proxying and tunneling other stuff. OPTIONS lets you find out what the server supports. PROPFIND and PROPPATCH are used for setting properties in the WebDAV protocol. MKCOL is for making a WebDAV collection. (These probably shouldn’t have all gotten their own methods...) TRACE asks the server to just repeat back the request it got (it’s useful for debugging).

But, frankly, GET and POST are the most frequently used, in no small part because they’re the ones supported by all Web browsers. GET, of course, is used every time you enter a URL or click on a link, while POST can be used in some forms. (Other forms are still GET, since they don’t change anything.)

Following these rules is called following REST, after the 2000 Ph.D. disser- tation of Roy Fielding, coauthor (with Tim Berners-Lee and some others) of the official HTTP specification (RFC 2616, if you’re interested). Roy, a big bear of a man with a penchant for sports, set out to describe theoretically the various styles (“architectures”) of network-based applications. Then he describes the interesting hybrid that the Web adopted, which he terms “Representational State Transfer” or REST.

While REST is often used to mean something akin to “use GET and POST correctly,” it’s actually much more complicated, and more interesting, and we’ll spend a little time on it just so you can see the different kind of architectural tradeoffs that those Masters of the Universe who have to design a system like the Web have to think about.

The first choice made was that the Web would be a client-server system. Honestly, the Web is probably this way because Tim did things this way and Tim did thinks this way because that’s how everything else on the Internet was back then. But it’s not impossible to imagine that the Web could have been more peer-to-peer, like some of the file-sharing services we see today. (After all, the Web is in no small part just file-sharing.)

The more likely option is, of course, to break away from the Web altogether, and force people to download special software to use your application. After all, this is how most applications worked before the Web (and how many still work today)—new software, new protocols, new architectures for every app. There are certainly some good reasons to do this, but doing so breaks you off from the rest of the Web community—you can’t be linked to, you can’t be crawled by Google, you can’t be translated by Babelfish, and so on. If that’s a choice you want to make, you probably shouldn’t be reading this book.

The second major choice was that the Web would be “stateless.” Imagine a network connection as your computer phoning up HQ and starting a conversation. In a stateful protocol, these are long conversations—“Hello?” “Hello, welcome to Amazon. This is Shirley.” “Hi Shirley, how are you doing?” “Oh, fine, how are you?” “Oh, great. Just great.” “Glad to hear it. What can I do for you?” “Well, I was wondering what you had in the Books department.” “Hmm, let me see. Well, it looks like we have over 15 million books. Could you be a bit more specific?” “Well, do you have any by Dostoevsky?” (etc.). But the Web is stateless—each connection begins completely anew, with no prior history.

This has its upsides. For one thing, if you’re in the middle of looking for a book on Amazon but right as you’re about to find it you notice the clock and geebus! it’s late, you’re about to miss your flight! So you slam your laptop shut and toss it in your bag and dash to your gate and board the plane and eventually get to your hotel entire days later, there’s nothing stopping you from reopening your laptop in this completely different country and picking up your search right where you left off. All the links will still work, after all. A stateful conversation, on the other hand, would never survive a day-long pause or a change of country. (Similarly, you can send a link to your search to a friend across the globe and you both can use it without a hitch.)

It has benefits for servers too. Instead of having each client tie up part of a particular server for as long as their conversation lasts, stateless conversations get wrapped up very quickly and can be handled by any old server, since they don’t need to know any history.

Some bad web apps try to avoid the Web’s stateless nature. The most common way is thru session cookies. Now cookies certainly have their uses. Just like when you call your bank on the phone and they ask you for your account number so they
can pull up your file, cookies can allow servers to build pages customized just for you. There’s nothing wrong with that.

(Although you have to wonder whether users might not be better served by the more secure Digest authentication features built into HTTP, but since just about every application on the Web uses cookies at this point, that’s probably a lost cause. There’s some hope for improvement in HTML5 (the next version of HTML) since they’re– oh, wait, they’re not fixing this. Hmm, well, I’ll try suggesting it.) (http://lists.whatwg.org/pipermail/whatwg-whatwg.org/2008-October/016742.html.)

The real problem comes when you use cookies to create sessions. For example, imagine if Amazon.com just had one URL: http://www.amazon.com/. The first time you visited it’d give you the front page and a session number (let’s say 349382). Then, you’d send call back and say “I’m session number 349382 and I want to look at books” and it’d send you back the books page. Then you’d say call back and say “I’m session number 349382 and I want to search for Dostoevsky.” And so on.

Crazy as it sounds, a lot of sites work this way (and many more used to). For many years, the worst offender was probably a toolkit called WebObjects, which most famously runs Apple’s Web store. But, after years and years, it seems WebObjects might have been fixed. Still, new frameworks like Arc and Seaside are springing up to take its place. All do it for the same basic reason: they’re software for building Web apps that want to hide the Web from you. They want to make it so that you just write some software normally and it magically becomes a web app, without you having to do any of the work of thinking up URLs or following REST. Well, you may get an application you can use through a browser out of it, but you won’t get a web app.

The next major piece of Web architecture is caching. Since we have this long series of stateless requests, it sure would be nice if we could cache them. That is, wouldn’t it be great if every time you hit the back button, your browser didn’t have to go back to the server and redownload the whole page? It sure would. That’s why all browsers cache pages—they keep a copy of them locally and just present that back to you if you request it again.

But there’s no reason things need to be limited to just browser caches. ISPs also sometimes run caches. That way, if one person downloads the hot new movie trailer, the ISP can keep a copy of it and just serve the same file to all of their customers. This makes things much faster for the customers (who aren’t competing with the whole world for the same files) and much easier on the server operator
(who no longer has to serve quite so many copies). The one problem is that it does tend to mess up your download statistics a bit, but server operators can decide if they want to pay that price.

Similarly, servers can run caches. Instead of browsers visiting the server di- rectly, they hit a server cache (technically known as a reverse proxy) that checks to see if it already has a copy of the page and, if so, serves it, but otherwise asks the real server for it. If you build your web app to follow REST, you can often make your site much, much faster just by sticking a nice server cache (like Polipo) in front of it. But, of course, if you do bad things like use session cookies and ignore the rules about GET and POST, the server cache will just screw everything up. (Notice that only GETs can be cached; you wouldn’t want to cache the result of something like adding a new blog post or the next blog post would never get added!)

GET and POST are, of course, part of the next piece of architecture, which Fielding calls “Uniform Interfaces.” Every web app works the same basic way: there are a series of URLs which you perform methods on. The methods some- times change the state of the object and the server always returns the resulting “representation” of the object.

Thus, the name: Representational State Transfer (REST).
