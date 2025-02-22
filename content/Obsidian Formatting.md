---
aliases:
  - Obsidian Styling
cssclasses:
  - embed-strict
date: 2022-12-12
dateModified: 2023-09-06
image: 
share: true
stage: 
title: Obsidian Formatting
tags:
  - someday
---

Obsidian should support the formats below:

---

### Callouts

Use the following syntax to denote a callout block: `> [!INFO]`.

```markdown
> [!INFO]
> Here's a callout block.
> It supports **markdown** and [[Obsidian Formatting|wikilinks]].
```

> [!INFO]
> Here's a callout block.
> It supports **markdown** and [[Obsidian Formatting|wikilinks]].
> 

> [!note]-  [!note]
> minimized by default

> [!abstract]+  [!abstract]  [!summary]  [!tldr]
> open by default

> [!todo]  [!todo]

> [!tip]  [!tip]  [!hint]  [!important]

> [!success]  [!success]  [!check]  [!done]  

> [!question]  [!question]  [!help]  [!faq]  

> [!warning]  [!warning]  [!caution]  [!attention]  

> [!failure]  [!failure]  [!fail]  [!missing]

> [!danger]  [!danger]  [!error]

> [!bug]  [!bug]

> [!example]  [!example]

> [!quote]  [!quote]  [!cite]

---

### Internal Linking

```md
Link to a page: [[Internal link]].
```

Link to a page: [[Obsidian Formatting|wikilinks]].

---

### Embeds

Embed another file section:

```md
![[Obsidian Formatting#Internal Linking]]
```



---

### Headers

```md
# This is a heading 1
## This is a heading 2
### This is a heading 3 
#### This is a heading 4
##### This is a heading 5
###### This is a heading 6
```

%% These headings use HTML to avoid cluttering the Outline/Table of contents %%
<h1>This is a heading 1</h1>
<h2>This is a heading 2</h2>
<h3>This is a heading 3</h3> 
<h4>This is a heading 4</h4>
<h5>This is a heading 5</h5>
<h6>This is a heading 6</h6>

---

You can also use the alternative syntax for Heading 1 and Heading 2.

```md
Heading 1
===

Heading 2
---
```

<h1>Heading 1</h1>

<h2>Heading 2</h2>

---

### Emphasis

```md
*This text will be italic*

_This will also be italic_
```

_This text will be italic_

_This will also be italic_

```md
**This text will be bold**

__This will also be bold__
```

**This text will be bold**

**This will also be bold**

```md
_You **can** combine them_
```

_You **can** combine them_

---

### Lists

#### Unnumbered Lists

test

```md
- Item 1
- Item 2
  - Item 2a
  - Item 2b
```

- Item 1
- Item 2
  - Item 2a
  - Item 2b

#### Numbered Lists

```md
1. Item 1
1. Item 2
1. Item 3
   1. Item 3a
   1. Item 3b
```

1. Item 1
1. Item 2
1. Item 3
	1. Item 3a
	1. Item 3b

---

Create a _loose list_ by adding a blank line between any two list items.

```md
- Item 1

- Item 2
- Item 3
```

Will look like this:
- Item 1

- Item 2
- Item 3

---

### Images

```md
![Engelbart](https://history-computer.com/ModernComputer/Basis/images/Engelbart.jpg)
```

