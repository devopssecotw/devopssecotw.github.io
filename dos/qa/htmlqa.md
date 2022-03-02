# dos
## Servlet
### QA
#### p1
#### p1
- Introduction to HTML:
  HTML stands for HyperText Markup language. It is a standardized system for creating web pages. HTML creates the structure of a web page and uses “tags” to mark up a web page.


Why do we use HTML?

HTML code ensures the proper formatting of text and images so that your Internet browser may display them as they are intended to look. Without HTML, a browser would not know how to display text as elements or load images or other elements. HTML also provides a basic structure of the page, upon which Cascading Style Sheets are overlaid to change its appearance. One could think of HTML as the bones (structure) of a web page, and CSS as its skin (appearance).

The Basic Skeleton of HTML:

<html>
<head>
<title> Interviewbit </title>
</head>
<body>
..........................
....Body contents here....
..........................
</body>
</html>
Concept and Syntax of HTML:

A plaintext document formatted using elements is known as an HTML document. Opening and closing tags are used to surround HTML elements. Angle brackets (<>) are used to start and end each tag. Several tags, such as <image>, <p>, etc. are empty or void and cannot contain any text. You can add attributes to HTML tags to provide them with more information that affects how the browser reads the element:


An HTML element's structure in detail is given in the picture above. An HTML file is saved with the.htm or.html extension, is provided by a web server, and may be viewed in any web browser.

Learn HTML: Basics to Advanced Concepts
1. Root Element in HTML
<html>...</html>: The root (top-level element) of an HTML page is represented by the <html> element or the <html> tag. This element must be the ancestor of all other elements. The structure of any HTML file showing the usage of the <html> element is shown below:
<!DOCTYPE html>
<html lang="en">
 <head>...</head>
 <body>...</body>
</html> 
The structure of an HTML document is shown below:


2. HTML Meta Tag
<head>...</head>: Machine-readable information (metadata) about the document, such as its title, scripts, and style sheets, is contained in the HTML <head> element. The <head> element This is used for setting the title and various other information that is not displayed.
<link>...</link>: The HTML External Resource Link <link> element establishes a connection between the current content and an external resource. This element is most typically used to connect to stylesheets, but it can also be used to create site icons (both "favicon" style icons and icons for the home screen and apps on mobile devices).
<meta>: Metadata that cannot be represented by other HTML meta related elements such as <base>, <link>, <script>, <style>, or <title> is expressed by the HTML <meta> element.
<style>...</style>: The HTML <style> element specifies the style of a document or a section of a document.
<title>...</title>: The HTML Title element <title> specifies the document title that appears in the title bar or tab of a browser. This is what is bookmarked when we bookmark pages.
An example showing the usage of all the above elements is given below:

<!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8">
      <title> HTML Cheatsheet </title>
      <link rel="stylesheet" href="styles.css">
      <style>
        h1 {colour:green;}
        p {colour:yellow;}
      </style>
    </head>
</html> 
3. HTML Elements: Sectioning the Root
<body>...</body>:The content of an HTML document is represented by the HTML <body> element. In a HTML document, there can only be one <body> element. Some of the attributes that can be used along with the <body> element are as follows:
<body bgcolour=?>: This is used for setting the background colour of the body via name or hex value.
<body text=?>: This is used for setting the text colour via name or hex value
<body link=?>: This is used for setting the colour of links via name or hex value
<body vlink=?>: This is used for setting the colour of visited links via name or hex value
<body alink=?>: This is used for setting the colour of active links (during mouse clicking)
An example illustrating the use of the body element is given below:

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title> HTML Cheatsheet </title>
<link rel="stylesheet" href="styles.css">
<style>
  h1 {colour:green;}
  p {colour:yellow;}
</style>
</head>
<body bgcolour="red">
<p>This is a HTML cheatsheet </p>
</body>
</html>
HTML Comments: Although HTML comments are not visible in the browser, they can aid in the documentation of your HTML source code. We can add comments to our HTML code by enclosing them within the symbole: <!-- →. The following syntax shows how to add comments to your HTML source:
<!-- We can write our comments over here -->

