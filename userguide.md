---

layout: doc  
title: "The vfmd userguide"  
permalink: userguide/  
license: http://vfmd.github.io/vfmd-spec/LICENSE.txt  
license-link-text: "the BSD license"  

---

# The vfmd userguide

**vfmd** is a variant of [Markdown] with an unambiguous specification of
its syntax.

This document describes the vfmd syntax in simple terms, and is intended
to be of help for people writing in vfmd.

The vfmd syntax is pretty much the same as the [original Markdown
syntax], with a few minor changes and added clarifications.

vfmd enables you to represent rich-text markup in plain-text files. It
supports block-level markup like lists, blockquotes and code-blocks, and
also supports span-level markup like emphasis, links and inline-code.

[original Markdown syntax]: http://daringfireball.net/projects/markdown/syntax
[Markdown]: http://daringfireball.net/projects/markdown/

## Table of contents

  * [Encoding]
  * [Block-level elements]
      * [Headers]
          * [setext-style headers]
          * [atx-style headers]
      * [Code blocks]
      * [Blockquotes]
      * [Lists]
      * [Horizontal rule]
  * [Mixing HTML with vfmd]
      * [Using vfmd along with HTML markup]
      * [Verbatim HTML]

<h2 id="encoding">Encoding</h2>

[Encoding]: #encoding

The input text should be in UTF-8 encoding. If you are writing your vfmd
document in English, it is most likely in UTF-8. If you are writing in
another language, please make sure that the document is in UTF-8
encoding (for example, if you are using a text editor to write the
document, ensure that it saves the document in UTF-8 encoding).

<h2 id="block-level-elements">Block-level elements</h2>

[Block-level elements]: #block-level-elements

<h3 id="headers">Headers</h3>

[Headers]: #headers

vfmd supports both [setext]-style and [atx]-style headers.

[setext]: http://docutils.sourceforge.net/mirror/setext.html
[atx]: http://www.aaronsw.com/2002/atx/

<h4 id="setext-style-headers">setext-style headers</h4>

[setext-style headers]: #setext-style-headers

To create a setext-style header, follow the header text with a line that
"underlines" the text with equal signs (`=`) or dashes (`-`).

For a first-level header, the "underline" line should be sequence of one
or more `=` characters. For a second-level header, it should be a
sequence of one or more `-` characters. There can be no other characters
in the "underline" line (trailing spaces are okay).

For example:

    This is a first-level header
    ============================

    This is a second-level header
    -----------------------------

    This is a first-level header
    ===

    This is a second-level header
    ---

Please note that in case the header is in the immediate next line of a
paragraph, it will be considered as a part of the paragraph, and shall
not be identified as a header.

    This is a paragraph. If you don't inculde a blank line
    between this paragraph of text and the title of the next
    section, the title will not be recognized as a title.
    This will not be recognized as a section title
    ----------------------------------------------

    If you do include a blank line between the paragraph and
    the title, it all works out correctly.

    This is a section title
    -----------------------

<h4 id="atx-style-headers">atx-style headers</h4>

[atx-style headers]: #atx-style-headers

atx-style headers start with one or more `#` characters. The first-level
header starts with a single `#`, second-level headers with `##`,
third-level headers with `###`, and so on, till 6 `#` characters for a
sixth-level header.

For example:

    # Title (first-level header)

    ## Section (second-level header)

    ### Subtitle (third-level header)

    ###### Sixth-level header

    ######### Still a sixth-level header

You may optionally "close" the header with any number of additional `#`
characters. However, the header level is determined only by counting the
"opening" `#` characters.

For example:

    ## Second-level header ##

    ### Third-level header ######

    ###### Sixth-level header #

Please note that in case the header is in the immediate next line of a
paragraph, it will be considered as a part of the paragraph, and shall
not be identified as a header.

    This is a paragraph. If you don't inculde a blank line
    between this paragraph of text and the title of the next
    section, the title will not be recognized as a title.
    # This will not be recognized as a section title

    If you do include a blank line between the paragraph and
    the title, it all works out correctly.

    # This is a section title

<h3 id="code-blocks">Code blocks</h3>

[Code blocks]: #code-blocks
[code block]: #code-blocks

Code blocks can be used to quote text verbatim. For example, it can be
used to quote source code. Every line of the code block should be
indented by 4 space characters.

