# DitherLib.js
dithering javascript library 
## Installation
```html
<script src="ditheringLib.min.js"></script>
```
## Usage
```html
<img src="photo.jpg" dither="floyd-steinberg">
<img src="photo.jpg" dither="atkinson" dither-palette="gameboy">
<video dither="ordered" dither-fps="30"><source src="video.mp4"></video>
```
## Attributes
```
dither               Algorithm (floyd-steinberg, atkinson, burkes, jarvis-judice-ninke, stucki, sierra, sierra-2, sierra-lite, fan, ordered, random, threshold)
dither-palette       Palette (gameboy, gameboyPocket, c64, cga, cgaPalette1, ega, apple2, bw, sepia)
dither-levels        Color count 2-256 (default 8)
dither-color         Color mode true/false (default false)
dither-contrast      Contrast 0.1-3.0 (default 1.0)
dither-brightness    Brightness -1.0 - 1.0 (default 0)
dither-diffusion     Effect strength 0-1.0 (default 1.0)
dither-serpentine    Quality improvement true/false (default false)
dither-fps           Frames per second for video 1-60 (default 30)
dither-linearize     Linearize colors true/false (default false)
dither-error-multiplier  Error distribution 0-2.0 (default 1.0)
```
## JavaScript API
```javascript
// Auto-initialization
DitherLib.init();
// Image
DitherLib.apply(img, { algorithm: 'atkinson', palette: 'gameboy' });
// Canvas
DitherLib.applyToCanvas(canvas, { levels: 4, isColor: true });
// Video
const ctrl = DitherLib.applyToVideo(video, outputCanvas, { fps: 30 });
ctrl.stop();
ctrl.start();
```
## Configuration
```javascript
{
  algorithm: 'floyd-steinberg',
  palette: 'gameboy',
  levels: 2,
  isColor: false,
  contrast: 1.0,
  brightness: 0,
  diffusion: 1.0,
  serpentine: false,
  fps: 30,
  linearize: false,
  errorMultiplier: 1.0
}
```
## Algorithms
```
floyd-steinberg      Universal, classic
atkinson             Soft effect
burkes               Fast, good quality
jarvis-judice-ninke  High quality, slow
stucki               High quality diffusion
sierra               Balanced quality/speed
sierra-2             Lighter Sierra
sierra-lite          Fastest Sierra
fan                  Directional diffusion
ordered/bayer        Patterns, for textures
random/noise         Random noise
threshold/bitmap     Simple black & white
```
## Palettes
```
gameboy              4 green shades
gameboyPocket        4 gray shades
c64                  16 colors Commodore 64
cga                  4 colors IBM CGA
cgaPalette1          4 colors CGA alternative
ega                  16 colors IBM EGA
apple2               16 colors Apple II
bw                   2 colors black and white
sepia                4 shades vintage
```
## Examples
```html
<!-- Game Boy effect -->
<img src="photo.jpg" dither="atkinson" dither-palette="gameboy" dither-serpentine="true">
<!-- Bitmap style -->
<img src="photo.jpg" dither="threshold">
<!-- Color pixel art -->
<img src="photo.jpg" dither="ordered" dither-color="true" dither-levels="3">
<!-- Video processing -->
<video dither="floyd-steinberg" dither-palette="gameboy" dither-fps="30">
  <source src="video.mp4">
</video>
```
```javascript
// Dynamic processing
DitherLib.apply(img, {
  algorithm: 'burkes',
  palette: 'c64',
  serpentine: true,
  diffusion: 0.8
});
// Video
const controller = DitherLib.applyToVideo(video, canvas, {
  algorithm: 'floyd-steinberg',
  palette: 'gameboy',
  fps: 30
});
```