4. HTML Elements: Sectioning the Content
<address>...</address>: The HTML address> element denotes that the enclosing HTML contains contact information for a person or group of people, or for a company. An example showing the usage of the address element is given below:
<address>
Written by <a href="mailto:interviewbit@example.com">Kit Harrington</a>.<br> 
Find us at:<br>
interviewbit.com<br>
Mumbai<br>
India
</address>
<article>...</article>: The HTML <article> element denotes a self-contained composition in a document, page, application, or site that is meant to be distributed or reused independently, for instance, in syndication. An example showing the usage of the article element is given below:
<article>
<h2>HTML Cheatsheet</h2>
<p>HTML is an important markup language for web development</p>
</article>
<aside>...</aside>: The HTML <aside> element denotes a section of a page whose content is only tangentially related to the main body of the document. An example showing the usage of the aside element is given below:
<aside>
<h4>What's more on Interviewbit</h4>
<p>Prepare for coding interviews of all companies at interviewbit</p>
</aside>
<header>...</header>: The HTML <header> element denotes introductory content, which is usually a collection of introductory paragraphs or aids to navigation. It may include certain heading elements, as well as a logo, a search form, an image and other elements such as the author's name. An example showing the usage of the header element is given below:
<header>
 <h1>Header over here</h1>
 <p>Content by Scaler</p>
</header>
<footer>...</footer>: The HTML <footer> element is used to create a footer for the sectioning content or sectioning root element that is closest to it. A footer usually includes information about the section's author, copyright information, or links to related papers. An example showing the usage of the footer element is given below:
<footer>
 <p>Author: Jon Snow</p>
 <p><a href="mailto:jonsnow@example.com">jon@example.com</a></p>
</footer>
<main>...</main>: The prominent material of a document's body is represented by the HTML <main> element. The primary content area contains stuff that is either directly related to or extends on the central theme, the theme of a document, or the fundamental functionality of an application. An example showing the usage of the main element is given below:
<main>
<h1>The Heading tag</h1>
</main>
<h1> to <h6>: Six levels of section headers are represented by the HTML <h1> to <h6> elements. The highest level is <h1>. The lowest is <h6> at the section level. An example showing the usage of these elements is given below:
<h1>The Heading tag</h1>
<h2>The Subheading tag</h2>
<nav>...</nav>: The HTML <nav> element denotes a portion of a page that contains navigation links, either within the current document or to other documents. Menus, tables of contents, and indexes are all examples of navigation sections. An example showing the usage of the nav element is given below:
<nav>  
 <a href="/oop/">Learn OOPs</a> |
 <a href="/c++/">Learn C++</a> |
 <a href="/os/">Learn Operating System</a> |
</nav>
<section>...</section>:  The HTML <section> element specifies a standalone section within an HTML document that does not have a more particular semantic element to represent it. An example showing the usage of the section element is given below:
<section>
<h2>More about Interviewbit</h2>
<p>Interviewbit helps students prepare for technical interviews and crack the various interview rounds of companies</p>
</section>
5. HTML Elements: Adding Text Content
<blockquote>...</blockquote>: The HTML<blockquote> Element (or HTML Block Quotation Element) denotes an extended quotation. Indentation is usually used to represent this. The HTML <cite> command can be used to provide a URL for the quotation's source. The <cite> element can be used to provide a text representation of the source, while the cite attribute can be used to provide a text representation of the source. An example that shows the usage of the <blockquote> element is given below:
<blockquote cite="http://www.worldwildlife.org/who/index.html">
For 50 years, WWF has been protecting the future of nature. The world's leading conservation organisation, WWF works in 100 countries and is supported by 1.2 million members in the United States and close to 5 million globally.
</blockquote>
<div>...</div>: The generic container for flow content is the HTML Content Division element (<div>). Unless it is styled with CSS, it has no effect on the content or layout. An example that shows the usage of the <div> element is given below:
<div>
<p> This is a paragraph inside a div element</p>
</div>
<p>...</p>: A paragraph is represented by the HTML <p> element. An example which shows the usage of the <p> element is given below:
<p> This is a paragraph </p>
<pre>...</pre>:  The HTML <pre> element denotes preformatted material that should be displayed precisely as it appears in the HTML source. An example which shows the usage of the <pre> element is given below:
<pre>
This message which is contained in a HTML pre tag
will be shown in a fixed size
font. Also,spaces and
line breaks are preserved as it is.
</pre>
<dd>...</dd>: In a description list (<dl>), the HTML <dd> element offers a description, definition, or value for the previous term (<dt>).An example which shows the usage of the <dd> element is given below:
<dl>...</dl>: A description list is represented by the HTML <dl> element. The element contains a list of term groups (defined by the <dt> element) and descriptions (supplied by the <dd> elements). This element is commonly used to display metadata (a list of key-value pairs) or to construct a glossary.
<dt>...</dt>: The HTML <dt> element is used to specify a term in a description or definition list, and it must be used within a <dl> element.
An example which shows the usage of the <dl>, <dd> and <dt> elements is given below:

