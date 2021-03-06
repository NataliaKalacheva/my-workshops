Basic Schema Markup / Structured data
=====================================

Schema Markup, alse called Structured data
------------------------------------------

it is code that you place on your website to help search engines return
more meaningful results to users. Schematic markup allows you to create
rich descriptions that appear in search results.

Rich snippets, alse called Rich Results
---------------------------------------

Rich Snippets are normal Google search results with additional data
displayed. This extra data is usually pulled from Structured Data found
in a page's HTML. Common Rich Snippet types include reviews, recipes and
events.

Examples
--------

![Rich results 1](pictures/example1.png) ![Rich results
2](pictures/example2.png)

How to implement? / Microdata
-----------------------------

With microdata, you can specify structured data information in the HTML
itself using the attributes of HTML tags. \
 + easy to add manually \
 - it is difficult to scale and automate when needed for larger websites
(eg e-commerce).

![Schema markup](pictures/schema-markup-screenshot.png)

By adding **itemscope**, you are specifying that the HTML contained in
the block is about a particular item.

By adding **itemtype**, you are specifying specifying what kind of an
item it is.

To label properties of an item, use the **itemprop** attribute.

How to implement? / RDFa
------------------------

RDFa is similar to Microdata, which means it’s also added through HTML
tag attributes. The difference is that RDFa is older and more complex.
It has other uses outside of the HTML realm and this means integration
with other apps/platforms/servers is easier if they use the technology.

![Schema markup](pictures/rdfa-code-example.jpeg)

How to implement? / JSON-LD
---------------------------

JSON-LD (JavaScript Object Notation for Linked Data) is a technique for
encoding and representing information about structured data using JSON.
This is recommended by the W3C and Google, which means it is
standardized.

![Schema markup](pictures/example-of-json-ld.jpeg)

Testing tools
-------------

[Rich Results Test](https://search.google.com/test/rich-results)

[Structured data testing
tool](https://search.google.com/structured-data/testing-tool/u/0/)

Documentation
-------------

-   [https://schema.org/Thing](https://schema.org/Organization)

