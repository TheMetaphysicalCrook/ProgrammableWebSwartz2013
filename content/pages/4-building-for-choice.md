---
title: "Building for Choice"
date: 2018-04-06T23:23:23+02:00
draft: true
---

Chapter 4

# Building for Choice: Allowing Import and Export

Robots and browsers and protocols are fun, sure, but if you want your site to succeed it ultimate has to appeal to humans—the real people who build and use all that other stuff. And even if information doesn’t, humans generally want to be free. If you don’t believe me, ask a friend to lock you in their trunk, and then reevaluate your position.

Greedy folks (i.e. businesspeople) tend to be kind of short-sighted about this. “If I put big metal spikes in front of the exit,” they think, “my customers will never want to leave! My customer retention rates will go thru the roof.” They decide to give a try and they have some big metal spikes installed in front of the exit. And, being the sober-minded realist businesspeople like to pretend they are, they measure customer retention rates before and after the metal spikes. And, sure enough, it worked—people aren’t leaving. Just look at those numbers! But what they didn’t measure is that people also aren’t coming back. After all, nobody wants to go someplace with spikes on the exits. Think about this next time you find that pop-up ads increase sell-thru rates.

This is why a site like Amazon is such a cluttered mess of sell boxes. Amazon’s managers insist that they’re rigorously hard-headed engineers. The boxes are there because they sell things and their job is to make money. Clean, clear, uncluttered pages may appeal to kids in art school or Apple interns, but here in the real world cash is king. And like Mark Penn advising Hillary Clinton, if you don’t believe them they’ll pull out the numbers to “prove” it. Every box, they say, was carefully tested: half the users were given a page with the new box, half without. And the users who got the page with the box bought more.

Well, no duh. Obviously more people are going to buy something if you ask them to, just like more McDonald’s customers will SuperSize their order when the disaffected teenager asks them to. But Amazon’s gone way beyond that—now we’re into the realm of the girl-with-the-headset pitching us on every third item off the
menu. Sure, you may buy more this time, but after the stomachache hits you’ll make sure your next outing is to Burger King.

Companies rarely try to measure such effects and even if they did, it’s not easy. It’s a piece of cake to serve someone an additional link and seeing if they click on it; keeping track of whether they come back to the store in the weeks and months to come is much harder. Worse, the difference made by any one additional box is subtle, and thus hard to measure. The real test isn’t whether removing one sell box gets Amazon more customers, it’s whether switching to a kindler, gentler layout does. But that would be a radical change for Amazon—and thus pretty hard to test without raising hackles and freaking people out. “Well, if you can’t measure people,” the MBAs say, “you can at least ask them.” And thus the dreaded “focus group,” whose flaws can dwarf even the most bogus statistical study. At least with the click- through games you’re measuring what people actually do; with focus groups you find out what people want you to think they say they do, which is a very different thing.

