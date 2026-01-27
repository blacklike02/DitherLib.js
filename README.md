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
dither               Algorithm (floyd-steinberg, atkinson, stucki, sierra, ordered, random)
dither-palette       Palette (gameboy, c64, cga, ega, apple2, bw, sepia)
dither-levels        Color count 2-256 (default 2)
dither-color         Color mode true/false (default false)
dither-contrast      Contrast 0.1-3.0 (default 1.0)
dither-brightness    Brightness -1.0 - 1.0 (default 0)
dither-diffusion     Effect strength 0-1.0 (default 1.0)
dither-serpentine    Quality improvement true/false (default false)
dither-fps           Frames per second for video/GIF 1-60 (default 30)
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

// GIF
const ctrl = DitherLib.applyToGif(gif, { palette: 'gameboy' });
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
  fps: 30
}
```

## Algorithms

```
floyd-steinberg      Universal, classic
atkinson             Soft effect
stucki               High quality for photos
sierra               Fast, good balance
ordered/bayer        Patterns, for textures
random/noise         Random noise
```

Full list: floyd-steinberg, atkinson, jarvis-judice-ninke, stucki, burkes, sierra, sierra-lite, two-row-sierra, ordered, bayer, random, noise

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

<!-- Newspaper print -->
<img src="photo.jpg" dither="floyd-steinberg" dither-contrast="1.3" dither-serpentine="true">

<!-- Color pixel art -->
<img src="photo.jpg" dither="ordered" dither-color="true" dither-levels="3">
```

```javascript
// Dynamic processing
DitherLib.apply(img, {
  algorithm: 'sierra',
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

