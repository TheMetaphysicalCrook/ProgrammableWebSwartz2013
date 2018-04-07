---
title: "Conclusion"
date: 2018-04-06T23:23:23+02:00
draft: true
---

Chapter 8

# Conclusion: A Semantic Web?

Well, we’ve been through a lot together, you and I. We’ve built up an application from its humble URLs to its high-falutin’ notions of democracy. Along the way, we’ve made its world safe for robots, query systems, researchers, and Richard Stallman. But how do we get from this kind of website to the grand vision of the Semantic Web we’ve heard so much about?

Let’s start by realizing that just being on the Web is an amazing thing. URLs provide a unified addressing scheme for any document — a pretty miraculous thing. Imagine trying to explain to folks of yesteryear about these incredible words which you could give to anyone and they could take it home, punch it into a box they have on their desk, and get just the article, picture, or video you meant. To a generation whose idea of document retrieval is driving to the local library, filling out some forms, and waiting a few weeks while they tried to make sense of your subscription and hunt it down, this is a pretty serious change.

But REST took it even further. By making the documents accessible by search engines through a standard protocol, you no longer even need to know the right URL for the thing you want. Just type a few choice words into Google and boom! back comes just the thing you wanted in a quarter of a second.

Of course it’s not just Google; REST makes possible an interconnected tapestry that supports everything from web browsers to web editors to intelligent translating intermediary proxies.

A hard act to follow. But then came the ability to get not just documents back from these far-off servers, but data. By importing and exporting raw data, we made it possible to switch software programs, providing a somewhat-free market of competition among products, creating massive consumer surplus. Go us!

But we didn’t stop there. Just letting users take their data home with them is weak brew compared to sharing it with the wider world. (Picture a wide world of
people at home with their weak data brew.) Which is why the Web invented APIs, letting us share the data with everyone who could think of a use for it.

Now we’re not just a simple website, pushing pages to the browser and pro- viding a “See also:” like list of other pages one can visit. We’re actually exchanging the data itself from application to application, making possible a new world of mashups and intelligent applications.

This is an entirely new notion of the tapestry — a tapestry of data instead of a tapestry of documents. Documents can’t really be merged and integrated and queried; they serve mostly as isolated instances to be viewed and reviewed. But data are protean, able to shift into whatever shape best suits your needs.

But as our needs grow more varied, we need better ways to get at the data that will best serve them. Which is where our queries and dumps come in. No longer are we hampered by only being able to ask the questions a site’s programmers have expected and accounted for; now we can ask whatever questions we like, or do processing that can’t even be put in the form of a question at all. Combining these dumps from different data sources, the possibilities are endless.

But where do we go from here?

Obviously the first step is to take the large dumps we’ve all made and load them into one big database. And, of course, we’ve started to see people do that, from research projects to commercial companies like Metaweb’s Freebase. Freebase is an enormous collaborative Web-editable RDF-like database, prepopulated with data extracted from Wikipedia and numerous other sources and supplemented with the contributions of various users. Freebase is still quite small, but their aims are ambitious — creating a database that combines numerous different sources and providing it as a backend to people who want to build more intelligent applications.

Ideally, of course, intelligent applications won’t be dependent on a single commercial site, like Freebase, but will merge and combine knowledge from various sites across the Web, crawling and trawling for more useful information and deciding which bits of it to trust.

Already we’re seeing things like this in research projects. One of the most exciting Semantic Web tools is a program called cwm, hacked together between (or during) meetings by Sir Tim Berners-Lee himself. Cwm (pronounced coom) is one of the most amazing programs I’ve seen; it’s a veritable data swiss-army knife, all built on RDF.

Of course it does all the basics — reading and writing RDF files of various formats, combining multiple files, printing all the results out in a pretty format.

Naturally, it can also search through the resulting data to answer your questions in much the same way SPARQL does.

But cwm goes a step further. It doesn’t just search through data; it thinks about it. cwm can follow logical rules; take this one for example:

    { ?x a :Man } => { ?x :mortality :mortal } .

(If something is a man, then it’s mortal.) Feed this into cwm, along with:

    :Socrates a :Man .

And it will logically deduce that Socrates is mortal. Such rulesets obviously have all sorts of uses, from logical parlor games to actual programming. But one obvious use is providing conversions between different RDF formats. Imagine two schemas: “joe:”, which has “small”, “medium”, and “large” and “starbucks:” which has “short”, “tall”, “grande”, and “venti”. Now we can just write a few rules to convert between them:

    { ?x joe:size joe:small }  <=>
    { ?x starbucks:size starbucks:tall } .
    { ?x joe:size joe:medium } <=>
    { ?x starbucks:size starbucks:grande } .
    { ?x joe:size joe:large }  <=>
    { ?x starbucks:size starbucks:venti } .

Feed these rules into cwm, along with the data in one format, and cwm will “think” about it and spit out data in the other format.

But cwm can do much more than just basic logical inference. It also has a wide variety of built-ins, that can do everything from mathematical processing to advanced cryptography. With them, and some clever rules, you can even build entire programs using cwm.

Incidentally, none of this is new — nearly all this stuff was written in 2001.

cwm is also smart enough to go onto the Web and find more rules like these, crawling through web pages for more bits of RDF to make it smarter. Following links and URLs and getting more data, it can surf the Web for data in the same way a bored teenager surfs the Web for fun.

If you’re interested in giving this process a spin for yourself, you can try Tim’s latest project: the Tabulator. It’s a little add-on to your web browser that lets it see
RDF documents in addition to regular web pages. Suddenly documents aren’t just a list of boring tags or text, but a pathway of clickable links you can follow to your heart’s content. (And, with later versions, you can even edit some of the fields.)

One can imagine tools like cwm and Tabulator sitting behind the applications we use every day, enhancing them with knowledge drawn from the wider Web.

For that’s the real idea behind the Semantic Web: letting software use the vast collective genius embedded in its published pages. Think of all the places software uses APIs or databases: your spellchecker queries a website to find the definition of a word, your addressbook does a search to see if your friends are online, your calendar downloads a page to keep you posted on upcoming events. Now, imagine these programs weren’t limited to one particular site, but could draw on the intelligence of the Internet at large.

Your spellchecker can suggest related or alternate words, or just keep up to date with the latest slang. Your address book can tell you where your friends are right now and what they’ve been up to lately. Your calendar can keep an eye out for events you might be interested in.

It’s easy to make fun of these kinds of visions. My father, upon seeing such demos, always used to ask, “But why does your toaster need to know about stock prices?” And perhaps, ultimately, they’re not worth all the effort. But the Semantic Web is based on bet, a bet that giving the world tools to easily collaborate and communicate will lead to possibilities so wonderful we can scarcely even imagine them right now.

Sure, it sounds a little bit crazy. But it paid off the last time they made that gamble: we ended up with a little thing called the World Wide Web. Let’s see if they can do it again.
