# Custom g2 extension for Kha to draw shapes using Signed distance fields

The extension uses distance functions as can be found here: [2D distance functions](https://www.iquilezles.org/www/articles/distfunctions2d/distfunctions2d.htm)
to (currently) draw circles and rounded rects, with borders.


## Usage:

1. Add this as a subproject to your project like this:
```javascript
await project.addProject(pathToSDFPainter);
```

2. Create a render target that can be used by SDFPainter to draw on:
```haxe
...
myTarget = Image.createRenderTarget(1280, 720);
sdfPainter = new SDFPainter(myTarget);
...
```

3. Use like g2:
```haxe
...

sdfPainter.begin();  // takes the same arguments as a normal g2 instance.
sdfPainter.color = Color.Red;
sdfPainter.sdfRect(10, 10, 400, 60, {tr: 20, br: 20, tl: 5, bl: 5}, 5, Color.White, 2.2);
// Individual corner radii can be set for each corner. Alternatively only setting corner radius
// for "tr" applies the radius to all four corners.

sdfPainter.color = Color.Cyan;
sdfPainter.sdfCircle(640, 360, 60, 7, Color.Orange, 2.2);
// The last argument for both shapes (2.2) is the amount of pixels to smooth, to avoid aliasing.
sdfPainter.color = Color.White;

sdfPainter.drawImage(myImg, 90, 150);
...
sdfPainter.end();

...
```
