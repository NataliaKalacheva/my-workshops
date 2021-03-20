# Dynamically resize crossdomen iframe height to fit content without scroll

## Overview

Usually we can’t predict the height of content in an iframe and often have a second vertical scroll on the page which doesn’t seem so beautiful for our users.

## Solution

- iFrame Resizer Library

This library enables the automatic resizing of the height and width of both same and cross domain iFrames to fit their contained content.
It provides a range of features to address the most common issues with using iFrames.

For cross domain connection you need to have an opportunity add scripts for both websites!

## Installation

### For Host

Add iframeResizer.min.js to the assets folder.

https://github.com/davidjbradshaw/iframe-resizer/blob/master/js/iframeResizer.min.js

```
<iframe id="myIframe" src="/pages/iframe-content" width="100%" title="Test iframe"></iframe>

<script src="{{ 'iframeResizer.min.js' | asset_url }}"></script>
<script>
  iFrameResize({ log: true, scrolling: 'true' }, '#myIframe');
</script>
```

Iframe Width 100% necessary to let lib know that we are going to resize height.

### For Content

Add this file to the content window website.

https://github.com/davidjbradshaw/iframe-resizer/blob/master/js/iframeResizer.contentWindow.min.js

```
<script src="{{ 'iframeResizer.contentWindow.min.js' | asset_url }}"></script>
```