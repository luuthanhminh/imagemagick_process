# Image Editing

## Prerequisites

- [ImageMagick 7x](https://imagemagick.org/script/download.php)


## Image Colorspace converstion

- Copy sRGB profile `sRGB-IEC61966-2.1.icc` into host system
- Convertion command

```sh
$ magick convert INPUT_IMAGE -intent Perceptual -profile sRGB-IEC61966-2.1.icc -black-point-compensation -dither Floyd-Steinberg -interlace plane OUTPUT_IMAGE
```

For example:

```sh

$ magick convert input_cmyk.jpeg -intent Perceptual -profile sRGB-IEC61966-2.1.icc -black-point-compensation -dither Floyd-Steinberg -interlace plane output_sRGB.jpeg
```

## Extracting layers from TIFF image

- Extracting command

```sh

$ magick convert INPUT_IMAGE.tif OUTPUT_IMAGE_%d.tif
```
- `%d` is layer number in order.
- Output is array of images: OUTPUT_IMAGE_1, OUTPUT_IMAGE_2,....

- From output images, check if which image has transparent background by get opacity value. The final output image has opacity value be the closest number to 0

```sh
# Value is from 0 -> 1
$ magick convert INPUT_IMAGE.tif -alpha Extract -format "%[fx:mean]" info:
```

## Get image metadata in json format

```sh

magick convert INPUT_IMAGE rose: metadata_output.json
```