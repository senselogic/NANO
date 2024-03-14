![](https://github.com/senselogic/NANO/blob/master/LOGO/nano.png)

# Nano

Image variant generator.

## Description

Nano generates image variants in different sizes and file formats.

## Installation

Install the [DMD 2 compiler](https://dlang.org/download.html) (using the MinGW setup option on Windows).

Build the executable with the following command line :

```bash
dmd -m64 nano.d
```

## Command line

```
nano [`<option>` ...] `<source folder path>` `<target folder path>`
```

### Options

```
--surface-ratio <surface ratio>
--quality-list <quality list>
--width-list <name> <width list>
--command-list <name> <command list>
--default-command-list <default command list>
--image-name-format <image name format>
--tool-path <tool path>
--recursive : process subfolders too
--keep : keep existing target images if they are newer than their source image
```

## Usage

### Commands

The source image file names can have one or several commands before their extension.

For instance :

*   "image.**jl**.png" generates "image.png.960.jpg"
*   "image.**j960**.png" generates "image.png.960.jpg"
*   "image.**j960@90**.png" generates "image.png.960.jpg" at 90% quality
*   "image.**jm@10.jl4**.png" generates "image.png.480.jpg", "image.png.960.jpg", "image.png.1920.jpg", "image.png.2880.jpg", "image.png.3840.jpg"
*   "image.**pt3**.png" generates "image.png.160.png", "image.png.320.png", "image.png.480.png"
*   "image.**p160,320,480**.png" generates "image.png.160.png", "image.png.320.png", "image.png.480.png"
*   "image.**p160,320,480@90,70,60**.png" generates "image.png.160.png" at 90% quality, "image.png.320.png" at 70% quality, "image.png.480.png" at 60% quality

The default command list is used if none was provided.

The first character of a command can be :

*   **@** : use default command list
*   **@** `<definition name>` : use named command list
*   **s** `<surface ratio>` : set surface ratio
*   **a** : generate .avif files
*   **j** : generate .jpg files
*   **p** : generate .png files
*   **w** : generate .webp files

For image generation commands, the next characters specify the target width list :

*   `<width>`,`<width>`,...

Alternatively, a named target width list can be used.

Here are those defined by default :

*   **n** : 80
*   **n2** : 80, 160
*   **n3** : 80, 160, 240
*   **n4** : 80, 160, 240, 320
*   **t** : 160
*   **t2** : 160, 320
*   **t3** : 160, 320, 480
*   **t4** : 160, 320, 480, 640
*   **s** : 320
*   **s2** : 320, 640
*   **s3** : 320, 640, 960
*   **s4** : 320, 640, 960, 1280
*   **c** : 480
*   **c2** : 480, 960
*   **c3** : 480, 960, 1440
*   **c4** : 480, 960, 1440, 1920
*   **m** : 640
*   **m2** : 640, 1280
*   **m3** : 640, 1280, 1920
*   **m4** : 640, 1280, 1920, 2560
*   **l** : 960
*   **l2** : 960, 1920
*   **l3** : 960, 1920, 2880
*   **l4** : 960, 1920, 2880, 3840
*   **b** : 1280
*   **b2** : 1280, 2560
*   **b3** : 1280, 2560, 3840
*   **h** : 1600
*   **h2** : 1600, 3200
*   **f** : 1920
*   **f2** : 1920, 3840
*   **u** : 3840

Those letters stand for : **N**ano, **T**iny, **S**mall, **C**ompact, **M**edium, **L**arge, **B**ig, **H**uge, **F**ull, **U**ltra.

A custom target quality list can also be specified after **@**.

### Image names

The target image name format can be specified using the following letters :

*   **{l}** : source image label
*   **{e}** : source image extension
*   **{w}** : target image width
*   **{q}** : target image quality
*   **{x}** : target image extension

The default target image name is : **{n}.{e}.{w}.{x}**

## Samples

```csh
nano --default-command-list s16_9.a1920@70 --image-name-format @l.@x --tool-path "convert" --recursive --keep SOURCE/ TARGET/
```

```csh
nano --quality-list 75,70,65,60 --default-command-list s16_9.am@10.al4 --tool-path "convert" --recursive --keep SOURCE/ TARGET/
```

```csh
nano --quality-list 80 --width-list m5 640,1280,1920,2560,3200 --command-list m5 ac@10.am5 --command-list sm5 s16_9.ac@10.am5
     --default-command-list @m5 --tool-path "convert" --recursive --keep SOURCE/ TARGET/
```

## Dependencies

*   ImageMagick convert

## Version

1.0

## Author

Eric Pelzer (ecstatic.coder@gmail.com).

## License

This project is licensed under the GNU General Public License version 3.

See the [LICENSE.md](LICENSE.md) file for details.
