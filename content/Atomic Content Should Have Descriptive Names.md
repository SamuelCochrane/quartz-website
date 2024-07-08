---
alias: 
date: 2023-08-30
dateModified: 2023-09-06
fileClass:
  - Note
image: 
share: true
stage: 🌱 Seedling
title: Atomic Content Should Have Descriptive Names
---

> A name should tell you why it exists, what it does, and how it is used. If a name requires a comment, then the name does not reveal its intent.
> -- Clean Code

[[./Atomic Content|Atomic Content]] should only define one 'idea'. It should be clear from the name what that is.

### Why

[[./Atomic Content|Atomic Content]] is only useful when interlinked with other Atomic Content. Creating clarity on what's being linked to makes life easier. We're not going for intrigue, we're going for operational ease.

### How

Avoid Clickbait. Don't phrase it like a question, phrase it like an answer. 
- Don't: `Was Licoln a Bad President?`
- Do: `Reasons Lincoln Was a Good President`. 
It's much more obvious what the second one contains and returns.

[[Atomic Code|Atomic Code]] should follow a similar pattern:
- Don't: `var d; // elapsed time in days`
- Do: `var elapsedTimeInDays;`

Clean Code suggests naming methods with verb-like names such as "deletePage" or "getUsers" to make it clear what you "get out of" the method.

[[Atomic Notes|Atomic Notes]] should be named much the same way you'd name your [[Atomic Code|Atomic Code]]: In a way that clearly communicates what this thing does and what info it will return.

`GetCurrentOpinionOnDoritos()`
`[[My Current Opinion On Doritos]]`
