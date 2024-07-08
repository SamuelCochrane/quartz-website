---
alias: 
cssClasses: embed-strict
date: 2022-11-26
dateModified: 2023-06-11
title: Style Transfer From Text In Stable Diffusion
fileClass:
  - Note
stage: 🌿 Fern
share: true
---

Using [[Stable Diffusion|Stable Diffusion]], we can alter the style of an image while still leaving it recognizable as the original.

|               Content                |       Style       |                Result                |
|:------------------------------------:|:-----------------:|:------------------------------------:|
| ![[./assets/images/Pasted image 20230624122740.png|Pasted image 20230624122740.png]] | "a bowl of salad" | ![[./assets/images/Pasted image 20230623091446.png|Pasted image 20230623091446.png]] |
|   ![[./assets/images/sad-keanu-meme.webp|sad-keanu-meme.webp]]                                   | "minimalist line art"                  |  ![[./assets/images/Pasted image 20230624165052.png|Pasted image 20230624165052.png]]                                    |

By using img2img, we can provide an inital image as a starting position. Then, providing a prompt and a low denoise value (~0.2) we can generate a batch of slightly altered pictures. Pick our favorite, send it back to img2img, and do it again until we have a result we like.

>[!faq]- Denoise
>Denoise (a value between 0 and 1) defines how much of the original image should be retained as we process a new picture. 
>1.0 gives us a completely new picture
>0.0 gives us the exact same picture.
>A low value like 0.2 means only 20% of the pixels in the generated image should be new, and 80% should be the same.

To further improve these results, we can pair this technique with a few [[ControlNet|ControlNet]] models to help keep the silhouettes consistent. 

Openpose helps keep the pose & face consistent
Canny/Lineart/Depth help keep the structure consistent

Using a photo of myself, I used this technique with the Canny & Openpose models to get a consistent structure while providing a prompt that changed the style.

| Input Image                          | Style                                     | Result                               |
| ------------------------------------ | ----------------------------------------- | ------------------------------------ |
| ![[./assets/images/Pasted image 20230623095317.png|Pasted image 20230623095317.png]] | "Cyberpunk city, 4k Unreal Engine, [...]" | ![[./assets/images/Pasted image 20230623095327.png|Pasted image 20230623095327.png]] |
|                                      | "Norman Rockwell, Painting, [...]"                                          |  ![[./assets/images/Pasted image 20230623095738.png|Pasted image 20230623095738.png]]                                    |
