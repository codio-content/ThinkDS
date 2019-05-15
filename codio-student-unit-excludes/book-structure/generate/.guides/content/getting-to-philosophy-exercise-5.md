In `WikiPhilosophy.java` you'll find a simple `main` method that shows how to use some of these pieces. Starting with this code, your job is to write a crawler that:



1. 
Takes a URL for a Wikipedia page, downloads it, and parses it.

1. 
It should traverse the resulting DOM tree to find the first
*valid* link. I'll explain what “valid” means below.

1. 
If the page has no links, or if the first link is a page we have
already seen, the program should indicate failure and exit.

1. 
If the link matches the URL of the Wikipedia page on philosophy, the
program should indicate success and exit.

1. 
Otherwise it should go back to Step 1.


The program should build a `List` of the URLs it visits and display the results at the end (whether it succeeds or fails).


So what should we consider a “valid” link? You have some choices here. Various versions of the “Getting to Philosophy” conjecture use slightly different rules, but here are some options:



1. 
The link should be in the content text of the page, not in a sidebar
or boxout.

1. 
It should not be in italics or in parentheses.

1. 
You should skip external links, links to the current page, and red
links.

1. 
In some versions, you should skip a link if the text starts with an
uppercase letter.


You don't have to enforce all of these rules, but we recommend that you at least handle parentheses, italics, and links to the current page.

If you feel like you have enough information to get started, go ahead. Or you might want to read these hints:



1. 
As you traverse the tree, the two kinds of `Node` you will need
to deal with are `TextNode` and `Element`. If you find
an `Element`, you will probably have to typecast it to access
the tag and other information.

1. 
When you find an `Element` that contains a link, you can check
whether it is in italics by following parent links up the tree. If
there is an `<i>` or `<em>` tag in the parent chain, the
link is in italics.

1. 
To check whether a link is in parentheses, you will have to scan
through the text as you traverse the tree and keep track of opening
and closing parentheses (ideally your solution should be able to
handle nested parentheses (like this)).

1. 
If you start from the Java page, you should get to Philosophy
after following
seven links, unless something has changed since I ran the code.


OK, that's all the help you're going to get. Now it's up to you. Have fun!