---
date: 2023-07-12
dateModified: 2023-09-06
image: 
share: true
stage: 🌱 Seedling
title: Highlight Internal Links
---

A styling pattern where internal links are given a subtle highlight, while external links aren't. 
This allows people to quickly identify which kind of content the link is referencing.

### Styling

To achieve this, I use code that looks something like this (you can always Inspect Element to see the most up to date code).

```css
/* Works because internal links point directly,
   without using http/https. We then filter out specific
   types of links */
a:not([href^=http]):not([class*=md-]) {
    border-radius: 0.25rem;
    background-color: var(--md-accent-fg-color--transparent);
    padding: 2px 1ox;
}
```

### Examples

#### Slack

![[./assets/images/Pasted image 20230712140556.png|Pasted image 20230712140556.png]]

```
.c-member_slug--link, .c-member_slug--mention {
background: #e8912d66;
color: rgba(var(--sk_secondary_highlight,242,199,68);
border-radius: 3px;
padding: 0 2px 1px;
```

#### ClickUp (when Someone Mentions you)

![[./assets/images/Pasted image 20230906134327.png|Pasted image 20230906134327.png]]

```
color: var(--cu-content-primary);
background-color: var(--cu-background-primary-subtle);
position: relative;
padding: 2px 5px;
margin: -2px 0;
border-radius: 3px;
font-weight: 500;
```
