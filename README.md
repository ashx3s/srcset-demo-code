# Srcset, Sizes, and Image Optimization

- `srcset` is an html attribute that identifies which image to render from a set depending on specified circumstances.
- use `srcset` and `sizes` together to serve web content that renders best for the user's device.

---

## Srcset

'Here are my images, pick whichever one you think is best'

### General Theory

- Pixels render differently depending on the screen size
- This syntax makes use of saving multiple sizes of the same image in full, lg, md, sm directories
- Use a logical naming system that includes same title and a distinction between them
  - you can use lg, md, sm (But if you have lots of image sizes this could become difficult later)
- When using chrome, the browser will cache the high res version of the image once it serves that and the other ones wont be needed anymore.
- **Important** This is particularly important for the initial load on different sized screens.
- Note that this example follows a mobile first approach

### Methods

- To create a srcset, define which version to use per display size

```
<img src="path-to-img/img-small.jpg"
  srcset="path-to-first-img/img-small.jpg 320w, path-to-second-img/img-medium.jpg 800w, path-to-third-img/img-large.jpg 1200w" 
  alt="describe image">
```
- Check your image sizes and be ready to play with your compression a bit as finding a good balance between quality and weight is important.
- in your html, use the `200w` syntax for widths
  - this helps improve speed because when the browser loads the image, these numbers + w will tell it how much space to save while the browser displays all the content

#### A note on `1x, 2x, 3x` syntax
- you can replace overt widths as shown above with `1x`, `2x`, `3x`

---

## Sizes
'At this viewport size I want an image slot this wide`
### General Theory
- This is used to specify the size range of image versions
- With your sizes, you essentially add media query breakpoints into your markup
- Use this alongside `srcset`
- sizes specifies width for image layout, this is not the same as srcset - srcset is the real img width. Sizes is for creating a placeholder for the image to be loaded into
- You cannot use percentages
- Don't use sizes to serve specific images. That is handled by `srcset`
- **Important** The browser will usually pick `srcset`'s smallest image that is _wider_ than the `sizes` slot.

### Method
- add `sizes` attribute after your `srcset`
- set your breakpoints and widths

```
<img src="path/img-sm.webp"
  srcset="path/img-sm.webp 320w,
    path/img-md.webp 800w,
    path/img-lg.webp 1200w"
  sizes="(min-width: 960px) 80vw,
         (min-width: 640px) 90vw,
         100vw"
  alt="img description>
```

#### Syntax

- `sizes="(breakpoint: value) value"`
- you can set multiple breakpoints

#### Logic Notes
- In this example the sizes declaration translate to:
  - **If** the viewport is at least 960 pixels wide, **then** make the slot for the image 80vw
  - **Else If** the viewport is at least 640 pixels wide, **then** make the slot for the image 90vw
  - **Else** make the slot for the image 100vw 
- This will effect the img selection
  - As the slot is 80vw at 960px, the actual px size of the slot will be closer to 860px
  - And the breakpoint at 640px slot will be closer to 570px
- This means that
  - if the slot is at 810px, img-lg will be used
  - if the slot is 780px, img-md will be used
  - as long as the slot is img-sm will be used

---

## Attributions

- [Penguin Photo](https://images.pexels.com/photos/4169874/pexels-photo-4169874.jpeg?auto=compress&cs=tinysrgb&h=750&w=1260) by [Vladimir Blyufer](https://www.pexels.com/@vladimir-blyufer-1991484) under a [Pexels Lcense](https://www.pexels.com/license/)
- [Video](https://www.youtube.com/watch?v=2QYpkrX2N48&t=559s) by [Kevin Powell](https://www.youtube.com/channel/UCJZv4d5rbIKd4QHMPkcABCw) under [Creative Commons License](https://creativecommons.org/)
- [Article](https://webdesign.tutsplus.com/tutorials/quick-tip-how-to-use-html5-picture-for-responsive-images--cms-21015) on using srcset and sizes
  - example logic in sizes is from this article