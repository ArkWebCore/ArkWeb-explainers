# Maxium fling speed

## Authors:

- Qin Wen Jun (Arkweb)


## Introduction

This proposal aims to establish a declarative mechanism via the HTML `meta` element to limit fling speed on websites with complex dom structure.   

## User-Facing Problem

Modern websites now feature increasingly complex DOM structures with rich functionalities. Many sites host a vast amount of media resources, such as images and videos, while adopting infinite-scrolling designs on mobile for a seamless experience. However, when a page is overloaded, rapid user scrolling (e.g., "flicking" gestures) can strain the rendering engine, potentially causing blank screens due to delayed rendering. Moreover, excessively fast scrolling negatively impacts user experience.

### Goals

- This proposal introduces two new attributes, max-fling-speed-x and max-fling-speed-y, to the content field of the `<meta name="viewport">` tag. These attributes accept ​​positive integer values​​ (in pixels per second, px/s) to cap the maximum fling speed in horizontal (X-axis) and vertical (Y-axis) scrolling, respectively.

## Proposed Approach

```html
<meta name=”viewport” content=”width=device-width, initial-scale=1,max-fling-speed-y=4500”>
<meta name=”viewport” content=”width=device-width, initial-scale=1,max-fling-speed-x=4500”>
<meta name=”viewport” content=”width=device-width, initial-scale=1,max-fling-speed-y=4500,max-fling-speed-x=4500”>
```

## Alternatives considered

scroll event listener: By listening to the scroll event and programmatically adjusting the scroll position (e.g., debouncing or snapping back), we can artificially cap scrolling speed. However, this method ​​negatively impacts performance​​.

## References & acknowledgements

Many thanks for valuable feedback and advice from:

- Ding Wei
- Feng Wei Quan
- Hu Xiao Cheng
- Liu Yao Ming
- Martin Alvarez
- Wang Hui
