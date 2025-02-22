---
aliases: 
date: 2022-01-18
dateModified: 2024-07-07
fileClass:
  - Page
image: 
share: true
stage: 🌿 Fern
title: I built a Pikachu classifier because there's way too many of them.
---

Using state-of-the-art convolutional neural networks, we can finally tell the difference between Pikachu and Plusle, Minun, Pachirisu, Emolga, Dedenne, Togedemaru, Morpeko....

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Kc5aLgwfL2_3qmC9goN_tgsnDzEfS4yf?usp=sharing)

Creating over a thousand distinct creatures is pretty hard, right? I've always said that. At some point, it's pretty understandable that GameFreak would have some repeated archetypes over 20yrs.

And for some reason, _Electric Rodent_ is #1.

Depending on who you ask, there are upwards of a dozen entirely seperate 'mons that fit into the [Pikachu Family](https://pokemon.fandom.com/wiki/Pikachu-family_Pok%C3%A9mon "Pikachu Family"), a fan term for the litany  of all-too-similar-looking mice, rats, squirrels, hedgehogs, and gerbils that (adorably) infest the Pokémon world.

![[./assets/images/pika_family_update.png|pika_family_update.png]]

Of course, this presents a distinct challenge for anyone who doesn't want to take take a college course on poké-taxonomy and just wants to know _which_ 'mon they saw a cute plushie for at Target.

To that end, [Check Out The Colab](https://colab.research.google.com/drive/1Kc5aLgwfL2_3qmC9goN_tgsnDzEfS4yf?usp=sharing)

It covers how to set up an Azure API instance to scrape the images, cleaning the data for consumption (removing transparency, corrupt files), transforming the images (setting dataloaders, resizing, adding image transforms, etc), building and evaluating a CNN against the data (spoiler: it does pretty well), and finally pickling the model for later inference, I even added a little UI at the end where you can add your own images to see how it does.
