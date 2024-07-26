<div align="center">

### [TO UPDATE based on KLC]
# Resource Files conventions

</div>

<div align="center">

![Open source](https://img.shields.io/badge/open-source-6894d4?logo=git&logoColor=6894d4)
![GitHub license](https://img.shields.io/github/license/Lpwlk/AetherStack?color=86c255 "Github repo license")
[![GitHub profile](https://img.shields.io/static/v1?label=Lpwlk&message=profile&color=6894d4&logo=github)](https://github.com/Lpwlk "Go to GitHub profile page")
[![GitHub tags](https://img.shields.io/github/v/tag/Lpwlk/AetherStack?color=6894d4)](https://github.com/Lpwlk/AetherStack/tags "Go to GitHub repo tags")
[![GitHub last release](https://img.shields.io/github/release-date/Lpwlk/AetherStack?color=6894d4?label=Release)](https://github.com/Lpwlk/AetherStack "Go to GitHub repo")

</div>

## Table of Contents

1 - [Symbols](#1---symbols)  
&nbsp;&nbsp;&nbsp;1.1 - [Naming convention](#11---naming-convention)  
&nbsp;&nbsp;&nbsp;1.2 - [Examples](#12---examples)  
2 - [Footprints](#2---footprints)  
&nbsp;&nbsp;&nbsp;2.1 - [Naming convention](#21---naming-convention)  
&nbsp;&nbsp;&nbsp;2.2 - [Examples](#22---examples)  
3 - [3D Models](#3---3d-models)  
&nbsp;&nbsp;&nbsp;3.1 - [Naming convention](#31---naming-convention)  
&nbsp;&nbsp;&nbsp;3.2 - [Examples](#32---examples)  
4 - [Contribution guidelines](#4---contribution-guidelines)

#### [Back to README](../README.md)

<div align="center">
<img src="https://github.com/Lpwlk/Lpwlk/blob/main/assets/pulsing-bar.gif?raw=true">
&nbsp;
</div>

This document aims to describe the ressources directory architecture and define naming conventions (nomenclature) for every ressource files used in this project. Every ressource file included in the project should be available from one of these online databases[^1].

```js
AetherStack
├── AetherFC (kicad project #1)
├── AetherESC (kicad project #2)
├── [...]
└── Ressources
    ├── Symbols
    │   ├── component_desc.kicad_sym
    │   └── [...]
    ├── Footprints
    │   ├── part_number.pretty
    │   │   ├── extended_part_number.kicad_mod
    │   │   └──[...]
    │   └── [...]
    └── Stepmodels
    │   ├── part_number.3dshapes
    │   │   ├── extended_part_number.kicad_mod
    │   │   └──[...]
    │   └── [...]
```

As we can see in the `AetherStack` repository structure, the `Ressources` directory includes all of the design files required by both kicad projects. These ressources are shared because some of the files it include are used by both projects. 

The directory is included in the version control to allow anyone to render & contribute to the project using kicad V6+. However, careful attention should be given to respect the *KiCad Library Convention*[^2] when editing the `Ressources` directory content.

> [!NOTE]
Advices on library & project management are welcome since this is my first "complex" development project on KiCad and I am probably not using some of the useful software tools/plugins.

## 1 - Symbols

Symbols represent the schematic symbols used this KiCad projects. They are stored in the `Symbols` directory as `.kicad_sym` files. This project uses only generic symbols. Generic symbols do not have a default footprint assigned.

### 1.1 - Naming Convention

- **File Extension**: `.kicad_sym`
- **Format**: `{component_desc}.kicad_sym`

The `component_desc` filename should be a concise and role-related description of the symbolized component.

This convention has multiple advantages when it comes to project development & review ...

 - **Lisibility** for project developement & review
 - **Generic symbols** allow flexibility in the design workflow. 
 - **Fast symbol edition** for multiple components with common pinout

> [!NOTE] 
Consice `component_desc` format : 1-to-3 camel-cased words with trailing underscore-separated uppercase tag(s) for eventual component declinations.

### 1.2 - Examples

Based on the previously described nomenclature, the `Symbols` directory should look like this ...

```
└── Symbols
    ├── Resistor.kicad_sym
    ├── InertialSensor.kicad_sym
    └── stm32MCU_F7_LQFP64.kicad_sym
```

<div align="center">
    <img src="https://github.com/Lpwlk/Lpwlk/blob/main/assets/pulsing-bar.gif?raw=true">
</div>

## 2 - Footprints

Footprints are basically the PCB implantation data of each schematic components. They are stored in the `Footprints` directory as `.pretty`collections of `.kicad_mod` files. 

### 2.1 - Naming Convention

 - **File Extension**: `.kicad_mod`
 - **Format**: `{part_number}.pretty/{extended_part_number}.kicad_mod`

The `part_number` directory name refers to the component's manufacturer part number (and not to the supplier one) whereas the `extended_part_number` filename is supposed to refer to component declinations (design preferences or available packages). 

This convention has multiple advantages when it comes to project development & review ...

 - **Lisibility** for project developement & review
 - **Generic symbols** for multiple components with common pinout
 - **Fast symbol edition** for multiple components with common pinout

> [!NOTE] 
Likehas for the symbols, the eventual component declinations are separated using trailing underscore-separated uppercase tag(s). In the case of footprints, an unique package tag should be sufficient (e.g. `_LQFP64`)

### 2.2 - Examples

Based on the previously described nomenclature, the `Footprints` directory should look like this ...

```
└── Footprints
    ├── ICM-20689.pretty
    │   └── ICM-20689.kicad_mod
    ├── STM32F722RETx.pretty
    │   ├── STM32F722RETx_LQFP64.kicad_mod
    │   ├── STM32F722RETx_LQFP100.kicad_mod
    │   └──[...]
    └── [...]
```

<div align="center">
    <img src="https://github.com/Lpwlk/Lpwlk/blob/main/assets/pulsing-bar.gif?raw=true">
</div>

## 3 - 3D Models

3D models allow to display the designed board in the KiCad PCB 3D viewer used this KiCad projects. They are stored in `.step` files which have to be associated with footprint(s) from the `Footprints`directory.

### 3.1 - Naming Convention

- **File Extension**: `.step`
- **Format**: `{extended_part_number}.step`

The `extended_part_number` filename should follow the `.kicad_mod` [filename format](#21---naming-convention) 
 in order to  <u>match at least one of the footprint filenames</u> contained in the `Footprints`directory. This allows to verify quickly if the right 3D  model is associated with any footprint used in the project.

### 3.2 - Examples

Based on the previously described nomenclature, the `Stepmodels` directory should look like this ...

```
└── Stepmodels
    ├── STM32F722RETx_LQFP64.step
    ├── STM32F722RETx_LQFP100.step
    ├── ICM-20689.step
    └── [...]
```

<div align="center">
    <img src="https://github.com/Lpwlk/Lpwlk/blob/main/assets/pulsing-bar.gif?raw=true">
</div>

## 4 - Contribution guidelines

Please make sure your contributions to the project respect the few following guidelines when it comes to ressources (symbols, footprints & 3D Models) management.

 - Respect all the previous indications about naming conventions for any modification of the project's library.
 - Provide clear explanation in the case of major change in the KiCad project's configurations and structures.


<div align="center">

<samp>

###### Mardown file generated using <a href ="https://github.com/Lpwlk/ReadmeEngine">readme-engine</a>

####  [Back to TOP](#table-of-contents) | [Back to README](../README.md)
</samp>

</div>

[^1]: Online KiCad component library databases : [KiCad GitLab](https://gitlab.com/kicad/libraries) | [KiCad References page](https://www.kicad.org/libraries/third_party/) | [Ultra librarian](https://www.ultralibrarian.com/) | [SnapEDA](https://www.snapeda.com/home/)

[^2]: Official KiCad libraries contribution requirements: [KiCad Library Convention (KLC)](https://klc.kicad.org/)