<dl>
<dt>Tea</dt>
<dd>Brown Hot drink</dd>
<dt> Milk </dt>
<dd>White cold drink</dd>
</dl>
<hr>...</hr>: A thematic break between paragraph level elements is represented by the HTML <hr> element: for example, a change of scene in a story or a shift in topic within a section.
<ol>...</ol>: An ordered list of items is represented by the HTML <ol> element, which is commonly shown as a numbered list.
<ul>...</ul>: An unordered list of elements, often shown as a bulleted list, is represented by the HTML <ul> element.
<li>...</li>: The <li> element in HTML is used to represent a list item.
An example which shows the usage of the <ol>, <ul>, <li> elements is given below:

<div>
<p>List of fruits</p>
<ol>
 <li>Apple</li>
<li>Orange</li>
<li>Kiwi</li>
</ol>
<p>List of vegetables</p>
<ul>
 <li>Carrots</li>
<li>Broccoli</li>
<li>Spinach</li>
</ol>
</div>
<figure>...</figure>: The HTML <figure> (Figure With Optional Caption) element denotes self contained content with an optional caption given by the (<figcaption>) element.
<figcaption>...</figcaption>: The HTML <figcaption> element, also known as Figure Caption, is a caption or legend that describes the rest of the contents of its parent <figure> element.
An example which shows the usage of the <figure> and <figcaption> elements is given below:

<figure>
<img src="/pictures/lion-1080-720.jpeg"
alt="Lion hunting">
<figcaption>Picture of a lion hunting its prey</figcaption>
</figure>
6. HTML Elements: Adding Image and Multimedia
<img>...</img>: The HTML <img> element is used to include an image in a document. An example that shows the usage of the <img> element is given below:
<img class="fit-picture"
src="/pictures/apple-660-480.jpeg"
alt="This is a picture of an apple">
<audio>...</audio>: Sound content is embedded in documents using the HTML <audio> element. It can have one or more audio sources, which are denoted by the src property or the source> element, with the browser picking the best one. It can also serve as a destination for media that is being streamed using a MediaStream. An example that shows the usage of the <audio> element is given below:
<figure>
<figcaption>Roaring of a lion:</figcaption>
<audio controls src="/audio/demo/lion-roaring.mp3">
 Your browser is not supporting the <code>Audio</code> element.
</audio>
</figure>
<video>...</video>: The HTML Video element (<video>) inserts a media player into the document that allows video playback. Although you can use the <video> element for audio material, the <audio> element may give a better user experience.
<track>...</track>: The HTML <track> element is a child of the <audio> and <video> media components. It allows you to set timed text tracks (or time-based data), for example, to handle subtitles automatically. WebVTT (Web Video Text Tracks or Timed Text Markup Language) is used to format the tracks (.vtt files) (TTML). An example which shows the usage of the <video> and <track> elements is given below:
<video controls width="360"  src="/videos/demos/teachHTML.mp4">
<track default kind="captions"  srclang="en" WebsiteSetup.org - Beginner's HTML Cheat Sheet 11  src="/videos/demos/teachHTML.vtt"/>
 Seems like your browser is not supporting the feature of embedded videos.
</video>
7. HTML Elements: Adding Inline Text Semantics
<a>...</a>: The href property on the HTML <a> element (or anchor element) generates a hyperlink to web pages, files, email addresses, page positions, or anything else a URL can address. An example which shows the usage of the <a> element is given below:
<a href="https://www.facebook.com">Welcome to Facebook</a>
<em>...</em>:  The HTML <em> element denotes text with a strong focus on it. The em> element can be used in a variety of ways, nested, with each level of nesting denoting a higher level of importance. An example that shows the usage of the <em> element is given below:
<p>We <em> need to</em> run faster!</p>
<code>...</code>: The HTML <code> element styles its contents to imply that the text is a small piece of computer code. An example that shows the usage of the <code> element is given below:
<audio controls src="/audio/demo/lion-roaring.mp3">
 Your browser is not supporting the <code>Audio</code> element.
