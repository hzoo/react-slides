react-slides

- `npm install` for browsersync (or just run a http-server)
- `npm start` to develop/present
- slide data is all in [index.md](index.md) using [remark.js]

Remark Info
- Uses markdown + html
- `class: ...` specifies css classes to apply to a slide
- `---` is a new slide.
- `--` means create a new slide with the previous content
- `???` you can put speaker notes after this
- `![:scale 100%](imageUrl)` can specify image size
- `background-image: url(imageUrl)` can specify a background image
- `.cssClass[textHere]` can wrap text in a css class
- You can put html as well (I used iframes for youtube videos)

PDF
- Created by changing the screen resolution in Chrome to `900x600` and then `Saving as a PDF`.

[remark.js](https://github.com/gnab/remark)
