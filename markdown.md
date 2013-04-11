Markdown
========

In which we list tips, tricks, and reminders.

* [Style](#style)
* [Links](#links)
* [Images](#images)
* [Headers](#headers)
* [Lists](#lists)
* [Blockquotes](#blockquotes)
* [Code Spans](#codespans)
* [Code Blocks](#codeblocks)
* [Horizontal Rules](#rules)
* [Manual Line Breaks](#linebreaks)

Official documentation:

* [Main][1]
* [Basics][2]
* [Syntax][3]
* [Dingus][4] (for live testing)

[1]: http://daringfireball.net/projects/markdown  "Main"
[2]: http://daringfireball.net/projects/markdown/basics  "Basics"
[3]: http://daringfireball.net/projects/markdown/syntax  "Syntax"
[4]: http://daringfireball.net/projects/markdown/dingus  "Dingus"


<div class="spacer" style="margin: 50px"></div>

  
## <div id="style">Style</div>

*italic*   

    *italic*   

**bold**

    **bold**

_italic_   

    _italic_   

__bold__

    __bold__


## <div id="links">Links</div>

[Inline ](http://url.com/ "Inline example")

    [Inline](http://url.com/ "Inline example")

[Reference-style][id] with labels (titles are optional).
[id]: http://example.com/  "Reference-style example"

    [Reference-style][id] with labels (titles are optional).
    [id]: http://example.com/  "Reference-style example"


## <div id="images">Images</div>

Inline (titles are optional):

    ![alt text](/path/img.jpg "Title")

Reference-style:

    ![alt text][id]

    [id]: /url/to/img.jpg "Title"


## <div id="headers">Headers</div>

Setext-style:

    Header 1
    ========
    
    Header 2
    --------

atx-style (closing #'s are optional):

    # Header 1 #

    ## Header 2 ##

    ###### Header 6


## <div id="lists">Lists</div>



Ordered, without paragraphs:

    1.  Foo
    2.  Bar

Unordered, with paragraphs:

    *   A list item.
    
        With multiple paragraphs.

    *   Bar

You can nest them:

    *   Abacus
        * answer
    *   Bubbles
        1.  bunk
        2.  bupkis
            * BELITTLER
        3. burper
    *   Cunning


## <div id="blockquotes">Blockquotes</div>

    > Email-style angle brackets
    > are used for blockquotes.
    
    > > And, they can be nested.

    > #### Headers in blockquotes
    > 
    > * You can quote a list.
    > * Etc.


## <div id="codespans">Code Spans</div>

    `<code>` spans are delimited
    by backticks.

    You can include literal backticks
    like `` `this` ``.


## <div id="codeblocks">Code Blocks</div>

Indent every line of a code block by at least 4 spaces or 1 tab.

    This is a normal paragraph.

        This is a preformatted
        code block.


## <div id="codefences">Code Fences</div>

Use three backticks to fence code blocks for better syntax-highlighting
support, but note that this is a Github *GFM* convention. 

    ```coffeescript
    hi = (name) ->
        print "hello #{name}!"

        hi __filename
    ```


## <div id="rules">Horizontal Rules</div>

Three or more dashes or asterisks:

    ---
    
    * * *
    
    - - - - 


## <div id="linebreaks">Manual Line Breaks</div>

End a line with two or more spaces:

    Roses are red,   
    Violets are blue.

