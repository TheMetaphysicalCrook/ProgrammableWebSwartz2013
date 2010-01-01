---
title: "Building a Platform"
date: 2018-04-06T23:23:23+02:00
draft: true
---

Chapter 5

# Building a Platform: Providing APIs

The other week I made one of my rare excursions from my plushly-appointed bed and attended a local party. There I met a man who made a website for entering and visualizing data. I asked him whether he had an API, since it seemed so useful for such a data-intensive site. He didn’t, he said; it would be too much work to maintain both a normal application and an API.

I tell you this story because the fellow at the party was wrong, but probably in the same way that you are wrong, and I don’t want you to feel bad. If even well- dressed young startup founders at exclusive Williamsburg salons make this mistake, it’s no grave sin.

See, the mistake is, that if you design your website following the principles in this book, the API isn’t a separate thing from your normal website, but a natural extension of it. All the principles we’ve talked about—smart URLs, GET and POST, etc.—apply equally well to web sites or APIs. The only difference is that instead of returning HTML, you’ll want to return JSON instead.

JSON (pronounced like “Jason”), for the uninitiated, is a simple format for exchanging basic pieces of data between software. Originally based on JavaScript but quickly adopted by nearly every major language, it makes it easy to share data over the Web.

Wait!, you may cry, I thought XML was for sharing data on the Web. Sadly, you have been misled by a sinister and harmful public relations campaign. XML is probably just about the worst format for sharing data. Here’s why:

Modern programming languages have largely standardized on the same basic components of internal data structures: integers, strings, lists, hashes, etc. JSON recognizes this and makes it easy to share these data structures. Want to share the number 5? Just write ’5;. The string “foo” is just “foo”. A list of the two of them is simply “[5, “foo”]”—and so on.

This is easy for humans to write and read, but even more importantly, it’s automatic for computers to write and read. In most languages you don’t even need to think about the fact that you’re using JSON: you just ask your JSON library to serialize a list and it does it. Read in a JSON file and you it’s just like your program’s getting a normal data structure.

XML, on the other hand, supports none of this. Instead, it thinks in terms of elements with character data and programming instructions and attributes, all of which are strings. Publishing data as XML requires figuring out how to shoehorn your internal data into a particular format, then making sure you do all of your quoting properly. Parsing XML is even worse.

The main reason XML is so bad at sharing data is because it was never de- signed to do that in the first place. It was a format for marking up textual documents; annotating writing with formatting instructions and metadata of various sorts, ala HTML. This is why it does things like distinguish between character data and attribute data—attribute data is stuff that isn’t part of the actual text, ala:

```
> I’m looking forward to a <font color="green">
  successful</font> demonstration.
```

The word “green” is an annotation, not part of the text, so it goes in an attribute. All of this goes out the window when you start talking about data:

```
> <person age="5">
> <name>Robert Booker</name>
> </person>
```

Why is “age” an attribute while “name” is an element? It’s completely arbitrary, because the distinction makes no sense.

Alright, so XML has a few more features that nobody needs. What’s the harm in that? Well, it’s also missing a whole bunch of features that you do need— by default, XML has no support for even the most basic concepts like “integer;” it’s all strings. And adding it requires XML Schema, a specification so mind-numbingly complex that it actually locks up my browser when I try to open it.

