---
alias: 
cssClasses: embed-strict
date: 2022-11-26
dateModified: 2023-06-25
fileClass:
  - Note
image: 
stage: 🌱 Seedling
share: true
title: Style Transfer From Image In Stable Diffusion
---

Some styles aren't something we can describe in words, and it isn't something the model would be trained on. We need a way to provide an image and tell the model "do something like this".

We can use [[./T2I-Adapter|T2I-Adapter]] on top of [[Stable Diffusion|Stable Diffusion]] to allow for a style image as an additional input.

Using the technique listed in [[./Style Transfer From Text In Stable Diffusion|Style Transfer From Text In Stable Diffusion]], we just add one more step to provide a style image.

>[!note]- Example prompt: Sad Keanu in the style of minimalist line art
>Model: AOM3+orangemix vae
>Sampler: Euler a, 20 steps
>3 ControlNets:
>
>>	- depth w/ original image
>>	- openpose_full w/original image
>>	- t2iadapter_style w/ style image
>
>Prompt:
>
>>	[basic prompt (e.g. man in jacket sitting)]
>>	<lora:add_detail:-0.5> 
>>	cartoon fanart style <lora:cartoon_fanart_style:0.5>
>>	Simple line <lora:20.50:0.5>

Notice that the style image impacts both the color and _content_ of the scene.

| Style Image                                                | Output                               |
| :--------------------------------------------------------: | :----------------------------------: |
| _[none]_                                                   | ![[./assets/images/Pasted image 20230624165052.png|Pasted image 20230624165052.png]] |
| ![[./assets/images/chocolate-chip-cookies.png|chocolate-chip-cookies.png]]                            | ![[./assets/images/Pasted image 20230624162236.png|Pasted image 20230624162236.png]] |
| ![[./assets/images/Reddit-Productivity-feature-image-in-ClickUp-blog.png|Reddit-Productivity-feature-image-in-ClickUp-blog.png]] | ![[./assets/images/Pasted image 20230624163213.png|Pasted image 20230624163213.png]] |
| ![[./assets/images/xzivdk4kgjxejm2qkbpb.png|xzivdk4kgjxejm2qkbpb.png]]                              | ![[./assets/images/Pasted image 20230624164116.png|Pasted image 20230624164116.png]] |
| ![[./assets/images/download (1).png|download (1).png]]                                      | ![[./assets/images/Pasted image 20230624164400.png|Pasted image 20230624164400.png]] |
