---
title: "Building a Database"
date: 2018-04-06T23:23:23+02:00
draft: true
---

Chapter 6

# Building a Database: Queries and Dumps

APIs are nice and all, but they’re fairly limiting: they only give you the answers to questions you already know how to ask. Want to find out more about book 3j7is? Sure, it’ll tell you. But want to know which books published recently share an author with a book published over a hundred years ago? That’s a little more complicated.
But, luckily, not impossible. It seems ridiculous to come up with your own API that could answer any sort of question like this. But remember those RDF query languages we were making fun of in the last chapter? This turns out to be just the sort of thing they’re perfect at.
The official RDF query language is called SPARQL (SPARQL Protocol And RDF Query Language—pronounced “sparkle”). If you’re familiar with SQL, the standard database query language, SPARQL will look similar, only with RDF stuck in all the right places. Here’s how you express our previous question in SPARQL:

```
>     PREFIX : <http://books.example.org/api/schema#>
>     SELECT ?booknew, ?bookold
> WHERE {
>
>
>
>
>
> >}
?booknew :author ?author .
?booknew :publication_year ?yearnew .
FILTER ( ?yearnew >= 2008 )
?bookold :author ?author .
?bookold :publication_year ?yearold .
FILTER ( ?yearold <= 1908 )
```

There’s a lot there, so let’s go through is slowly. First we just declare the prefixes for our URIs, as usual. This is just to save us some typing. Then we say that we want the values “?booknew” and “?bookold” returned for us. In SPARQL, anything beginning with ‘?’ is a placeholder that the query engine will try to find something to fit into.

The “WHERE” clause puts constraints on what can fit in those placeholders. “?booknew” has to have an author and a publication year and that publication year has to be equal to or larger than 2008. “?bookold” also has to have an author and a publication year—and furthermore, its author has to be the same as “?booknew”’s author. But its publication year has to be equal or less than 1908.

Now because SPARQL is designed to work at web-scale, you don’t have to just keep this query at home. Instead, you can point it at another server’s search system, called a SPARQL endpoint. You may not have a lot of information about books, but books.example.org probably does—you can have it search for things that match your query.

To do so, you just take the query we generated above and stick into a properly formatted URL. And—boom!—back comes your list of answers.

Now another neat thing about SPARQL is that, done right, it can spread these queries across multiple SPARQL endpoints. So, for example, we can imagine writing a query for books whose authors were Jewish. The information about books and authors we can get from the bookserver, while Wikipedia (whose RDF version is called DBPedia) can tell us about people’s religion. Of course, figuring out how to structure these queries in such a way that they don’t take forever is an ongoing research project.

In the meantime, we can at least help those who can help themselves to our data, by providing bulk dumps. The theory here is simple: there are lots of queries and merges and visualizations people will want to do with your data that are going to be impractical to do through any sort of API, even one as fancy as SPARQL. So you might as well just give them a full copy of the data set.

And the practice is even simpler: just take the JSON you generate for each item on your site and put it in one big file.

You may want to compress it, since it’ll probably be quite large.