For one thing, people are notoriously bad observers of themselves. For the most part, we don’t know why or how we do things, so when we’re asked we make up rationalizations on the spot. This isn’t just carelessness—it’s how the brain works. To accomplish tasks of any complexity, we need to make their component parts automatic—you’d never get to the store if you had to think about which thigh muscles to move to get your leg in the right position—and automatic behavior is exactly behavior we don’t think about (this is why athletes’ memoirs are so boring.(See D. F. Wallace, “How Tracy Austin Broke My Heart” in Consider the Lobster (2005).)

So not only are you asking people a question they don’t—can’t—know the answer to, you’re also asking them in a nice conference room, filled with other people, after giving them some cash. It doesn’t take much reading in social psychology to realize this isn’t exactly an ideal situation for honesty. People are, of course, going to say what they think you want to hear, and even if you have the most neutral of moderators asking the questions, they’re going to be able to make some educated guesses as to what that is.

Which is why watching focus groups is such an infuriating experience: like a girl pretending to play dumb in a bar, you’re watching people act the way they think people expect people like them to behave.

But if you can’t measure people and you can’t ask them, what does that leave? Well, good old-fashioned experience. As is usually true in life, there’s no shortcut
around incompetence; at some point, you just need genuine ability. When it comes to pleasing users, this generally has two parts: First, you need the basic skill of empathy, the ability to put yourself in a user’s shoes and see things through their eyes. But for that to work, you also need to know what it’s like inside a user’s head, and as far as I can tell the best way to do this is just to spend lots of time with them.

The best usability expert in the world, Matthew Paul Thomas, spent the first few years of his life doing tech support in a New Zealand cybercafe. This is the kind of job you imagine Stalin exiling programmers to, but Thomas made the best of it. Instead of getting angry at dumb users for not understanding what a “Taskbar” was, he got pissed off at the idiots who designed a system that required such arcane knowledge. And now that he’s in a position to fix such things, he understands at a deep visceral level what their flaws are.

I wouldn’t wish to force such an exile on anyone (well, I suppose there are a couple anonymous UI designers who might be candidates), but there’s certainly no shortage of people who already possess a user’s intuition to various degrees. The problem is that no one listens to them. It’s always so easy to dismiss them as naive or dumb or out-of-touch. After all, the additional menu bar option you want to add makes perfect sense to you—how could it really make things worse?

When a company does focus on their users, it’s a real shock. Take Zappos, an online shoe store. Zappos is fanatical about customer service. They quietly upgrade first-time purchasers to overnight delivery, they write cards and send flowers when the situation warrants it, and they not only give complete refunds but pay for shipping the shoes back as well. It’s the kind of company people rave about. But, most interestingly for our purposes, if they don’t have the shoe you want in stock, they try to find you a competitor that does!

From the short-term perspective, this seems insane: why would you actually do work to help your customers buy shoes from someone else? But, in the long term, it’s genius. Sure, you may make one purchase somewhere else, but not only will you go back to Zappos for every other shoe purchase for the rest of your life, you’ll also write long, glowing blog posts about how awesome Zappos is.

This is one of the secrets of success on the Web: the more you send people away, the more they come back. The Web is full of “leaf nodes”—pages that say something interesting, but really don’t link you anywhere further. And leaf nodes are great—they’re the core of the Web in fact—but they’re the end of a journey, not the beginning. When people start their day, or their web browser, they want a page that will take them to a whole bunch of different sites and perspectives, not just try
to keep them cooped up in one place. What’s the by-far most popular site on the Internet? Google Search, a site whose goal is to get you someplace else as quickly and unobtrusively as possible.

The reason all this stuff about metal spikes and New Zealand exiles and shoe stores and leaf nodes is relevant to a book on web apps is because I’m now going to ask you to do something that seems insane, something that sounds like it will kill your site. I’m going to ask you to open up your data. Give it away.

I’ll give you a second to catch your breath.

It’s not as crazy it sounds. Wikipedia, a successful site by any measure, gives away the store—you can download full database dumps, including not just every page on Wikipedia, but every change made to every page, along with full permission to republish it as you see fit. It doesn’t seem to have hurt their popularity any.

Obviously, I’m not saying you publish users’ personal details for everyone to see. It would be crazy for Gmail to put up a site where you could download every one of their users’ email. Instead, I’m suggesting you let users get their own data out of your site. People who put their events in your calendar should be able to export their calendar; people who got their email thru Gmail should be able to get it back out again.

Good export isn’t just the right thing to do, it can also be a strong way to attract users. Folks are uncomfortable about pouring their whole life into a hosted web application—they’ve been burned too many times by companies that took all their data and went bust. Going out of your way to make sure they can get their stuff out of your site can do a lot to regain their trust.

While I have a lot to say about formats in this book, the actual format you use is kind of irrelevant here. The important thing is that you do it at all. XML, RDF, CSV—the popular blogging system Movable Type actually just dumped posts as long text files, and while it was a dreadful format to work with, it was better than nothing. As long as you pick something halfway sensible, people will find a way to make it work.

The exception is if there’s already a standard (de facto or otherwise) in your field. For example, OPML is pretty widely accepted as the way to export the list of blogs you read. If there is, you just have to support the standard. Sorry. If other software provides a way to important a certain format, you’re just going to have to bite the bullet and output in that format. Anything else looks like churlishness and users aren’t going to care about the technical details.

And, of course, it goes both ways: a great way to attract users is to provide import functionality yourself. By supporting import from other products, whether they have official export features or not, you make it easy for users to slide into your own version. Even if your competitors don’t have an official export function, you can still help users out (and offend your competitors) by scraping data out of their system—writing custom tools to pull stuff out of their user interface and into your database.

The end result is the kind of frictionless world savvy users can only dream of—smoothly gliding from one app to another, taking advantage of new features without having to give up your old data. And if the company making it gets bought and the developers who wrote all the new features quit and start a competitor, you can pull your data right back out again and zip over to the new app.

Which means more choice—and isn’t that ultimately best for everyone?