But the costs of such complexity aren’t simply more work for developers— they really come in the form of bugs, especially security holes. As security expert Dan Bernstein observes, two of the biggest sources of security holes are complexity (“Security holes can’t show up in features that don’t exist”) and parsing (“The parser
often has bugs... The quoter often has bugs... Only on rare joyous occasions does it happen that the parser and the quoter both misinterpret the interface in the same way.”).(http://cr.yp.to/qmail/guarantee.html.)

XML combines the worst of both worlds: it is an incredibly complex system of parsing. Not surprisingly, XML has been responsible for hundreds of security holes.(http://cve.mitre.org/.)

So aside from being simpler, easier, more featureful, safer, and faster than XML, what does JSON have to offer? Well, it has one killer feature that’s guaran- teed its place atop the format wars: because it’s based on JavaScript, it has a deep compatibility with web browsers.

You’ve probably heard about AJAX, a technique that uses the XmlHttpRe- quest function in modern web browsers to allow web pages to initiate their own HTTP requests to get more data. But, for security reasons, XmlHttpRequest is only permitted to request pages on the same domain as the web page it initi- ates from. That is, if your page is at http://www.example.net/foo.html it can request things like http://www.example.net/info.xml but not http:// whitehouse.gov/data/dump.xml.

For APIs, this is kind of a disaster—the whole point of opening up your data on the web is so that other sites can use it. If you’re the only people who can access it, why go to the trouble?

Luckily, there’s one exception: JavaScript. A webpage can embed an HTML ‘<script>‘ tag that points to any random site on the Internet. Even better, JavaScript code can arbitrarily add these script tags to the page. The browser then goes and fetches the page and tries to process it.

Now with regular JSON that wouldn’t be too useful—the browser would download a list or an object or something and wouldn’t know what to do with it. So instead of just returning the JSON, it returns the JSON wrapped in a function call:

```
> myCallback([5, ‘‘foo"]);
```

Then you just have the function “myCallback” do whatever it was you wanted to do with the data.

Of course, if you’re doing lots of requests you’ll want to keep them all separate—they can’t all call myCallback. So you support a callback parameter that
lets you pick the function name. So a URL like http://www.example.net/ info.json?callback=foo would return:

```
> foo([5, ‘‘foo’’]);
```

The whole technique is known as JSONP and, naturally, it’s automated by all the major JSON libraries so you don’t have to worry about any of these details. Alright, so now that we have a pile of JSON, where do we put it. The answer,
of course, is the same place as your HTML. Going back to an older example, let’s say we have some information about a book at:

      http://books.example.org/b/3j7is

Where does the JSON go? At the very same place!

You see, HTTP has a nifty feature called Content Negotiation that allows for the same URL to return different formats depending on who’s requesting things. The classical example of content negotiation is the transition from GIF images to the newer PNG image format. Some older versions of Internet Explorer didn’t support PNG; servers could use Content Negotiation to send them older GIF images instead.

The way it works is that every time you make an HTTP request (like a GET), the client sends along a series of Accept headers saying what formats it likes. Here’s a typical example:

```
> Accept: text/html; q=1.0, text/*; q=0.8, image/gif; q=0.6, image/jpeg; q=0.6, image/*; q=0.5, */*; q=0.1
```

This says the browser prefers HTML, then takes text, then GIFs and JPEGs, then any other image, then anything else.

But for APIs we don’t need to do anything so complicated. We can just have our API clients send:

```
> Accept: application/json
```

and have the server keep an eye out for that and return the JSON version if it sees it. Otherwise, it serves the HTML as usual.

Of course, you’ll probably want to provide an option for people who can’t easily do Content Negotiation. So it’s traditional to let:

 http://books.example.org/b/3j7is.html

force the server to return HTML while

    http://books.example.org/b/3j7is.json

always returns JSON. (And then you could have:

    http://books.example.org/b/3j7is.json?callback=myCallback

to support JSONP.)

Alright, let’s get concrete. What might one of these JSON pages look like?

Let’s stick with our book example for a moment. You could imagine a book page looking something like:

```
>{
    >       ’id’: ’3j7is’,
    >       ’title’: ’The ABC book’,
    >       ’by_statement’: ’designed and cut on wood,
    >        by C. B. Falls.’,
    >       ’pagination’: ’ ̃\cite{bib30} p. incl. col. illus.’,
> ’description’: “An all-time favorite and a classic in its field, this big and beautiful ABC book by distinguished artist C. B. Falls has been making new friends with delighted children for over forty years.
Mr. Falls designed the book for his little three-year-old daughter who likes a big book with lots of pictures. The drawings are cut on wood blocks and printed from fourcolor plates, and the artist has personally superintended the reproduction of them. The imagination of a child or grown-up is left free to capture by its own thrill of recognition the familiar in a new-old medium where color has not obscured the outline nor played too many tricks with nature.,”
 > > >
’publisher’: ’Doubleday, Page & company’,
’authors’: [
  {’id’: ’OL115179A’, ’name’: ’C. B. Falls’}
> ], 
>}
```

And if your site let people update book pages, you could imagine supporting PUT requests on this URI that allowed people to submit an updated version of the JSON object. You’d parse it and then execute the update.

Or, if you just let people comments on books, you could let them POST simple JSON data to the same URI that comments are normally posted to.

In fact, if your really wanted, you could just let them POST form data and parse it the same way as you would input from web browsers. Then you could let them know success or failure via HTTP error codes—a 500 error would let them know it failed, while a 303 See Other redirect to the page itself would let them know they succeeded. When they followed the redirect and grabbed the page, it too could content negotiate to JSON.

***

Alright, now it’s time to talk about a touchy subject. I’ve been holding off on this, but at some point it becomes unavoidable. Yes, I’m afraid it’s time to talk about RDF.

You see, all this JSON stuff is great for writing little scripts on clients that talk to other scripts on servers, but it leaves something to be desired when working at Web scale. It’s hard to imagine, for example, building particularly useful tools that work across different JSON APIs, the way web browsers work across all different kinds of HTML pages. Each JSON API has its own internal representations and conventions and protocols, which means you need to write special code to deal with each different one.

That’s where RDF comes in. The idea behind it is simple: what if we had a format that did to data what HTML did to documents—provide a single, consistent representation for them that supports the hypertextual nature of the Web. That probably makes no sense, so let’s look at some examples.

RDF documents are quite simple—they’re made up of “triples,” simple sen- tences with three parts: a subject, a verb (called a predicate), and an object. Let’s take a bit of our example from before, namely that the book with ID 3j7is has the title “The ABC book”—in RDF, the subject would be “3j7is”, the verb “title” and the object the string “The ABC book”.

Only RDF is meant to work at webscale, so instead of fuzzy-wuzzy terms like “title”, everything’s a URI. As in:

```
>    <http://books.example.org/b/3j7is#it>
    http://www.w3.org/1999/02/22-rdf-syntax-ns#label
    ‘‘The ABC book’’ .
(Those ‘#’ signs are there to distinguish the fact that we’re talking about the concept described by a web page, rather than the web page itself.)
Of course, typing all those URLs out each time gets old fast, so we tend to abbreviate them:
    >    @prefix rdfs: <http://www.w3.org/1999/02
    >                         /22-rdf-syntax-ns#> .
    >
    >    <http://books.example.org/b/3j7is#it> rdfs:label
> ‘‘The ABC book’’.
Here’s a rough rendering of the above JSON in RDF:
    > @prefix : <http://books.example.org/api/schema#> .
    >
 > > > > >
<http://books.example.org/b/3j7is#it>
  :title ’The ABC book’;
  :by_statement ’designed and cut on wood,
   by C. B. Falls.’;
  :pagination: ’ ̃\cite{bib30} p. incl. col. illus.’;
:description “An all-time favorite and a classic in its field, this big and beautiful ABC book by distinguished artist C. B. Falls has been making new friends with delighted children for over forty years.
Mr. Falls designed the book for his little three-year-old daughter who likes a big book with lots of pictures. The drawings are cut on wood blocks and printed from fourcolor plates, and the artist has personally superintended the reproduction of them. The imagination of a child or grown-up is left free
to capture by its own thrill of recognition the familiar in a new-old medium where color has not obscured the outline nor played too many tricks with nature.;”
 > > > > >
  :publisher ’Doubleday, Page & company’;
  :author <http://openlibrary.org/a/OL115179A#it> .
<http://openlibrary.org/a/OL115179A#it>
:name ‘‘C. B. Falls’’ .
Aside from consistently using URIs, RDF has some pretty nice features. For one thing, something you want to do a lot with data is combine it, and RDF makes that very easy. To combine two RDF documents, you just concatenate them—it’s just a list of facts; two lists of facts together makes one long list of facts. It’s not quite as simple with JSON, let alone XML.
Another nice feature of RDF is that it makes it easy to map between formats. Converting between two JSON formats typically requires code, but with RDF you can just publish another RDF document that explains the mapping, like:
    >   rdfs:label = :title .
```

That way software that knows about “rdfs:label” know that they can use “:title” properties the same way.

RDF does have these many nice features, but it does have one big downside: it’s nowhere near as easy to use as JSON. Like XML, it has its own data model, which means writing special code to move between its way of viewing the world and yours. There are some tools and techniques to mitigate this (like my own rdftramp,(http://www.aaronsw.com/2002/rdftramp/.) which tries to make RDF look more like normal Python objects) but it’s still a serious problem.

The RDF world has tried to address it by writing RDF replacements for all the existing tools of the software world: RDF databases, RDF programming languages, RDF query systems, RDF browsers, RDF reasoning engines, and so on. If you want, there’s a whole world of RDF you can dive into.

Ultimately, however, I fear this isn’t a very promising strategy—it’s going to be hard to create replacements for all these things which are as good or better than
the original, and even if you do, people will still have sentimental attachments to the others.

So at this point, I would still categorize RDF as an aspiration. It would be nice as a universal publishing format—there’s a lot that cold be done with it—but for day-to-day work, JSON is much better.

That said, RDF is, of course, far, far preferable to XML.
