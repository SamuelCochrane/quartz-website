---
alias: 
cssClasses: embed-strict
date: 2022-11-26
dateModified: 2023-06-24
fileClass:
  - Note
image: 
stage: 🌱 Seedling
share: true
title: T2I-Adapter
---

T2I-Adapter is an injection-based SD control, an additional model that can sit "in front" of a [[Stable Diffusion|Stable Diffusion]] model to help control the outputs. See their [Overview on Github](https://github.com/TencentARC/T2I-Adapter/blob/main/docs/coadapter.md). 
![](https://user-images.githubusercontent.com/17445847/225639246-26ee67a9-a9d9-47e4-b3bf-813d570e3d96.png)

T2I-Adapter is similar to [[ControlNet|ControlNet]], allowing you to define a depth-map, outline, etc for your [[Stable Diffusion|Stable Diffusion]] model's output.

![](https://user-images.githubusercontent.com/17445847/225656254-f0aff320-42fc-49bf-b8ff-9a779ad68db1.png)

### Unique Features

T2I seems to do a lot of the same things as [[ControlNet|ControlNet]], and I haven't yet explored the differences.

One unique feature for now is allowing for a style image as input _(not currently supported by [[ControlNet|ControlNet]])._ This makes T2I pivotal for doing [[./Style Transfer From Image In Stable Diffusion|Style Transfer From Image In Stable Diffusion]].

| Sketch | Style image | Result |
| --- | --- | --- |
|  ![](https://user-images.githubusercontent.com/11482921/225659269-2d50e40d-f79b-41bc-9a0e-9dc73663f010.png)   | ![](https://user-images.githubusercontent.com/11482921/225659792-07f3d5f4-3e26-4c52-988b-c4f228d6e45d.jpeg)    | ![](https://user-images.githubusercontent.com/11482921/225660076-665b5889-3825-48cc-b9f9-06903fdd0c4b.jpg)    |

### Using T2I

To use T2I, you can download models from [GitHub - TencentARC/T2I-Adapter: T2I-Adapter](https://github.com/TencentARC/T2I-Adapter)

The [ControlNet WebUI Extension](https://github.com/Mikubill/sd-webui-controlnet) (which is just a UI, _not_ the actual [[ControlNet|ControlNet]] models) now supports T2I models as well.
