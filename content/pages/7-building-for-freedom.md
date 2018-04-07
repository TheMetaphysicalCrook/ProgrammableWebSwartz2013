---
title: "Building for Freedom"
date: 2018-04-06T23:23:22+02:00
draft: true
---

Chapter 7

# Building for Freedom: Open Data, Open Source

Our story starts with a paper jam. It was 1980 and the Artificial Intelligence Lab at MIT had received an elegant new printer from Xerox. The printer, however, had an unfortunate tendency to jam, causing print jobs to pile up and nothing to get printed until someone happened to notice and fix the jam.

For Richard Stallman, one of the programmers at the AI Lab, this wasn’t such a big deal. With their previous printer, Stallman had simply changed the printer driver to detect whether the printer was jammed and, if it was, to notify anyone who had sent it a print job. “If you got that message, you couldn’t assume somebody else would fix it,” Stallman later recalled. “You had to go to the printer. A minute or two after the printer got in trouble, the two or three people who got messages arrive to fix the machine. Of those two or three people, one of them, at least, would usually know how to fix the problem.”

But the Xerox printer was different: Xerox hadn’t provided the lab with the source code to their printer drivers. There was no way for Stallman to add this new functionality to the driver. When Stallman asked Xerox for the code, they refused to provide it, insisting that it was an important trade secret for their business. And when Stallman found a student at Carnegie Mellon who had been given access to the software, that student also refused to provide a copy, saying he’d signed a contract with Xerox not to share it.

Stallman was outraged. Computer software was supposed to be a tool to serve people; that’s why he and his labmates spent their time writing software. And yet, through a combination of greed and legal restrictions, people were forced to suffer because they were prevented from improving these tools.

Stallman wanted to ensure no one else would be forced to suffer in this way; he wanted to build a computer system based around principles of freedom. In 1984 he quit his job and announced the GNU project.

Stallman later clarified that free software was software that guaranteed users four freedoms:

0. The freedom to run the program, for any purpose.

1. The freedom to study how the program works, and adapt it to your needs. (Source code is a requirement for this.)

2. The freedom to redistribute copies so you can help your neighbor.

3. The freedom to improve the program, and release your improvements to the public, so that the whole community benefits.

(Again, source code is a requirement for this.) “I consider that the golden rule requires that if I like a program I must share it with other people who like it. I cannot in good conscience sign a nondisclosure agreement or a software license agreement. So that I can continue to use computers without violating my principles, I have decided to put together a sufficient body of free software so that I will be able to get along without any software that is not free.”

Stallman codified these freedoms in the GNU General Public License or GPL. If you modify a piece of software that is licensed under the GPL and redis- tribute it, the license requires that you also redistribute the source code at no extra charge and allow everyone who receives a copy to do likewise.

Since 1984, the GNU operating system (whose most popular flavor is GNU/Linux) has been built and released under the GPL. A 2007 study found that 13% of servers and 1% of desktops were sold running GNU/Linux. And any- one can download the entire operating system for free off the Internet.

The success of GNU/Linux has led to a larger free software movement as well as the “open source” movement, which releases software and its source code under copyright licenses that provide some of the software freedoms.

The Mozilla Firefox browser, for example, is open source and currently makes up around 15% of market. Large portions of the Mac OS X operating system are also open source, including WebKit, the core of Safari, the Mac OS X web browser.

The open source and free software movements have now built free alternatives for just about every major type of computer application, from word processing to video games. And for a time it seemed like Stallman’s dream had come true: one could truly continue to use computers without having laws restrict one’s freedom — it was possible “to get along without any software that is not free.”

\* * *

Meanwhile,TimBerners-Lee,anEnglishmanlivinginFrancewhoworkedat a physics lab in Switzerland, was frustrated with how difficult it was for physicists to share documents. And so, in 1989, he came up with the World Wide Web, developed the standards that made it work, and built the first web browser and web server.

The power of the browser was its flexibility (or, in law professor Jonathan Zittrain’s phrase, its “generative nature”). Just as a general-purpose computer al- lowed you to run any program, from a music player to a graphing calculator, the web browser let you view any kind of document. A book, a physics paper, or photos of cats with funny captions — the web browser doesn’t care; it displays whatever the server provides it with.

This seems like a trivial point now, but it was a vast change from other networked software at the time. Email programs, for example, are designed simply to display email — they have an enormously specialized interface for composing emails, finding emails, seeing who an email is from and to, and placing emails in different folders. The same was true for discussion software, chat software, and other pieces of software that communicated over the network.

The Web was different: it did not specialize in any particular type of content, but let you share whatever you like.

This lack of specialization in the Web browser allowed people to move this specializationtotheWebserver.ThetraditionalWebserversimplyservedupstatic documents that someone had previously written. But it was quickly clear that there was no reason the server had to be so constrained.

Instead of simply serving up previously-composed documents, the server could compose new documents “on-the-fly” as they were requested. Thus, instead of simply having a document which listed what restaurants have tables available, a web server could be instructed to query the different restaurants, learn their availability, and construct a page from the results.

And users, instead of passively requesting different prewritten documents, could submit requests to the server and actually begin to interact with it. Thus, they could ask the server to reserve one of the tables and send their name and phone number along with that request.

The result was that the humble web browser quickly began to overtake all the other “specialized” applications. Instead of having a special program just for reading
email, people read their email over the Web. Similarly, discussion groups, chat rooms, and other forms of social interaction have moved inside the Web browser.

