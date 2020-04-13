Export for earthgen
=
An Earth-like planet generator with export to icosahedral (Dymaxion) and equirectangular projections.

Earthgen
-
Earthgen is a tool developed by vraid. You can find the original version [here](https://github.com/vraid/earthgen) and it's older version written on C++ [here](https://github.com/vraid/earthgen-old). The latter has better Readme with a list of things the program does. The newer version has no documentation

Export
-
Although the earthgen is a fascinating project, there was no built-in export functionality. Therefore, its use is limited. This repository contains additional racket and python scripts to export the generated planet. The racket script
`export.rkt` generates file `earthgen_export.py` that contains the necessary information about the planet in a python format. The python script `generate_images.py` tries to categorize each tile to one of the following groups best to its ability:

- Jungle Forest
- Heavy Jungle Forest
- Deciduous Forest
- Heavy Deciduous Forest
- Mixed Forest
- Heavy Mixed Forest
- Boreal Forest
- Heavy Boreal Forest
- Grass
- Warm Desert
- Cold Desert
- Savanna
- Swamp
- Marsh
- Hill Jungle Forest
- Hill Deciduous Forest
- Hill Mixed Forest
- Hill Boreal Forest
- Hill Savanna
- Mountain Jungle Forest
- Mountains Jungle Forest
- Mountain Deciduous Forest
- Mountains Deciduous Forest
- Mountain Mixed Forest
- Mountains Mixed Forest
- Mountain Boreal Forest
- Mountains Boreal Forest
- Mountain
- Mountains
- Snow Mountain
- Snow Mountains
- Surface Ocean
- Mid Ocean
- Deep Ocean

Then, 3 images are generated, using icons from `pics` directory. The images are icosahedral map projection, equirectangular map projection, and equirectangular height map projection. The icons are the same used in [hexographer/worldographer](https://www.hexographer.com/). The intended use of icosahedral map projection is to be traced in hexographer/worldographer. The intended use of equirectangular map projections is to be used in [MapToGlobe](https://www.maptoglobe.com/). Note, that if you use heightmap in MapToGlobe, there are some known issues with lightning (the problem of MapToGlobe, not the heightmap generated by this program). The output pictures are located in the `./output` directory by default. See instruction to change settings / seeds for planet generation or tile classification / icons / output image resolution below.

### Racket

DrRacket can be downloaded [here](https://download.racket-lang.org/)

once installed, set memory to unlimited (in Racket -> Limit Memory), then restart DrRacket

in File -> Install Package, install the package located in "earthgen/package/vraid/"

### Python

You can download and install Python 3 [here](https://www.python.org/downloads/)

Configuration
-
### Planet generation (Racket)

There are two files you can modify to change the configuration used in planet generation: `./export.rkt` and `./terrain-generation/default.txt`

#### export.rkt

```(define planet-characteristic-size 4)```
The number characterizes the size of the planet. 0 is a minimal number, the highest I ever went was 10 and it's way more than needed in most cases. ```diff - Use only even numbers for the export to work```

``` 
    #:axial-tilt (/ pi 8)
    #:acceptable-delta 0.05
    #:precipitation-factor 1.0
    #:humidity-half-life-days 5.0
    #:seasons-per-cycle 4)
```
[Axial tilt](https://en.wikipedia.org/wiki/Axial_tilt) is defined in radians and a non-zero value is required for a season change. All other factors have such values that the generated planet is close to Earth's conditions. `seasons-per-cycle` how many states of climate are generated within one planet year, see explanatory picture [here](https://github.com/vraid/earthgen-old#seasonal-variation). Different seasons are only used in python script to classify tiles (ex.). So, there is no reason to have many seasons, unless you are modifying the python script.


#### default.txt

This file contains some settings for the planet generation. I will not go into detail as this is the part of earthgen. You are welcome to try different combinations of values. The values you most likely want to change here are seeds on lines 8, 21, and 27. Changing them will generate different planets (otherwise, the generated planet would be always the same). To change them, just substitute numbers, ex.
```[seed (seed 0)]```
to
```[seed (seed 75)]```

### Export (Python)
The parameters in the code are heavily commented, so if you want to change something, read the comments. The default settings are for Windows. To run the script just type
`python generate_images.py`
You might need to add python to the PATH environmental variable on Windows (google "python add to PATH").


To do
-
Add export of rivers

Final Notes
-
This is my first experience with Racket and functional programming in general. I had no intention to learn it until I decided to do this project. I feel that I didn't spend enough time getting into the language paradigms and as a result, the code might go against language concepts. The output of the racket script also contains a lot of redundant information and can be heavily reduced.