No Markdown syntax is processed within a code block. In addition, for
HTML output, ampersands (`&`) and angle brackets (`<` and `>`) within a
code block are automatically converted into HTML entities, so that the
text appears as specified when the output HTML in viewed in a browser.

For example:

    Consider the following snippet that mixes Markdown with HTML5:

        ## Introduction

        This is <del>normal text</del> an intro.

becomes, in HTML output:

    <p>Consider the following snippet that mixes Markdown with HTML5:</p>

    <pre><code>## Introduction

    This is &lt;del&gt;normal text&lt;/del&gt; an intro.
    </pre></code>

If you'd like to have two code blocks one after the other, please use
two blank lines to separate them.

<h3 id="blockquotes">Blockquotes</h3>

[Blockquotes]: #blockquotes
[blockquote]: #blockquotes

Blockquoting is done by starting a line with `>` characters, like it's
done in email. It looks best if you hard wrap the text and start every
line with a `>`, like this:

    > 'Very true,' said the Duchess: 'flamingoes and mustard both
    > bite.  And the moral of that is - "Birds of a feather flock
    > together."'
    >
    > 'Only mustard isn't a bird,' Alice remarked.
    >
    > 'Right, as usual,' said the Duchess: 'what a clear way you
    > have of putting things!'

But you are allowed to skip the leading `>` for subsequent lines of a
hard-wrapped paragraph, as long as the first line of the paragraph
starts with a `>`. If there's only one blank line between multiple
blockquoted paragraphs, they form a single blockquote, like this:

    > 'Very true,' said the Duchess: 'flamingoes and mustard both
    bite.  And the moral of that is - "Birds of a feather flock
    together."'
    
    > 'Only mustard isn't a bird,' Alice remarked.
    
    > 'Right, as usual,' said the Duchess: 'what a clear way you
    have of putting things!'

If you'd like to have two blockquotes one after the other, please use
two blank lines to separate them.

Blockquotes can contain other elements, like headers, code blocks and
nested blockquotes.

For example:

    > ## Section header
    >
    > This is a paragraph inside a blockquote.
    >
    > > This is a nested blockquote.
    > > The second line of the nested blockquote.
    > > > This is the third level of nesting.
    >
    > Some code that gives the ultimate answer of
    > _Life, the Universe and Everything_:
    >
    >     int main() {
    >         return 42;
    >     }

Blockquotes should be separated from other block-level elements with a
blank line. However, a preceding blank line is not necessary for nested
blockquotes.

For example:

    This text should be followed by a blank line
    before the blockquote can begin.

    > But within the blockquote, nested blockquotes
    > can start without being separated by a blank
    > line.
    > > This is a nested blockquote
    > > that starts without a preceding blank line


<h3 id="lists">Lists</h3>

[lists]: #lists

A numbered list is created by numbering each item in the list, like
this:

     1. Donuts
     2. Chocolate
     3. Cupcakes

The numbers used in the list need not necessarily be ordered - the
output will have them in the right order anyway. However, the number
used for the first item will be used as the starting number for the
list.

A bulleted list is created by using asterisks(`*`) or pluses (`+`) or
hyphens (`-`) as list marker characters, like this:

      * Donuts
      * Chocolate
      * Cupcakes

The list marker character can be placed at the left margin, or may be
indented by up to three spaces, and must be followed by one or more
spaces.

When you change the list marker character, or change the number of
spaces before/after the list marker, each set of uniform list markers
form a separate list. For example, the following forms four top-level
lists placed one after the other:

     *  Donuts
     *  Chocolate
     *  Cupcakes
     +    Banana
     +    Apple
     +    Kiwi
       + The Fellowship of the Ring
       + The Two Towers
       + The Return of the King
     -   Tomato
     -   Cucumber

If a list item is separated by blank lines on both sides, the HTML
output shall wrap that item with `<p>` tags.

For example, this input:

    * Bird
    * Plane
    * Superman
    * UFO
    * Paper plane
    * Dragonfly
    * Helicopter

will turn into:

    <ul>
    <li>Bird</li>
    <li>Plane</li>
    <li>Superman</li>
    <li>UFO</li>
    <li>Paper plane</li>
    <li>Dragonfly</li>
    <li>Helicopter</li>
    </ul>