![Engelbart](https://history-computer.com/ModernComputer/Basis/images/Engelbart.jpg)

```md
![[og-image.png]]
```

![[og-image.png|og-image.png]]

#### Resizing Images

Example of this above image resized to 100 pixels wide:

```md
![Engelbart|100](https://history-computer.com/ModernComputer/Basis/images/Engelbart.jpg)
```

![Engelbart|100](https://history-computer.com/ModernComputer/Basis/images/Engelbart.jpg)

or for local images

```md
![[og-image.png|200]]
```

![[og-image.png|200]]

---

### Links

#### External Links

Markdown style links can be used to refer to either external objects, such as web pages, or an internal page or image.

```md
http://obsidian.md - automatic!
[Obsidian](http://obsidian.md)
```

#### Obsidian URI Links

[[Using obsidian URI|Obsidian URI]] links can be used to open notes in Obsidian either from another Obsidian vault or another program.

For example, you can link to a file in a vault like so (please note the [[Using obsidian URI#Encoding|required encoding]]):

```md
[Link to note](obsidian://open?path=D:%2Fpath%2Fto%2Ffile.md)
```

[Link to note](obsidian://open?path=D:%2Fpath%2Fto%2Ffile.md)

You can link to a note by its vault name and file name instead of path as well:

```md
[Link to note](obsidian://open?vault=MainVault&file=MyNote.md)
```

[Link to note](obsidian://open?vault=MainVault&file=MyNote.md)

#### Escaping

If the URL contains spaces, you can escape them by replacing them with `%20`.

```md
[Export options](Pasted%20image)
```

[Export options](Pasted%20image)

Or you can enclose the target in `<>`, such as:

```md
[Slides Demo](<Slides Demo>)
```

[Slides Demo](<Slides Demo>)

---

### Blockquotes

```md
> Human beings face ever more complex and urgent problems, and their effectiveness in dealing with these problems is a matter that is critical to the stability and continued progress of society.

\- Doug Engelbart, 1961
```

> Human beings face ever more complex and urgent problems, and their effectiveness in dealing with these problems is a matter that is critical to the stability and continued progress of society.

\- Doug Engelbart, 1961

---

### Code

#### Inline Code

```md
Text inside `backticks` on a line will be formatted like code.
```

Text inside `backticks` on a line will be formatted like code. 

#### Code Blocks

You can add syntax highlighting to a code block by adding a language code after the first set of backticks.

Obsidian uses Prism for syntax highlighting. For more information, refer to [Supported languages](https://prismjs.com/#supported-languages).

> [!note]
> [[Live preview update|Live Preview mode]] doesn't support PrismJS and may render syntax highlighting differently.

~~~md
```js
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
```
~~~

```js
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
```

---

```md
    Text indented with a tab is formatted like this, and will also look like a code block in preview. 
```

    Text indented with a tab is formatted like this, and will also look like a code block in preview. 

---

### Task List

Syntax	Description
- [ ] to-do ` `
- [/] incomplete `/`
- [x] done `x`
- [-] canceled `-`
- [>] forwarded `>`
- [<] scheduling `<`
- [?] question `?`
- [!] important `!`
- [*] star `*`
- ["] quote `"`
- [l] location `l`
- [b] bookmark `b`
- [i] information `i`
- [S] savings `s`
- [I]  idea `i`
- [p] pros `p`
- [c] cons `c`
- [f] fire `f`
- [k] key `k`
- [w] win `w`
- [u] up `u`
- [d] down `d`

---

### Tables

You can create tables by assembling a list of words and dividing the header from the content with hyphens, `-`, and then separating each column with a pipe `|`:

```md
|First Header | Second Header|
|------------ | ------------|
|Content from cell 1 | Content from cell 2|
|Content in the first column | Content in the second column|
```

|First Header | Second Header|
|------------ | ------------|
|Content from cell 1 | Content from cell 2|
|Content in the first column | Content in the second column|

The vertical bars at the start and end of a line are optional.

```md
First Header | Second Header
------------ | ------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column
```

This results in the same table as the one above.

---

```md
Tables can be justified with a colon | Another example with a long title | And another long title as a example
:----------------|-------------:|:-------------:
because of the `:` | these will be justified |this is centered
```

Tables can be justified with a colon | Another example with a long title | And another long title as a example
:----------------|-------------:|:-------------:
because of the `:` | these will be justified |this is centered

If you put links in tables, they will work, but if you use [[Add aliases to note|aliases]], the pipe must be escaped with a `\` to prevent it being read as a table element.

```md
First Header | Second Header
------------ | ------------
[[Format your notes\|Formatting]]	|  [[Keyboard shortcuts\|hotkeys]]
```

First Header | Second Header
------------ | ------------
[[Format your notes\|Formatting]]	|  [[Use hotkeys\|hotkeys]]	

---

### Strikethrough

```md
Any word wrapped with two tildes (like ~~this~~) will appear crossed out.
```

Any word wrapped with two tildes (like ~~this~~) will appear crossed out.

---

### Highlighting

```md
Use two equal signs to ==highlight text==.
```

Use two equal signs to ==highlight text==.

---

### Horizontal Bar

Use three stars ***, hyphens ---, or underscores ___ in a new line to produce an horizontal bar.

***

---

### Footnotes

```md
Here's a simple footnote,[^1] and here's a longer one.[^bignote]

[^1]: meaningful!

[^bignote]: Here's one with multiple paragraphs and code.

    Indent paragraphs to include them in the footnote.

    `{ my code }`

    Add as many paragraphs as you like.
```

Here's a simple footnote,[^1] and here's a longer one.[^bignote]

[^1]: meaningful!

[^bignote]: Here's one with multiple paragraphs and code.

	Indent paragraphs to include them in the footnote.

	`{ my code }`

	Add as many paragraphs as you like.

---

```md
You can also use inline footnotes. ^[notice that the caret goes outside of the brackets on this one.]
```

You can also use inline footnotes. ^[notice that the caret goes outside of the brackets on this one.]

---

### Math

```md
$$\begin{vmatrix}a & b\\
c & d
\end{vmatrix}=ad-bc$$
```

$$\begin{vmatrix}a & b\\
c & d
\end{vmatrix}=ad-bc$$

---

```md
You can also do inline math like $e^{2i\pi} = 1$ .
```

You can also do inline math like $e^{2i\pi} = 1$ .

To render math from [[LaTeX|LaTeX]] notation Obsidian uses [MathJax](http://docs.mathjax.org/en/latest/basic/mathjax.html).
For more information about the syntax, refer to [MathJax basic tutorial and quick reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference).

For a list of supported MathJax packages, refer to [The TeX/LaTeX Extension List](http://docs.mathjax.org/en/latest/input/tex/extensions/index.html).

---

### Comments

Use `%%` to enclose comments, which will be parsed as Markdown, but will not show up in the preview.

```md
Here is some inline comments: %%You can't see this text%% (Can't see it in Reading mode)

Here is a block comment: (can't see it in Reading mode either)
%%
It can span
multiple lines
%%
```

Here is some inline comments: %%You can't see this text%% (can't see it in Reading mode)

Here is a block comment: (can't see it in Reading mode either)
%%
It can span
multiple lines
%%

---

### Diagram

Obsidian uses [Mermaid](https://mermaid-js.github.io/) to render diagrams and charts. Mermaid also provides [a helpful live editor](https://mermaid-js.github.io/mermaid-live-editor).
Mermaid provides the following diagram types:
- Flowchart
- Sequence diagram
- Class Diagram
- State Diagram
- Entity Relationship Diagram
- User Journey
- Gantt
- Pie Chart
- Requirement Diagram

````md
```mermaid
sequenceDiagram
    Alice->>+John: Hello John, how are you?
    Alice->>+John: John, can you hear me?
    John-->>-Alice: Hi Alice, I can hear you!
    John-->>-Alice: I feel great!
```
````

```mermaid
sequenceDiagram
    Alice->>+John: Hello John, how are you?
    Alice->>+John: John, can you hear me?
    John-->>-Alice: Hi Alice, I can hear you!
    John-->>-Alice: I feel great!
```

````md
```mermaid
graph TD

Biology --> Chemistry
```
````

```mermaid
graph TD

Biology --> Chemistry
```


Obsidian supports linking to notes in Mermaid,
these links will not show up on [[Graph view]].
````md
```mermaid
graph TD

Biology --> Chemistry

class Biology,Chemistry internal-link;
```
````

```mermaid
graph TD

Biology --> Chemistry

class Biology,Chemistry internal-link;
```

An easier way to do it is the following: ^376b9d
````md
```mermaid
graph TD

A[Biology]
B[Chemistry]

A --> B

class A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z internal-link;
```
````

This way, all the note names (at least until `Z[note name]`) are all automatically assigned the class `internal-link` when you use this snippet.

If you use special characters in your note names, you need to put the note name in double quotes.
`"⨳ special character"`
It looks like this if you follow the [[Format your notes#^376b9d|second option]]:
`A["⨳ special character"]`

---

## Developer Notes

We strive for maximum capability without breaking any existing formats, therefore we use a slightly unorthodox combination of flavors of markdown. It is broadly CommonMark, with the addition of some functionality from GitHub Flavored Markdown (GFM), some LaTeX support, and our chosen embed syntax, which you can read more about at [[Accepted file formats]].

We intentionally do not support parsing markdown syntax and blank lines within HTML blocks. This is the result of an optimization to handle very large files and to support synchronization between editing and reading mode.


---

## Icons

- Obsidian
			- [GitHub - aidenlx/obsidian-icon-shortcodes: Obsidian Plugin: Insert emoji and custom icons with shortcodes](https://github.com/aidenlx/obsidian-icon-shortcodes]
- MKDocs - [Icons, Emojis - Material for MkDocs](https://squidfunk.github.io/mkdocs-material/reference/icons-emojis/)
	- The following icon sets are bundled with Material for MkDocs:
		-  – [Material Design](https://materialdesignicons.com/)
		-  – [FontAwesome](https://fontawesome.com/search?m=free)
		-  – [Octicons](https://octicons.github.com/)
		-  – [Simple Icons](https://simpleicons.org/)




`:fontawesome-solid-dice:` should render as :fontawesome_solid_dice:
`:material-bandage:` should render as :material-bandage:
These are anybodys guess: 
- Roll: :fontawesome_solid_dice: :rpg_awesome_perspective_dice_six:
- Strength: :muscle
- Miss: :fas_minus: : material-numeric-6-box-multiple: :material-minus:
- Weak Hit: :material-numeric-7-box-multiple: - :material-numeric-9-box-multiple:
- Strong Hit: :fas_greater_than_equal: :material-numeric-10-box-multiple: :material-plus:
- Stats: :fontawesome-solid-scroll: :material-bandage:  :material-run-fast: :material-speedometer: :fontawesome-solid-person-breastfeeding: :material-pill-multiple:
- Move: :fas_angles_right: 
- Cost: :material-checkbox-multiple-marked-circle: :material-package-variant-closed: :fontawesome-solid-money-bills: :fontawesome-solid-money-bill-wave: :material-smoke-detector-variant: :material-smoke-detector-outline: :material-alpha-c-circle: :material-checkbox-multiple-blank-circle-outline: :material-hand-coin: :fontawesome-solid-coins:
- Specific Move icons : :rpg_awesome_broadsword: :rpg_awesome_crossbow: :rpg_awesome_archer: :fontawesome_solid_hands_asl_interpreting:  :fontawesome_solid_handshake_angle: :luc_chevrons_down: :fontawesome_solid_expand_alt: :fontawesome_solid_hand_dots: :rpg_awesome_round_shield: :fontawesome_solid_person_walking:
- Harm: :material-water-circle: :fontawesome_solid-heart-circle-xmark: :material-heart-off: :material-heart-box: :material-heart-circle: :fontawesome-solid-heart-crack:



## Obsidian Dialog Plugin


```dialogue
left: Ingmar Bergman
right: Wong Kar-wai

< I will talk
> And now I will

```



```dialogue
left: Ingmar Bergman
right: Wong Kar-wai

< I will talk
> And now I will

```
