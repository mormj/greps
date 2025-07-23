# GREP [0027] -- [GNU Radio 4.0 Licensing and Repo Structure]

- Original Author: [Josh Morman <jmorman@gnuradio.org>]
- Champion: [TBD]
- Status: Draft 

History:
- 23-Jul-2025: Initial Draft

## Abstract

GNU Radio 4.0 built upon the gnuradio4 repo from FAIR gives the project licensing flexibility, but also needs to 
support the integration of GPL licensed modules.  This GREP proposes a naming and repo structure to be consistent
with the project history, but take advantage of the permissively licensed core

## Copyright / License

CC-BY-ND

## Motivation

There is a strong desire with the introduction of GNU Radio 4.0 to have the ability to expand the userbase beyond lab based prototyping
and allow deeper integrations into industry.  Permissive licensing of at least parts of the codebase are required
in some scenarios to enable collaboration where previously not possible.  By making the licensing of the core (and thus derived works)
more permissive we hope to 

- Maximize adoption and enable public-private collaboration
- Encourage contributions from a diverse ecosystem by lowering legal barriers
- Remain free in the sense of open source principles
- Empower submodule authors to license as desired
- Stay compliant in evolving legal landscapes


The repository structure should help in keeping the license distinctions clean and modular

Note: No part of existing GNU Radio (3.x) is being relicensed

## Description

### What gets licensed as what

The "core" should be MIT licensed to be compatible with the broadest range of licenses.  This includes in-tree runtime, schedulers, base classes, framework, and a minimal set of blocks.  

Things that migrate from GNU Radio 3.x, or are developed by entities who desire for these blocks to be licensed as such should be GPLv3

Primarily, the following GR3 modules should be migrated into GR4 as GPLv3:
- gr-dtv
- gr-channels
- gr-fec
- gr-digital
- gr-analog (many simpler math blocks migrated elsewhere)
- gr-zeromq
- gr-network
- gr-fftw (since FFTW is GPLv3)

More fundamental blocks like mathematical operations, filtering, and enough processing to get to basic meaningful working examples (e.g. FM radio transmit and receive) can stay in the radio-core, or a separate MIT licensed block module

### Components

### Repo Structure

The following should be separate repositories

```
github
└── gnuradio
    ├── gnuradio4
    ├── gr4-official
    ├── gr4-extended
    ├── gr4-[OOT Module Name] ...
    └── radio-core
```

#### dependencies

License: Compatible with MIT

Dependencies that live within the `gnuradio` workspace that radio-core will rely on need to be MIT or MIT compatible.  Currently this should only be PMT


#### radio-core

License: MIT

The bulk of the current `gnuradio4` repo which includes the in-tree runtime, schedulers, base classes, framework, and a minimal set of blocks.  

#### gr4-official

License: GPLv3

This is the set of blocks that officially developed and maintained by the GNU Radio organization and community.  


#### gr4-extended

License: ???

This is the set of blocks that is perhaps more experimental or application specific in nature 


#### gr4-[OOT Module Name]

License: As inherited from the initial author

Multiple OOT modules that the project inherits to maintain in the `gnuradio` workspace need to maintain the original license


#### gnuradio4

License: LGPL????

This is the builder project that brings together the `radio-core` and all the supported blocksets.  Also could grab other OOTs from elsewhere on the
internet for installation into a prefix - without becoming a custom package manager

Can be built with flags such as `NOGPL` or turn on/off individual modules for building and installation