But this:

    * Bird
    * Plane

    * Superman

    * UFO

    * Paper plane
    * Dragonfly
    * Helicopter

will turn into:

    <ul>
    <li>Bird</li>
    <li>Plane</li>
    <li><p>Superman</p></li>
    <li><p>UFO</p></li>
    <li>Paper plane</li>
    <li>Dragonfly</li>
    <li>Helicopter</li>
    </ul>

If every list item is separated by blank lines, then each of them will
get wrapped in `<p>` tags in the HTML output.

Each list item can contain multiple paragraphs. To make lists look
nice, you can indent all lines within each list item to vertically align
with the starting paragraph of the list item, like this:

    *   Lorem ipsum dolor sit amet, consectetur adipiscing elit.

        Ut pulvinar, odio a luctus molestie, sapien libero
        hendrerit risus, a mollis quam ipsum non purus.

        Integer dignissim faucibus metus a aliquet. Nulla vitae
        neque mattis, cursus ipsum a, bibendum lorem. Phasellus
        dignissim neque nec libero sollicitudin, nec tempor orci
        vehicula.

    *   Vivamus non mauris massa. Aliquam hendrerit feugiat
        vulputate. Ut quis justo dapibus, tempor sem ut,
        ullamcorper sem.

But if you want to be lazy, you don’t have to, as long as the first
lines of the paragraphs are indented to align vertically:


    *   Lorem ipsum dolor sit amet, consectetur adipiscing elit.

        Ut pulvinar, odio a luctus molestie, sapien libero
    hendrerit risus, a mollis quam ipsum non purus.

        Integer dignissim faucibus metus a aliquet. Nulla vitae
    neque mattis, cursus ipsum a, bibendum lorem. Phasellus
    dignissim neque nec libero sollicitudin, nec tempor orci
    vehicula.

    *   Vivamus non mauris massa. Aliquam hendrerit feugiat
    vulputate. Ut quis justo dapibus, tempor sem ut, ullamcorper
    sem.

A list item can contain other block-level elements, like blockquotes,
headers, code blocks and nested lists. Any nested element should be
indented to align vertically with the starting paragraph of the list
item.

    -   List item with a blockquote. The blockquote should be indented
        to align with the starting position of this paragraph.

        > This is a blockquote
        > inside a list item

    -   List item with a code-block. The code-block should be indented
        by 4 spaces from the starting position of this paragraph.

            int main() {
                return 42;
            }

    -   List item with two nested lists. The lists can be indented
        by 0 to 3 spaces from the starting position of this paragraph.

         - First
         - Second
         - Third

         1. One
         2. Two
         3. Three

You can force-end a list with two consecutive blank lines. You can use
this technique to write two numbered lists one after the other, or to
have a code-block immediately after a list.

Lists should be separated from other block-level elements with a blank
line. However, a preceding blank line is not necessary for nested lists.

For example:

    This text should be followed by a blank line
    before the list can begin.

     *  But within the list, nested lists can
        start without being separated by a
        blank line.
         * Item 1 of nested list
           1. Second level of nesting
           2. Still second level of nesting
         * Item 2 of nested list
         * Item 3 of nested list


<h3 id="horizontal-rule">Horizontal rule</h3>

[Horizontal rule]: #horizontal-rule

A horizontal rule tag (`<hr/>`) can be created by placing three or more
hyphens (`-`), or three or more underscores (`_`) or three or more
asterisks (`*`) on a line by themselves. The hyphens (or the
underscores, or the asterisks) forming the horizontal rule can
optionally be interspersed with spaces.

Each of the following lines results in a horizontal rule:

    ***

    *****

    * * * *

    -------------
    _   _   _   _   _   _   _

    -- --- --

But the following lines don't result in a horizontal rule:

    **

    --

    *-*-*

    _-_-_-_


<h2 id="mixing-html-with-vfmd">Mixing HTML with vfmd</h2>

[Mixing HTML with vfmd]: #mixing-html-with-vfmd

If you are capable of authoring HTML documents, you can use snippets of
HTML in your vfmd document to augument the vfmd feature set. That said,
if you would like to convert a vfmd source document to any output format
other than HTML, the support for using HTML tags in the vfmd source
document is implementation-dependant.