</audio>
<abbr>...</abbr>: An abbreviation or acronym is represented using the HTML Abbreviation element (<abbr>); the optional title property might offer an expansion or description for the abbreviation. An example that shows the usage of the <abbr> element is given below:
<p> The <abbr title="Indian Space Research Organisation">ISRO</abbr> is headquartered in Bengaluru, India.</p>
<br>...</br>: The <br> element in HTML creates a line break in text (carriage-return). It is beneficial when composing a poem or an address where the line division is important. An example that shows the usage of the <br> element is given below:
<p>Hi, Welcome to<br> Interviewbit. We help you master <br>data structure and algorithms</p>
<mark>...</mark>: The HTML Mark Text element (mark>) denotes text that has been marked or highlighted for citation or notation,  due to the marked passage's relevance or importance in the enclosing context. An example that shows the usage of the <mark> element is given below:
<p>Please bring the <mark>Homework Copy</mark> tomorrow.</p>
<span>...</span>: The HTML <span> element is a general inline container for expressing information that does not represent anything by default. It can be used to group items for styling (using the class or id properties) or because they have similar attribute values, such as lang. An example that shows the usage of the <span> element is given below:
<p>My father has a <span style="color:red">red </span> suit.</p>
<cite>...</cite>: The HTML Citation element (<cite>) is used to describe a reference to a referenced creative work, and the title of that work must be included. An example that shows the usage of the <cite> element is given below:
<p><cite>Mona Lisa</cite> Painting by Leonardo da Vinci </p>
<small>...</small>: Independent of its stylistic presentation, the HTML <small> element represents side comments and small print, such as copyright and legal material. It renders text within it one font size smaller by default, such as small to x-small. An example that shows the usage of the <small> element is given below:
<p><small>A very small piece of text.</small></p>
<time>...</time>: The HTML <time> element denotes a specific time period. An example that shows the usage of the <time> element is given below:
<p>The library can be visited from <time>9:00</time> to <time>19:00</time> from monday to friday.</p>
<strong>...</strong>: The HTML Strong Significance Element (<strong>) denotes a high level of importance, seriousness, or urgency in the material. The contents are usually displayed in bold type in browsers. An example that shows the usage of the <strong> element is given below:
<strong>Strong texts in HTML are important content!</strong>
8. HTML Elements: Adding Scripting
<script> … </script>: The HTML <script> element is used to embed or refer to executable code; for example, JavaScript code is generally embedded or referred to using this element. An example which shows the usage of the <script> element is given below:
<!-- HTML4 -->
<script type="text/javascript" src="javascript.js"></script>
<!-- HTML5 -->
<script src="javascript.js"></script>
9. HTML Elements: Interactive Elements
<details>...</details>: The HTML Details Element (<details>) produces a disclosure widget that only shows information when it is toggled to the "open" state.
<summary>...</summary>:  The HTML Disclosure Summary element (<summary>) specifies a summary, caption, or legend for the disclosure box of the details> element.
An example that shows the usage of the <summary> element and the <details> element is given below:

<details>
<summary>Summary of the topic</summary>
Java is an Object Oriented Programming Language.
</details>
10. HTML Elements: Demarcating Edits
<del>...</del>: A region of text that has been deleted from a document is represented by the HTML <del> element.
<ins>...</ins>: A range of text can be added to a document using the HTML <ins> element.
An example which shows the usage of the <del> element and <ins> element is given below:

<!DOCTYPE html>
<html>
<body>
<h1>Demo of the del element and ins element</h1>
<p>Her favourite colour is <del> green</del> <ins> magenta</ins>!</p>
</body>
</html>
11. HTML Elements: Tables
<table>...</table>: The HTML <table> element is used to display tabular data, which is information presented in a two dimensional table with rows and columns of data filled cells.
<caption>...</caption>: The HTML Table Caption element (<caption>) specifies a table's caption (or title), and is always the first child of a <table> if it is utilised.
<thead>...</thead>: The HTML <thead> element creates a series of rows that constitute the table's column heads.
<tbody>...</tbody>: The HTML Table Body element (<tbody>) incorporates a collection of table rows (<tr> elements) that make up the table's body (<table>).
<td>...</td>: The HTML <td> element designates a data-filled table cell. It is a part of the table model.
<tr>...</tr>: A row of cells in a table is defined using the HTML <tr> element. Cells for the row can then be created using a combination of <td> (data cell) and <th> (header cell) components.
<th>...</th>: A cell is designated as the header of a set of table cells by the HTML <th> element. The scope and header attribute specify the exact nature of this group.
<tfoot>...</tfoot>: The HTML <tfoot> element defines a series of rows that summarise the table's columns.
An example that shows the usage of a table in HTML is given below:

<table>
<caption>Details about Tables in HTML</caption>
<thead>
<tr>
 <th rowspan="5">HTML table's header</th>
</tr>
</thead>
<tbody>
<tr>
 <td>Body of the table</td>
 <td>Table has 5 rows</td>
</tr>
</tbody>
<tfoot>
<tr>
 <td>Footer of the table </td>
