---
alias: 
cssClasses: embed-strict
date: 2022-11-26
dateModified: 2023-06-11
fileClass:
  - Note
image: 
stage: 🌿 Fern
share: true
slug: using-controlnet-to-create-battle-maps
title: Using ControlNet to Create Battle Maps
---

[[Image Generative AI|Image Generative AI]] is great for creating art, but will struggle with something like a battle map that needs consistent room sizes, doors, etc that conform to a rigid grid.

Using [[ControlNet|ControlNet]], we can try to constrain the output of [[Stable Diffusion|Stable Diffusion]] to the specific geometry of a battle map.

[[Stable Diffusion|Stable Diffusion]] models trained on the 'look/feel' of battle maps
- models
	- [D&D battlemaps - 1024 v1.0 | Stable Diffusion Checkpoint | Civitai](https://civitai.com/models/23240/dandd-battlemaps)
		- [!] 2.1 model, not compatible (yet) with ControlNet models
	- [DnD Map Generator - v3 | Stable Diffusion Checkpoint | Civitai](https://civitai.com/models/5012/dnd-map-generator)
- LoRAs
	- [Table Rpg / D&D Maps #11 - Mix (op1) - v1.0 | Stable Diffusion LoRA | Civitai](https://civitai.com/models/71700/table-rpg-dandd-maps-11-mix-op1)

![[./assets/images/Pasted image 20230506214609.png|300]]

Raw Map
- [Dungeon Scrawl](https://www.dungeonscrawl.com/) can generate quick maps which we can feed to ControlNet.

![[./assets/images/map_24x24 (1).png|300]]

Taking the raw map from Dungeon SCrawl, we can preprocess it with the Canny [[ControlNet|ControlNet]] model to create distinct edges.

![[./assets/images/Pasted image 20230506215746.png|300]]

Using the canny output, we can put these all together to constrain the Stable Diffusion model to create this output.

![[./assets/images/Pasted image 20230506214553.png|Pasted image 20230506214553.png]]

Nice! Obviously it's a bit blurry but that's fixable. 
What we _have_ proved is we can provide composable inputs that add style to a map without changing the underlying content.

---

From here, we probably want to explore [[Upscaling Stable Diffusion Outputs|Upscaling Stable Diffusion Outputs]] to add more detail and resolution to the generated maps.

We also might want to explore [[Regional Prompting With Stable Diffusion|Regional Prompting With Stable Diffusion]] to specify specific areas as a bedroom, tavern interior, forest, etc.