vfmd handles different HTML elements differently. In vfmd, HTML elements
are seen as belonging to one of the following four groups:

 1. <span id="phrasing-html-elements">**Phrasing HTML elements** are
    HTML elements that belong to the [phrasing content] category in
    [HTML5].</span> The elements in this group are: `a`, `abbr`, `area`,
    `audio`, `b`, `bdi`, `bdo`, `br`, `button`, `canvas`, `cite`,
    `code`, `data`, `datalist`, `del`, `dfn`, `em`, `embed`, `i`,
    `iframe`, `img`, `input`, `ins`, `kbd`, `keygen`, `label`, `map`,
    `mark`, `meter`, `noscript`, `object`, `output`, `progress`, `q`,
    `ruby`, `s`, `samp`, `select`, `small`, `span`, `strong`, `sub`,
    `sup`, `textarea`, `time`, `u`, `var`, `video` and `wbr`.

 2. <span id="verbatim-html-starter-elements">**Verbatim HTML starter
    elements** are HTML elements that are [flow content], but not
    [phrasing content], and can in turn [contain][content models] [flow
    content].</span> The elements in this group are: `address`,
    `article`, `aside`, `blockquote`, `details`, `dialog`, `div`, `dl`,
    `fieldset`, `figure`, `footer`, `form`, `header`, `main`, `nav`,
    `ol`, `section`, `table` and `ul`.

 3. <span id="verbatim-html-container-elements">**Verbatim HTML
    container elements** are HTML elements within which vfmd syntax
    should never be recognized.</span> `pre`, `style` and `script`
    elements fall in this group.

 4. <span id="other-html-elements">**Other HTML elements** are HTML
    elements that don't belong to any of the above groups.</span>

[HTML5]: http://www.w3.org/TR/html5/ "HTML5 Specification"
[content models]: http://www.w3.org/TR/html5/dom.html#content-models
[flow content]: http://www.w3.org/TR/html5/dom.html#flow-content-1
[phrasing content]: http://www.w3.org/TR/html5/dom.html#phrasing-content-1
[Phrasing HTML elements]: #phrasing-html-elements
[phrasing HTML elements]: #phrasing-html-elements
[Verbatim HTML starter elements]: #verbatim-html-starter-elements
[verbatim HTML starter elements]: #verbatim-html-starter-elements
[Verbatim HTML container elements]: #verbatim-html-container-elements
[verbatim HTML container elements]: #verbatim-html-container-elements
[Other HTML elements]: #other-html-elements
[other HTML elements]: #other-html-elements


<h3 id="using-vfmd-along-with-html">Using vfmd along with HTML markup</h3>

[Using vfmd along with HTML markup]: #using-vfmd-along-with-html

[Phrasing HTML elements] can be freely intermingled with vfmd text. Such
HTML elements can contain, and be contained in, vfmd markup.

For example:

    According to the <u>_Special_ Theory of Relativity</u>,
    **E** <em>(energy)</em> = **mc<sup>2</sup>**

becomes, in HTML output:

    <p>According to the <u><em>Special</em> Theory of Relativity</u>,
    <strong>E</strong> <em>(energy)</em> = <strong>mc<sup>2</sup></strong></p>

[Other HTML elements] can contain vfmd text, but cannot be contained
within vfmd markup. Moreover, vfmd paragraphs containing any of the
[other HTML elements] are not wrapped in `p` tags.

The following example shows how vfmd markup can be used within `td`
elements of a HTML table:

    <td>Apply some _stress_</td>
    <td>Make it sound **important**</td>

The HTML output for the above example shall not have any `p` tags:

    <td>Apply some <em>stress</em></td>
    <td>Make it sound <strong>important</strong></td>

Also, if the vfmd paragraph contains any mismatched or misnested HTML
tags (i.e. opening tags without correctly-placed closing tags or vice
versa), vfmd will not wrap the paragraph content in `p` tags, because
doing so might result in invalid HTML output.

<h3 id="verbatim-html">Verbatim HTML</h3>

[Verbatim HTML]: #verbatim-html

Anything within a [verbatim HTML container element] \(i.e. a `pre`,
`script` or `style` element\) is preserved as-is in the HTML output.

Moreover, any tag (opening, closing or self-closing tag) of a [verbatim
HTML starter element] marks the start of verbatim HTML, and the
verbatim-HTML-mode stays on till the next blank line.