But software developers quickly discovered that, for social creatures like us humans, everything has a component of social interaction. For example, titling and categorizing the photos you take would seem like an obviously solitary activity. But sites like Flickr demonstrate that people love to discuss and categorize photos of their friends, or even strangers, and that people, all things considered, would prefer to organize their photos in a program that exposes them to other people.

The result is the recent “Web 2.0” phenomenon, in which just about every piece of computing is moved onto the Web and made social in some way. For photos and videos, there is Flickr and YouTube. For news, there are sites like Digg and Reddit where you can submit, edit, and vote on news stories. Calendars, todo lists, even music collections and word processors are all being made into dynamic social web applications.

Pundits now discuss a not-too-distant future of “dumb clients” and “cloud computing” where the other applications on the computer disappear and all that is left is the web browser. And for people who use kiosk computers or Internet cafes, that future is already here.

For some, this is an exciting prospect. But for those, like Stallman, concerned with issues of software freedom, it is frightening. Even in the dark days of the proprietary printer driver, Stallman still had control over the computer which drove the printer, even if he did not have the source code to modify it. But with a Web 2.0 application, you don’t have even that. The computer running your software is locked away in some distant server farm. You can only communicate with it through your web browser.

Now this does provide some flexibility. Web browsers can be programmed to block ads or extract content. Plugins like Zotero and Greasemonkey let users add new functionality to existing sites by intercepting and modifying documents as they come back from the Web server.

But this is a rather pale notion of freedom, like saying that moviegoers have control over the films they watch because they can hold pictures up in front of the screen as they watch.

Another option, of course, is providing APIs. Thus, instead of having to manually click the “buy” button on an Amazon page to buy a new set of razors, with an Amazon API you can have a program automatically purchase the razors for you every month.

This is undoubtedly useful, but again, a rather pale notion of freedom com- pared to the four freedoms that free software provides. If Amazon was truly free, you wouldn’t just be able to write programs to automate your usage of the application, you’d be able to change how the application actually works.

The obvious solution to this challenge is simply to release the software on the Web server under the GPL or some other free software license. Then anyone could download a copy and modify it to their heart’s content. And a new version of the GPL has been released, AGPLv3, which requires that people who use its software in web applications make their software available to the application’s users under its free terms.

But only a completely asocial web application consists purely of software. The vast majority of them are interesting because they give you access to data contributed by other users as well. For example, the software that lets people edit web pages is just about the least interesting thing about Wikipedia. The reason the site is so popular is because so many people have put their accumulated knowledge into that software.

Wikipedia has addressed this by going one step further — not only is the source code free, the data is too. Anyone can download a copy of the Wikipedia database (excluding users personal information) and start up their own copy of Wikipedia based on it. And then they can modify their copy of Wikipedia’s software to work however they please.

It’s beautiful in theory, but in practice, of course, nobody does this. Even if your version of Wikipedia was full of fantastic new features, it would still be nearly impossible to get anyone to use it. People use Wikipedia because that’s where all the other people are; it’s practically impossible to get everyone to switch.

For Wikipedia, the problem is somewhat ameliorated by having some pseudo- democratic control over the site. So Wikipedia is run by a board elected by (a tiny subset) of its users and the board has nominal control over the software and modi- fications that get made to it. But this is still a far cry from the freedom GNU/Linux users have in the non-networked world. Running for office, getting elected, then pushing your patches through a change-resistant bureaucracy is a lot more difficult than modifying some source code files on your computer and restarting.

And so, the hard-core partisans of software freedom propose that we will see the pendulum once again swing away from centralized server computing and back to a world where we all run applications on our local machines. Only this time, instead of being applications that don’t use the network or only talk to a distant
server, they will be peer-to-peer applications, seeking out other users and interacting with them directly.

Some great strides have been made in building peer-to-peer software, in no small part because of the vast amount of interest in using the technology to share music without getting caught by enforcers of the law. But, especially compared to Web 2.0 server technology, peer-to-peer is still in its infancy. Writing a social application so that its peer-to-peer is about a thousand times harder than writing the same program as a web app.

Still, peer-to-peer software, if we could make it work, would seem to give the best of both worlds: the freedom to modify how a program functions on our local computers as well as the ability to share and collaborate with others across the Internet. And so, for those who care about freedom (as well as those who care about sharing music), this seems like an important avenue for further research.

In the meantime, even if, like the question of how to query across many large SPARQL databases, the problems of web application freedom are unsolved, you can still do get started. The Open Knowledge Foundation, a group promoting freely shared databases, has proposed an Open Software Service Definition.http://opendefinition.org/ossd.() The definition essentially codifies the principles we discussed above:

1. Make your code available as free or open source software

2. Make your data available as Open Knowledge

For free/open source software, there’s the official lists of the Open Source Initiative and Free Software Foundation to tell whether your license is sufficiently free and open. Examples include the Expat/BSD license, the GPL, etc. The Open Knowledge Foundation similarly lists a series of licenses including some Creative Commons licenses, the GNU Free Documentation License, and so on.

That’s the legal details, but the technical ones are just as simple: provide a source code repository for all your code and SQL dumps for all your data.

Of course, this leaves a lot of open questions. What about private data, for example? My own feeling is that people should at least be allowed to download their own data and any data they can access through the Web interface — e.g. the data about your friends on Facebook.

And there’s lots of room for experimenting in building sites that promote more Democratic control. Maybe you can try some things and tell me about them and they’ll make them into the second edition of this book.
