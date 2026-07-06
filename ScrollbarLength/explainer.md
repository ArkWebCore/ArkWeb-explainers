# ScrollbarLength property

## Authors
- Liu Yao Ming [yaomingliu@gmail.com] (ArkWeb)
 
## Introduction

The proposal introduces scrollbar-length as a new CSS property to define the alignment of the scrollbar with its corresponding web element. 

## User-Facing Problem

To provide users with a immersive experience, web apps may display a webpage in full screen. On some platforms, the content may be overlapped by the status bar at the top (e.g., time, battery status, signal strength, and notifications) and the navigation bar at the bottom.   
 
In this scenario, the web content would need to avoid the system bars at the top and the bottom. 
Currently, web developers can achieve this by obtaining the system's safe area from the 'env()' CSS function and then setting a padding for the content.

```
env(safe-area-inset-top);
env(safe-area-inset-bottom);
```

As shown in the figure below, the blue rectangle represents the content box.

However, the scrollbar cannot use the same mechanism, resulting in an inconsistent user experience: the part labeled 3 in the picture.

![Screenshots showing how the scrollbar overlaps the status bar in a smartphone viewport](./images/current.jpg)


 
## Proposal

This proposal aims to introduce CSS longhand properties 'scrollbar-length-x', 'scrollbar-length-y', and shorthand property 'scrollbar-length'.

Syntax:

'scrollbar-length-x: padding-edge | content-edge'

'padding-edge': the horizontal scrollbar has the same length and is horizontally aligned with the padding edge of the element.

'content-edge': the horizontal scrollbar has the same length and is horizontally aligned with the content edge of the element.

### Example:

```html
<!--index.html-->
<!DOCTYPE html>
<html>
	<head>
        <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
		<title>Demo</title>
		<style>
			body {
				width:2560px;
				height:2560px;

				padding-top: env(safe-area-inset-top);
                padding-bottom: env(safe-area-inset-bottom);

                scrollbar-length-y:content-edge;

				border:5px solid blueviolet
			}
		</style>
	</head>
	<body>
		<p>Testing Set padding area for web content and scrollbar</p>
	</body>
</html>
```

![Screenshots showing how the scrollbar overlaps the status bar in a smartphone viewport](./images/after.jpg)

## Other activities to consider 

NA
