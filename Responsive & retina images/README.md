# Responsive & retina images

## SRCSET attr

```srcset``` defines the set of images we will allow the browser to choose between, and what size each image is. Each set of image information is separated from the previous one by a comma. For each one, we write:

- An image filename (img-480w.jpg)
- A space
- The image's intrinsic width in pixels (480w) — note that this uses the w unit, not px as you might expect. This is the image's real size, which can be found by inspecting the image file on your computer (for example, on a Mac you can select the image in Finder and press Cmd + I to bring up the info screen).

## SIZES attr

```sizes``` defines a set of media conditions (e.g. screen widths) and indicates what image size would be best to choose, when certain media conditions are true — these are the hints we talked about earlier. In this case, before each comma we write:

- A media condition ((max-width:600px)) — "when the viewport width is 600 pixels or less".
- A space
- The width of the slot the image will fill when the media condition is true (480px). When sizes has not been specified, it’s default value is always 100vw.


## Responsive images

```html
<img srcset="img-480w.jpg 480w, img-800w.jpg 800w"
     sizes="(max-width: 600px) 480px, 800px"
     src="img-800w.jpg" alt="">
```

## Picture element

Like ```<video>``` and ```<audio>```, the ```<picture>``` element is a wrapper containing several ```<source>``` elements that provide different sources for the browser to choose from, followed by the all-important ```<img>``` element.

The ```<source>``` elements include a media attribute
The srcset attributes contain the path to the image to display.
In all cases, you must provide an ```<img>``` element, with src and alt, right before ```</picture>```, otherwise no images will appear.


```html
<picture>
  <source media="(max-width: 799px)" srcset="img-480w.jpg">
  <source media="(min-width: 800px)" srcset="img-800w.jpg">
  <img src="img-800w.jpg" alt="">
</picture>
```


## Retina support

You can specify a pixel density in ```srcset```.

Your browser attempts to calculate the best fit image based on the device width.

For regular devices the ratio it is looking for is 1. If the device is considered “retina." Then the browser will multiply the result by 2 to find the best image size.
```html
<img src="/photo.jpg"

   srcset="/photo@1000w.jpg 1x,

           /photo@2x.jpg 2x,

           /photo@3x.jpg 3x" alt="" />
```

## Retina example with liquid

```html
<img src="{{ block.settings.image | img_url: '180x' }}"
     srcset="{{ block.settings.image | img_url: '360x' }} 2x,
            {{ block.settings.image | img_url: 'master' }} 3x"/>
```
