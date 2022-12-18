# VASP - Localized Orbital Locator + Electron Localizability Indicator
This project provides patch files for VASP v6.3.0 that:
1. Enabling calculation of the Localized Orbital Locator (LOL)
2. Enabling calculation of the Electron Localizability Indicators (ELI) parallel-spin electron pair density (D)
3. Fixing [a bug](https://www.vasp.at/forum/viewtopic.php?t=18361) in spin
polarized electron localization function calculations.
4. Updating ELF calculation so that no fictitious high localization will occur in
the vacuum region (see [Tian Lu and Fei-Wu Chen, Meaning and Functional Form of
the Electron Localization Function, Acta Phys. -Chim. Sin. 27 (12), (2011),
2786-2792](https://www.ingentaconnect.com/content/apcs/apcs/2011/00000027/00000012/art00011?crawler=true))
(Check the source for details.)

Before getting into things, you might want to check out the following paper:

1. [H.L Schmider and A.D Becke, Chemical content of the kinetic energy density,
J. Mol. Struct.: THEOCHEM 527 (2000) 51](https://doi.org/10.1016/S0166-1280(00)00477-2)

2. [A. Savin, The electron localization function (ELF) and its relatives:
interpretations and difficulties, J. Mol. Struct.: THEOCHEM 727 (2005) 127–13](https://doi.org/10.1016/j.theochem.2005.02.034)

3. [M. Kohout, Bonding indicators from electron pair density functionals, Faraday Discuss. 135 (2007) 43-54](https://pubs.rsc.org/en/content/articlelanding/2007/fd/b605951c)

4. [M. Kohout, A measure of electron localizability, Int. J. Quantum Chem. 97 (2004) 651-658](https://onlinelibrary.wiley.com/doi/epdf/10.1002/qua.10768)


## Applying patches
1. To enable LOL, ELI-D and the ELF bug fix all together, put the `VASP6.3_ELI_D.patch` under `$VASP_SOURCE` folder
 and issue the following command:
```
patch -p0 < VASP6.3_ELI_D.patch
```

2. To fix the ELF bug, put the `VASPv6.3.0_ELF.patch` under `$VASP_SOURCE` folder
 and issue the following command:
```
patch -p0 < VASP6.3_ELF.patch
```
3. To enable LOL calculation, put `VASPv6.3.0_LOL.patch` under `$VASP_SOURCE`
and issue the following command:
```
patch -p0 < VASP6.3_LOL.patch
```

## Running calculations
Setting `LLOL=.TRUE.` in `INCAR` file will enable the calculation of LOL at the end of the single point cycle.
A file named `LOLCAR` is generated after the calculation.

Setting `LELID=.TRUE.` in `INCAR` file will enable the calculation of ELID at the end of the single point cycle.
A file named `ELIDCAR` is generated after the calculation.

__Note__: [VESTA](https://jp-minerals.org/vesta/en/) treates `LOLCAR` and `ELIDCAR` as charge
density object so the iso-value displayed by it is divided by the volume of the unitcell. You might want to rename them as `ELFCAR_LOL` and `ELFCAR_ELID`

## Disclaimer

*1. VASP is a commercial package, be sure you have a proper license to use it.

*2. `VASPv6.3.0_ELF.patch` is forked directly from [VASP forum](https://www.vasp.at/forum/viewtopic.php?f=3&t=18361).

*3. The correctness of this patch has been checked with few simple cases.
However, this is not guaranteed to work for your specific system. Make sure you KNOW WHAT YOU ARE DOING!
