---
layout: default_en
title: home_en
permalink: /home_en
---

# AkaiKKR

- AkaiKKR is an ab-initio software based on the density function theory proposed by Korringa, Kohn, Rostoker [1, 2].

- The CPA (Coherent Potential Approximation) method [3] can be naturally applied to the KKR method. By using this combination (the KKR-CPA method [4]), we can calculate alloys and impurity systems at high speed. 

## Functions

- Electronic state calculation by using the KKR-CPA method. We can perform calculations for SCF, the density of states, and the energy dispersion.

- Percentage of atoms can be specified for each position. We can calculate the system with alloys, vacancies, and impurities.

- We can deal with relativity (scalar relativity, spin-orbit interaction) and magnetism.

- The exchange correlation potential can be selected from Morruzi-Janak-Williams [5], von Barth-Hedin [6], Vosko-Wilk-Nusair [7], Generalized Gradient Approximation 91 [8], Perdew-Burke-Ernzerhof [9].

## How to introduce AkaiKKR

- [Build with Intel compiler on Linux](./md_en/linux_intel_en.md)

- [Build with gfortran on Linux](./md_en/linux_gfortran_en.md)

- [Build with Intel compiler on Mac](./md_en/mac_intel_en.md)

- [Build with gfortran on Mac](./md_en/mac_gfortran_en.md)

- [Build with WSL on Windows](./md_en/wsl_en.md)

## Usage

- [Input](./md_en/input_en.md)

- [Output](./md_en/output_en.md)

- [DOS calculation tutorial](./md_en/tutorial_DOS_en.md)

## References （PDF）

- [KKR method (AkaiKKR Tutorial Courses 2022/11/17) (in Japanese)](./pdf/AkaiKKR_RIST2022_8jpn.pdf)

- [KKR Green functional method (AkaiKKR Tutorial Courses 2022/11/17) (in Japanese)](./pdf/beginner2022_5jpn.pdf)

- [Band calculation by using KKR Green functional method (in Japanese, external link)](http://kkr.issp.u-tokyo.ac.jp/jp/document/akaikkr_j.pdf)

- [Notes on the use of Machikaneyama2000 (in Japanese, external link)](http://kkr.issp.u-tokyo.ac.jp/jp/document/machikaneyama2000_memo.pdf)

- [Korringa-Kohn-Rostoker Method (external link)](http://kkr.issp.u-tokyo.ac.jp/jp/document/kkrnote.pdf)

## References

[1] J. Korringa, Physica, **13** (1947) 3

[2] W. Kohn and N. Rostoker, Phys. Rev., **94** (1954) 1111

[3] P. Soven, Phys. Rev., **156** (1967) 809

[4] H. Ehrenreich and L. M. Schwartz, in Solid State Physics, Vol. 31, edited by H. Ehrenreich, F. Seitz, and D. Turnbull (Academic,  New York, 1976)

[5] V. L. Moruzzi, A. R. Williams, and J. F. Janak, Phys. Rev. B, **15** (1977) 2854 

[6] U. von Barth and L. Hedin, J. Phys. C: Solid State Phys., **5** (1972) 1629

[7] S. H. Vosko, L. Wilk and M. Nusair, Can. J. Phys., **58** (1980) 80

[8] J. P. Perdew, J. A. Chevary, S. H. Vosko, K. A. Jackson, M. R. Pederson, D. J. Singh, and C. Fiolhais,  Phys. Rev. B, **46** (1992) 6671

[9] J. P. Perdew, K. Burke, and M. Ernzerhof, Phys. Rev. Lett., **77** (1996) 3865

## Releases

- AkaiKKR Latest version (released on 2024/9/26)

- GPU (Nvidia) compatible version (released on 2024/9/26)

- [Release Log](./md_en/release_log_en.md)