</tr>
</tfoot>
</table>
12. HTML Elements: Forms
<form>...</form>: A document section with interactive controls for submitting information to a web server is represented by the HTML <form> element. An example which shows the usage of the <form> element is given below:
<form action="" method="get" class="demoForm">
<div class="demoForm">
<label for="name">Please input your name: </label>
<input type="text" name="name" id="name" required>
</div>
<div class="demoForm">
<label for="email">Please input your email id: </label>
<input type="email" name="email" id="email" required>
</div>
<div class="demoForm">
 <input type="submit" value="Submit!">
</div>
</form>
<button>...</button>: The HTML <button> element specifies a clickable button that can be used in forms or anywhere else in a document where a conventional button is required. An example which shows the usage of the <button> element is given below:
<!DOCTYPE html>
<html>
<body>
<p>Example of a button</p>
<button type="button" onclick="alert(This is a button click!')">Click Me!</button>
</body>
</html>
<datalist>...</datalist>: The HTML <datalist> element includes a series of <option> components that indicate the values that can be used for other controls.
<!DOCTYPE html>
<html>
<body>
<p>Demo of the datalist tag in HTML</p>
<form action="" method="get">
 <label for="browser">Choose your favourite fruit from the list given below:</label>
 <input list="fruits" name="fruit" id="fruit">
 <datalist id="browsers">
   <option value="Apple">
   <option value="Orange">
   <option value="Kiwi">
   <option value="Pomegranate">
   <option value="Dragon Fruit">
 </datalist>
 <input type="submit">
</form>
</body>
</html>
<input>: The HTML <input> element is used to create interactive controls for web based forms in order to accept data from the user; depending on the device and user, a range of sorts of input data and control widgets are accessible. Examples of the usage of the input element have been given above.
<progress>...</progress>: The HTML <progress> element shows a progress indicator for an activity, which is commonly shown as a progress bar. An example which shows the usage of the <progress> element is given below:
<!DOCTYPE html>
<html>
<body>
<p>Demo of the progress tag</p>
<label for="fileDownload">Progress of the download:</label>
<progress id="fileDownload" value="64" max="80"> 64% </progress>
</body>
</html>
<select>...</select>: The HTML <select> element denotes a control with a menu of options.
<optgroup>...</optgroup>: Within a <select> element, the HTML optgroup> element generates a grouping of alternatives.
<option>...</option>: An item contained in a <select>, an <optgroup>, or an <datalist> is defined by the HTML <option> element. As a result, option> can be used to represent popup menu items and other lists of things in an HTML text. An example which shows the usage of the <select>, <optgroup>, <option> elements is given below:
<label for="cuisine">Select your favourite cuisine:</label>
<select  name="cuisine" id="cuisine">
 <optgroup label="Indian Cuisine">
   <option value="chola-bhature">Chola Bhature</option>
   <option value="dahi-vada">Dahi Vada</option>
 </optgroup>
 <optgroup label="Italian Cuisine">
   <option value="pizza">Pizza</option>
   <option value="pasta">Pasta</option>
 </optgroup>
</select>
<label>...</label>: A caption for an item in a user interface is represented by the HTML <label> element. Examples of the usage of a label element have been given above.
<legend>...</legend>: The caption for the content of its parent <fieldset> is represented by the HTML <legend> element.
<fieldset>...</fieldset>: Within a web form, the HTML <fieldset> element is used to organise many controls as well as labels (<label>). An example which shows the usage of the <legend> and <fieldset> elements is given below:
<!DOCTYPE html>
<html>
<body>
<p>Demo of the legend and fieldset elements</p>
<form action="">
<fieldset>
 <legend>Personal Information:</legend>
 <label for="firstname">First name:</label>
 <input type="text" id="firstname" name="firstname">
 <label for="lastname">Last name:</label>
 <input type="text" id="lastname" name="lastname">
 <label for="emailId">Email Id:</label>
 <input type="emailId" id="emailId" name="emailId">
 <label for="birthday">Date of birth:</label>
 <input type="date" id="birthday" name="birthday"><br><br>
 <input type="submit" value="Submit">
</fieldset>
</form>
</body>
</html>
<textarea>...</textarea>: When you wish to allow users to submit a large quantity of free-form text, such as a comment on a review or feedback form, the HTML <textarea> element indicates a multi-line plain-text editing control. An example which shows the usage of the <textarea> element is given below:
<textarea id="interviewbitReview" name="interviewbitReview" rows="2" cols="33">
At interviewbit.com we can learn how to prepare for coding interviews as it offers free tutorials in all Computer Science subjects.
</textarea>






### references
#### links
- <https://www.interviewbit.com/html-cheat-sheet/>