So, if you'd like to use vfmd syntax within a [verbatim HTML starter
element] \(like `div` or `table`\), you can use one or more blank lines
to separate the parts that need to be output verbatim, from the parts in
which vfmd syntax needs to be processed.

For example, for the input:

    <table>
      <tr>
        <th>Single *asterisk* or _underscore_</th>
        <th>Double **asterisks** or __underscores__</th>
      </tr>
      <tr>

    <td>Apply some _stress_</td>
    <td>Make it sound **important**</td>

      </tr>
    </table>

The corresponding HTML output shall be:

    <table>
      <tr>
        <th>Single *asterisk* or _underscore_</th>
        <th>Double **asterisks** or __underscores__</th>
      </tr>
      <tr>

    <td>Apply some <em>stress</em></td>
    <td>Make it sound <strong>important</strong></td>

      </tr>
    </table>

However, please make sure that the starting line of each snippet of HTML
is not indented by more than 3 spaces (if it's indented by 4 or more
spaces, it would become a [code block]).

On the contrary, if you want the whole block of HTML reproduced verbatim
in the HTML output, make sure that there are no blank lines in the
content of any of the HTML elements.

For example:

    <table>
      <tr>
        <th>Single *asterisk* or _underscore_</th>
        <th>Double **asterisks** or __underscores__</th>
      </tr>
      <tr>
    <td>Apply some _stress_</td>
    <td>Make it sound **important**</td>
      </tr>
    </table>

The text within the `td` tags in the above example shall not be
processed as vfmd, and shall be reproduced as-is in the HTML output.

Note that `pre`, `script` or `style` elements can have blank lines
enclosed within, and those blank lines don't cause the
verbatim-HTML-mode to end.

<h3 id="html-blocks-within-blockquotes-and-lists">
HTML blocks within blockquotes and lists</h3>

[HTML blocks within blockquotes and lists]: #html-blocks-within-blockquotes-and-lists

When including a HTML block within a [blockquote], please make sure that
the HTML block is completely contained within the [blockquote].

For example, the following is wrong, and will result in invalid HTML
output:

    > This is a blockquote.
    > Below is a HTML block inside the blockquote.
    >
    > <div>
    > Inside the blockquote and inside the div block

    Outside the blockquote
    </div>

To correctly include the HTML block within the [blockquote], please use
the `>` prefix for all the lines in the HTML block (or atleast for any
line following a blank line in the HTML block).

    > This is a blockquote.
    > Below is a HTML block inside the blockquote.
    >
    > <div>
    > Inside the blockquote and inside the div block
    >
    > Still inside the blockquote
    > </div>

Similarly, when including a HTML block within a list, please make sure
that the HTML block is completely contained within the list.

For example, the following is wrong, and will result in invalid HTML
output:

     1. This is a list.
        Below is a HTML block inside the list.

        <div>
        Inside the list and inside the div block

    Outside the list
    </div>

Instead, please indent all the lines of the HTML block (or atleast the
lines following a blank line) to line up with the list.

     1. This is a list.
        Below is a HTML block inside the list.

        <div>
        Inside the list and inside the div block

        Still inside the list
        </div>

<h3 id="matching-open-and-close-html-tags">
Matching open and close HTML tags</h3>

[Matching open and close HTML tags]: #matching-open-and-close-html-tags

When you use HTML tags within the vfmd document, please take care to
correctly match up the open tags with the close tags. Any mismatched or
misnested HTML tags will remain mismatched or misnested in the output
HTML as well. Some implementations might clean up the invalid HTML, but
then their output might not really match what you intended in your
input. The best way to be clear about your intent is to provide
correctly matching HTML tags in the vfmd source document.

In addition, span-level vfmd markup will not be recognized
across mismatching or misnested HTML tags. 

For example, the asterisks in the following vfmd input are not
interpreted to mean strong emphasis:

    Cannot span **across <b><i>misnested</b></i> HTML tags** _at all_

For them to be recognized as vfmd markup, the HTML tags should be fixed
to nest correctly:

    Can span **across <b><i>correctly nested</i></b> HTML tags** _anytime_

So, when mixing HTML with vfmd, please ensure that the open HTML tags
and the close HTML tags you insert match up correctly.
