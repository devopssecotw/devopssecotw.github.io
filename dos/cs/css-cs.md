# dos
## CSS 
### Cheat Sheet
#### basics
- Syntax
```css
selector{
property: value;
}
```
- Include external css file
```css
<link rel="stylesheet" type="text/css" href="/style.css" />
```
- Internal styles
```css
<style type="text/css">
div { color: #888;}
</style>
```
- Inline styles
```css
<div style="property: value"> </div>
```
- Box model
```css
margin
border
padding
content 
```

#### Selectors
```css
ID Selector
#id {}

Class Selector
.class {}

Type Selector
h1, h2 ,h3 {}

Child Selector
ul > li {}

Attribute Selector
div[attribute="SomeValue"] {}

*all elements
divall div tags
div,pall divs and paragraphs
div pparagraphs inside divs
div > pall p tags, one level deep in div
div + pp tags immediately after div
div ~ pp tags preceded by div
.classnameall elements with class
#idnameelement with ID
div.classnamedivs with certain classname
div#idnamediv with certain ID
#idname *all elements inside #idname


```
#### Pseudo Selectors & Elements
```css
Checked elements selector
input:checked {}

Pseudo classes
a:linklink in normal state
a:activelink in clicked state
a:hoverlink with mouse over it
a:visitedvisited link
p::after{content:"yo";}add content after p
p::beforeadd content before p
input:checkedchecked inputs
input:disableddisabled inputs
input:enabledenabled inputs
input:focusinput has focus
input:in-rangevalue in range
input:out-of-rangeinput value out of range
input:validinput with valid value
input:invalidinput with invalid value
input:optionalno required attribute
input:requiredinput with requred attribute
input:read-onlywith readonly attribute
input:read-writeno readonly attrib.
div:emptyelement with no children
p::first-letterfirst letter in p
p::first-linefirst line in p
p:first-of-typefirst of some type
p:last-of-typelast of some type
p:lang(en)p with en language attribute
:not(span)element that's not a span
p:first-childfirst child of its parent
p:last-childlast child of its parent
p:nth-child(2)second child of its parent
p:nth-child(3n+1)nth-child (an + b) formula
p:nth-last-child(2)second child from behind
p:nth-of-type(2)second p of its parent
p:nth-last-of-type(2)...from behind
p:only-of-typeunique of its parent
p:only-childonly child of its parent
:rootdocuments root element
::selectionportion selected by user
:targethighlight active anchor


Attribute selectors
a[target]links with a target attribute
a[target="_blank"]links which open in new tab
[title~="chair"]title element containing a word
[class^="chair"]class starts with chair
[class|="chair"]class starts with the chair word
[class*="chair"]class contains chair
[class$="chair"]class ends with chair
input[type="button"]specified input type
```
#### Box Properties
```css
Box Sizing
box-sizing: border-box | content-box

Margin
margin: 2px 4px 6px 8px | 0 auto

Border Style
border-style: none | hidden | dotted | dashed | solid | double | groove | ridge | inset | outset

Border Width
border-width: 10px

Border Color
border-color: #2AA9E0

Padding
padding: 2px 4px 6px 8px
```
#### Text Styling
```css
Font style
font-style: normal | italic | oblique

Font Variant
font-variant: normal | small-caps

Font Weight
font-weight: normal | bold | bolder | lighter | 100 - 900

Vertical Alignment
vertical-align: baseline | 10px | sub | super | top | text-top | middle | bottom | text-bottom | initial

Text Transform
text-transform: capitalise | lowercase | uppercase

Font Size
font-size: 12px | 0.8em | 80%

Space Between Characters
letter-spacing: normal | 4px

Line Height
line-height: normal | 3em | 34%

Horizontal Alignment
text-align: left | right | center | justify

Text Align Last
text-align-last: auto | left | right | center | justify | start | end | initial | inherit

Text Decoration
text-decoration: none | underline | overline | line-through

Indent First Line
text-indent: 25px

Font Family
font-family: 'Open Sans', sans-serif

Text Justify
text-justify: auto | inter-word | inter-character | none | initial | inherit

Text Overflow
text-overflow: clip | ellipsis | string | initial | inherit

Text Shadow
text-shadow: h-shadow v-shadow blur-radius color | none | initial | inherit
```
#### Background
```css
Background Image
background-image: url()

Background Repeat
background-repeat: repeat-x | repeat-y | repeat | space | round | no-repeat

Background Attachment
background-attachment: scroll | fixed | local | initial | inherit

Background Color
background-color: #2AA9E0

Background Position
background-position: top | right | bottom | left | center | initial | inherit
```
#### Position
```css
Position
position: static | relative | absolute | fixed | sticky

Position Properties
top | right | bottom | left

Float Element
float: left | right | none

Clear Floating Elements
clear: none | left | right | both

Z Index
z-index: 3 | auto | inherit
```
#### Colors
```css
Colors 
color
inherit
color
opacity
inherit
number 
```
#### Backgrounds
```css

```
#### Selectors
#### Properties
```css
align-contentbehavior of the flex-wrap property
align-itemsalignment for items inside the container
align-selfalignment for the selected item
allchanges all properties
animationbinds an animation to an element
animation-delaydelays animation start
animation-directionreverse animation or in alternate cycles
animation-durationanimation duration in seconds or ms
animation-fill-modestyle when the animation is not playing
animation-iteration-countnumber of an animation replays
animation-namename for the @keyframes animation
animation-play-statethe animation is running or paused
animation-timing-functionspeed curve of an animation
backface-visibilityis element visible when not facing the screen
backgroundall background properties in one declaration
background-attachmentis the background image fixed or scrolls
background-blend-modeblending mode of each background layer
background-clippainting area of the background
background-colorbackground color
background-imagebackground image
background-originwhere the background image is positioned
background-positionstarting position of the background image
background-repeatthe way the background image is repeated
background-sizebackground image size
bordersets all border properties in one line
border-bottombottom border properties in one line
border-bottom-colorcolor of the bottom border
border-bottom-left-radiusborder bottom left radius
border-bottom-right-radiusborder bottom right radius
border-bottom-styleborder bottom style
border-bottom-widthborder bottom width
border-collapseborder collapse
border-colorborder color
border-imagesets an image as border
border-image-outsetborder image area extends beyond the border box
border-image-repeatborder image repeated, rounded or stretched
border-image-slicehow to slice the border image
border-image-sourcepath to the border image
border-image-widthborder image width
border-leftleft border properties in one line
border-left-colorborder left color
border-left-styleborder left style
border-left-widthborder left width
border-radiusborder radius of the four rounded corners
border-rightright border properties in one line
border-right-colorborder right color
border-right-styleborder right style
border-right-widthborder right width
border-spacingborder spacing
border-styleborder style
border-toptop border properties in one line
border-top-colorborder top color
border-top-left-radiusborder top left radius
border-top-right-radiusborder top right radius
border-top-styleborder top style
border-top-widthborder top width
border-widthborder width
bottombottom offset for relative and absolute elements
box-shadowshadow to element
box-sizingbox sizing properties
caption-sideplacement of a table caption
cleardeny floating of an element
clipclip an absolutely positioned element
colortext color
column-countdivide the content in columns
column-fillbalanced fill or not
column-gapgap between the columns
column-ruleseparator between columns, like border
column-rule-colorcolumn rule color
column-rule-stylecolumn rule style
column-rule-widthcolumn rule width
column-spancolumn span
column-widthcolumn width
columnsset column-width and column-count
contentinsert content :before and :after elements
counter-incrementcount sections
counter-resetreset counter
cursorcursor type when element is hovered
directionwriting direction, Arabic is using rtl
displaybox display type
empty-cellshide borders and background on empty table cells
filterimage effects: grayscale, blur, invert etc.
flexitem length, relative to others inside the container
flex-basisinitial length of a flexible item
flex-directiondirection of the flexible items
flex-flowshorthand for flex-direction and flex-wrap
flex-growhow much the item will grow relative other items
flex-shrinkhow to shrink the item relative to other items
flex-wrapwrap flexible items
floatfloat elements left or right
fontall font properties in one line
@font-facedeclare non-web-safe fonts
font-familyfont of the element
font-sizefont size
font-size-adjustcontrol font size if the first declared option is not available
font-stretchwiden or narrow text
font-stylefont style: normal, italic, oblique
font-variantset small-caps
font-weightuse bold or thin characters
hanging-punctuationcan a punctuation mark be placed outside the line box?
heightheight of the element
justify-contentjustifies flexible container's items horizontally if necessary
@keyframesspecifies the animation code
leftleft offset for relative and absolute elements
letter-spacingspace between characters
line-heightline height of text or inline-block elements
list-styleall list properties in one line
list-style-imagereplace the list item marker with an image
list-style-positionlist item markers inside or outside the content flow
list-style-typeset the type of the list item marker
marginset the top, right, bottom and left margins in one line
margin-bottombottom margin
margin-leftleft margin
margin-rightright margin
margin-topmargin top
max-heightmaximum height of element
max-widthmaximum width of element
@mediasee media queries
min-heightminimum height
min-widthminimum width
nav-downwhere to navigate when the the arrow-down button is pressed
nav-indexsets sequential navigation order
nav-leftwhere to navigate when the the arrow-left button is pressed
nav-rightwhere to navigate when the the arrow-right button is pressed
nav-upwhere to navigate when the the arrow-up button is pressed
opacitytransparency level of an element
orderreorder elements in a container
outlinedrow an outer border around elements
outline-coloroutline color
outline-offsetgap between the element and the outline
outline-styleoutline style
outline-widthoutline width
overflowhide, display or scroll if the content overflows its container
overflow-xhorizontal overflow
overflow-yvertical overflow
paddingpadding between the element border and content
padding-bottompadding bottom
padding-leftpadding left
padding-rightpadding right
padding-toppadding top
page-break-afteradds page break after an element
page-break-beforeadds page break before an element
page-break-insideallow page break inside an element
perspectivehow many pixels the 3D element is placed from the view
perspective-originwhere is the 3D element based in the x- and y-axis
positionpositioning type: absolute, fixed, relative, static
quotesset quotation marks to wrap an element
resizedeclare resizable elements
rightright offset for relative and absolute elements
tab-sizetab character space length
table-layouttable layout algorithm
text-alignhorizontal alignment of text
text-align-lasthorizontal alignment of last line of text
text-decorationoverline, underline or line-through the text
text-indentindentation of the first line of the text
text-overflowthe way how overflowed content is marked (ellipsis)
text-shadowtext shadow
text-transformcapitalization of text
toptop offset for relative and absolute elements
transform2D 3D transformation. See widget.
transform-originchanges the position of transformed elements
transform-stylerender nested elements in 3D
transitiontransition properties in one line
transition-delaydelay before transition effect start
transition-durationtransition effect duration
transition-propertywhich CSS property is the transition affecting
transition-timing-functionspeed curve of the transition
unicode-bidishould the text be overridden to support more languages
user-selectdisable user content selection
vertical-alignvertical alignment
visibilityvisibility:hidden elements leave a gap
white-spacehow are white-spaces handled
widthwidth of an element
word-breaktext breaking rules when text reaches the end of the container
word-spacingsize of white space between words
word-wrapbreak long words and wrap onto the next line
z-indexstack order of the element
```


###
```css
Backgrounds 
background
background-image
background-position
background-size
background-repeat
background-attachment
background-origin
background-clip
background-color
background-image
url
gradients
none
background-position
top left | top center | top right | center left | center center |
center right | bottom left | bottom center | bottom right
x-% y-%
x-pos y-pos
background-size
length
%
auto | cover | contain
background-repeat
repeat | repeat-x | repeat-y |
no-repeat 

background-attachment
scroll | fixed | local
background-origin
border-box | padding-box | content-box
background-clip
border-box | padding-box | content-box
background-color
color
transparent
Border 
border
border-width
border-style
border-color
border-width
thin | medium | thick | length
border-style
none | hidden | dotted |
dashed | solid | double |
groove | ridge | inset | outset
border-color
color
border-bottom
border-bottom-width
border-style
border-color
border-left
border-left-width

border-style
border-color
border-left-style
border-style
border-right-color
border-color
border-right-width
thin | medium | thick | length
border-top-width
thin | medium | thick | length
border-break
border-width
border-style
color
close
border-bottom-color
border-color
border-bottom-style
border-style
border-left-color
border-color
border-left-width
thin | medium | thick length
border-right-style
border-style
border-top
border-top-width
border-style
border-color 

border-top-color
border-color
border-top-style
border-style
box-shadow
inset || [ length, length, length, length || <color> ]
none
border-collapse
collapse | separate
border-image
image
[ number / % border-width stretch | repeat | round ]
none
border-right
border-right-width
border-style
border-color
border-radius
border-radius
border-top-right-radius
border-bottom-right-radius
border-bottom-left-radius
border-top-left-radius
border-top-right-radius
length
border-bottom-right-radius
length
border-bottom-left-radius
length 

Box Model 
float
left | right | none
height
auto
length
%
max-height
none
length
%
max-width
none
length%
min-height
none
length
%
width
auto
%
length
margin
margin-top
margin-right
margin-bottom
margin-left
margin-bottom

auto
length
%
margin-left
auto
height
%
margin-right
auto
height
%
margin-top
auto
length
%
padding
padding-top
padding-right
padding-bottom
padding-left
padding-bottom
length
%
padding-left
length
%
padding-right
length
% 

padding-top
length
%
display
none | inline | block | inline-block | flex | inline-flex | grid |
inline-grid | contents | list-item |run-in | compact | table |
inline-table | table-row-group | table-header-group |
table-footer-group | table-row | table-column-group | table-column |
table-cell | table-caption | ruby | ruby-base | ruby-text |
ruby-base-group | ruby-text-group
overflow
visible | hidden | scroll |
auto | no-display | no-content
overflow-x
overflow-y
overflow-style
auto | marquee-line | marqueeblock
overflow-x
visible | hidden | scroll |
auto | no-display | no-content
visibility
visible | hidden | collapse
clear
left | right | both | none
Font 
font
font-style
font-variant
font-weight
font-size/line-height 

font-family
caption | icon | menu | messagebox | small-caption | status-bar
font-size-adjust
none | inherit
number
font-family
serif | sans-serif | Font Name
font-style
normal | italic | oblique | inherit
font-variant
normal | small-caps | inherit
font-size
xx-small | x-small | small | medium | large | x-large | xxlarge |
smaller | larger |
inherit
length
%
font-weight
normal | bold | bolder | lighter | 100 | 200 | 300 | 400 | 500 | 600 |
700 | 800 | 900 | inherit
Text 
direction
ltr | rtl | inherit
hanging-punctuation
none | [ start | end | endedge ]
letter-spacing
normal
length
% 
text-outline
none
color
length
unicode-bidi
normal | embed | bidi-override
white-space
normal | pre | nowrap | pre-wrap | pre-line
white-space-collapse
perserve | collapse | pre-servebreaks | discard
punctuation-trim
none | [ start | end | adjacent ]
text-align
start | end | left | right | center | justify
text-align-last
start | end | left | right | center | justify
text-decoration
none | underline | overline | line-thorugh | blink
text-shadow
none
color
length
word-break
normal | keep-all | loose | break-strict | break-all
word-wrap
normal
nowrap
text-emphasis
none | [ [ accent | dot | circle | disc | [ before | after ]?] 

text-indent
length
%
text-justify
auto | inter-word | interideograph | inter-cluster | distribute |
kashida | tibetan
text-transform
none | capitalize | uppercase | lowercase
text-wrap
normal | unresrricted | none | suppress
word-spacing
normal
length
% 

Table 
border-collapse
collapse | separate
empty-cells
show | hide
border-spacing
length length
table-layout 
auto | fixed
caption-side
top | bottom | left | right




```



### references
#### links
- <https://developer.mozilla.org/en-US/docs/Web/CSS>
- <https://htmlcheatsheet.com/css/>
- <https://websitesetup.org/wp-content/uploads/2019/11/wsu-css-cheat-sheet-gdocs.pdf>
- <https://web.stanford.edu/group/csp/cs21/csscheatsheet.pdf>
- <https://adam-marsden.co.uk/css-cheat-sheet>
- 
