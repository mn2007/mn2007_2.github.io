---
layout: default_en
title: output_en
permalink: /output_en
---

# Notes on AkaiKKR output files

## Composition of output files
### Part1. Calculation parameters and loaded data

An output is displayed on the screen or in the saved file. 
```start
  6-Nov-2022
    22:59:50
    meshr   mse    ng   mxl
      400    35    21     3
```
First, the date and time are displayed. These represent the start time of the calculation.
The following means: 
* meshr : mesh number of coordinates for radial direction
* mse : energy mesh number of complex integration
* ng : degree of Chebyshev expansion
* mxl : maximum amount of significant scattering angular momentum. The unit is $\hbar$.

Next, Input data is displayed. This data and the meaning of keywords are explained in detail on the notes on input files. Please read the link below.

[Notes on AkaiKKR input files](../input_en/input.md_en)

```start
   data read in
   go=go   file=data/fe                                                         
   brvtyp=bcc     a=  5.27000  c/a= 0.00000  b/a= 0.00000
   alpha=  0.0  beta=  0.0  gamma=  0.0
   edelt= 1.0E-03  ewidth=  1.000  reltyp=nrl    sdftyp=mjw      
   magtyp=mag     record=2nd   outtyp=update  bzqlty=4       
   maxitr= 50  pmix= 0.02300  mixtyp=tchb-brydn
   ntyp=  1  natm=  1  ncmpx=  1
```

### Part2. Complex energy paths
After that, the complex energy paths are displayed as a series of n (ewidth, edelt). As we wrote in [Notes on AkaiKKR input files](../input_en/input_en.md), it is closely related to the success of the calculation that these values are appropriate.

To check the validity of the integration range, it is good to compare the value of ewidth and the energies of core states (the values of the core level (spin-up) and the core level (spin-down)).
Specifically, we need to confirm that the difference between the output Fermi energy and the shallow core state energy is sufficiently (greater than 0.1 Ry) greater than the value of ewidth. If we find that this is not true, or that the convergence is strange, we should confirm it by plotting the DOS.

```start
   complex energy mesh
   1( -1.0000, 0.0000)   2( -0.9998, 0.0027)   3( -0.9990, 0.0062) 
   4( -0.9971, 0.0107)   5( -0.9933, 0.0163)   6( -0.9862, 0.0234) 
   7( -0.9738, 0.0319)   8( -0.9535, 0.0421)   9( -0.9220, 0.0536) 
  10( -0.8757, 0.0660)  11( -0.8117, 0.0782)  12( -0.7292, 0.0889) 
  13( -0.6307, 0.0965)  14( -0.5224, 0.0999)  15( -0.4130, 0.0985) 
  16( -0.3115, 0.0926)  17( -0.2245, 0.0835)  18( -0.1553, 0.0724) 
  19( -0.1037, 0.0610)  20( -0.0671, 0.0500)  21( -0.0424, 0.0403) 
  22( -0.0262, 0.0320)  23( -0.0160, 0.0251)  24( -0.0096, 0.0195) 
  25( -0.0057, 0.0151)  26( -0.0034, 0.0116)  27( -0.0020, 0.0089) 
  28( -0.0012, 0.0069)  29( -0.0007, 0.0052)  30( -0.0004, 0.0040) 
  31( -0.0002, 0.0031)  32( -0.0001, 0.0023)  33( -0.0001, 0.0018) 
  34( -0.0000, 0.0014)  35( -0.0000, 0.0010) 
```

### Part3. Information on potential data storage files and lattices

There is no file specified in the current calculation, so the new file is created.

```start
   file to be accessed=data/fe                  
   created
```

In the next part, the information of the crystal is summarized. 

```start
   lattice constant
   bravais=bcc   a=  5.27000   c/a= 1.0000   b/a= 1.0000
   alpha=  90.00   beta=  90.00   gamma=  90.00
```

The unit cell volume and the filling volume by muffin tin (MT) sphere, which is 68%, are displayed. 

```start
   unit cell volume=    73.18159(a.u.)
   volume filling=  68.0%
```

The following are primitive translation vectors. The unit is a.

```start
   primitive translation vectors (in units of a)
   a=( -0.50000  0.50000  0.50000)
   b=(  0.50000 -0.50000  0.50000)
   c=(  0.50000  0.50000 -0.50000)
```

ga, gb, and gc represent reciprocal lattice vectors. The unit is 2π/a.

```start
   reciprocal lattice vectors (in units of 2*pi/a)
   ga=(  0.00000  1.00000  1.00000)
   gb=(  1.00000  0.00000  1.00000)
   gc=(  1.00000  1.00000  0.00000)
```

### Part4. Information on atoms occupying each site, lattice symmetry, number of k points

At first, we make the "types" of sites. The position of the following type is occupied 100% by iron. Details are written in the notes on Input.

[Notes on AkaiKKR input files](../input_en/input.md_en)

```start
type of site
   type=Fe        rmt= 0.43301 field=  0.000   lmxtyp=  2
                  component= 1  anclr=  26.00  conc= 1.0000
```

Next, the position of the type, in other words, the atomic position, is displayed.

```start
   atoms in the unit cell
   position=   0.00000000   0.00000000   0.00000000  type=Fe
```
The information of the energy window for the Chebyshev expansion is given.
* ew : the center of the energy window
* ez : the width of the energy window

```start
 ***wrn in spmain...eof detected; data generated
 ***msg in spmain...new ew, ez generated
   ew=   0.19997  ez=   1.25000

   preta= 0.35542  eta= 0.35542
```

#### About symmetrical manipulation

Symmetric manipulation allowed for given atomic coordinates **symop** is written. Allowed manipulation is represented by 1, forbidden manipulation is represented by 0.
* g : gerade
* u : ungerade
  
**nk** represents the number of k-points in the irreducible zone.
```start
   symop   E  C4*3   C2*3  C4^3*3   C3*4    C3^2*4      C2'*6
     g     1  1 1 1  1 1 1  1 1 1  1 1 1 1  1 1 1 1  1 1 1 1 1 1
     u     1  1 1 1  1 1 1  1 1 1  1 1 1 1  1 1 1 1  1 1 1 1 1 1

   last=  243   np=  19   ngpt= 273   nrpt= 169   nk=     29   nd=    1
```

### Part5. Atomic calculations

In the present calculation, the atomic LDA/GGA calculation is performed because the value of the potential energy is not given. The number of iterations is displayed. The following shows that the calculation converges in 15 iterations.

```start
 atomic potential generated

   itr=  1      rms error =  0.245
   itr=  2      rms error = -0.412

　　　　　　．．．

   itr= 15      rms error = -6.237
   interval= 15     cpu time=      0.00 sec
   nuclear charge=26.00
```
The calculated energy levels are written in **energy**. The unit is Ry.

```start
         nl      cnf         energy
    -----------------------------------
         1s     2.000       -508.5203
         2s     2.000        -59.2074
         2p     6.000        -51.1807
         3s     2.000         -6.8027
         3p     6.000         -4.4563
         3d     6.000         -0.6696
         4s     2.000         -0.4930
```

### Part6. Other Information

```start
   record 1 will be overlaied by input and
   record 2 will be replaced by new output.

   core configuration for Z= 26
   state  1s 2s 2p 3s 3p 3d 4s 4p 4d 5s 5p 4f 5d 6s 6p 5f 6d 7s
    up     1  1  3  1  3  0  0  0  0  0  0  0  0  0  0  0  0  0
   down  1  1  3  1  3  0  0  0  0  0  0  0  0  0  0  0  0  0
```
In **record1**, the record is overlaid with the input potential. In the second record, it is replaced by the newly calculated potential. 
The structure of a potential file contains two records consisting of binary data.
* record1 ： the one before data
* record2 ： the latest data

These are corresponding to the record keywords in Input file, so we quote the explanation in Input file as follows: 
> **record**  is the keyword for the use of potential data. 
> Two sets of data (the latest results and the previous results) are stored so that we do not lose results in case of abnormal termination. 
> * init : New potential data (Use potential data calculated from given atomic positions)
> * 2nd : Continue calculations from the latest potential data
> * 1st : Continue calculations from the previous data

The description followed by **core configuration** means the core-level occupancy numbers.

### Part7. Iterative calculation start
```start
 ***** self-consistent iteration starts *****
       Fe
   itr=  1 neu=   -2.5047  moment=  4.0909  te=  -2523.19969054  err=  0.502
   itr=  2 neu=   -1.6328  moment=  2.5475  te=  -2522.86071488  err= -0.371
   itr=  3 neu=   -0.3261  moment=  2.6308  te=  -2522.80866273  err= -0.443
   itr=  4 neu=    0.0541  moment=  2.5226  te=  -2522.80177581  err= -0.367
   itr=  5 neu=    0.0943  moment=  2.5160  te=  -2522.80050661  err= -0.335
   itr=  6 neu=    0.0459  moment=  2.4553  te=  -2522.80806361  err= -0.454
   itr=  7 neu=   -0.1653  moment=  2.2229  te=  -2522.81662663  err= -0.640
   itr=  8 neu=   -0.3538  moment=  1.9560  te=  -2522.82374971  err= -1.132
```

* itr : iteration number
* neu : total number of electron in the system. If it is zero, charge neutrality is maintained.
* moment : magnetic moment of the system（$µ_B$）
* te : total energy (Ry)
* err : the maximum number of the norm of the difference between the input potential and the output potential. It is represented as a logarithmic number. If it grows as a negative number, the error is getting smaller. 

### Part8. Convergence of iteration

```start
　 itr= 46 neu=   -0.0001  moment=  2.1598  te=  -2522.81762151  err= -5.193
   itr= 47 neu=   -0.0001  moment=  2.1598  te=  -2522.81762150  err= -5.557
   itr= 48 neu=   -0.0001  moment=  2.1598  te=  -2522.81762150  err= -6.104
   interval= 48     cpu time=      0.31 sec
   sdftyp=mjw     reltyp=nrl     dmpc= 0.10000
       Fe
   itr= 48  neu -0.0001  chr,spn   8.0000   2.1598  intc,ints  1.0307 -0.0270
   rms err= -6.140 -6.104
   ef=   0.7686596   0.7779665  def=     5.0213887    17.8605662
   band energy=    4.763028241   total energy=  -2522.817621496
   magnetization=   2.3210 T
```
This calculation converged in 48 iterations as it is in **interval**. It finishes correctly when the value of err is less than the set error value. If err is not small enough after the maximum number (maxiter) of iterations, the calculation is aborted.

* intc, ints : electric number and spin moment accumulated in the lattice gap
* ef : Fermi level (up, down)
* def : density of states in the Fermi energy
* total energy : total energy (Ry)

**ef** has two values because it depends on the spin direction. The energy zero points are different between up and down because we use the flat part of the muffin tin as the zero point.

### Part9. Local information for each site
```start
　                                      *** type-Fe     Fe (z= 26.0) ***
   core charge in the muffin-tin sphere =17.9774112
   valence charge in the cell (spin up  ) =     0.19393(s)   0.19656(p)   4.19816(d)
   valence charge in the cell (spin down) =     0.20117(s)   0.22849(p)   1.97357(d)
   total charge=  24.96929   valence charge (up/down)=   4.58865   2.40323
   spin moment=   2.18542  orbital moment=   0.00000
   orbital current (up/down)=   0.00000   0.00000
   core level  (spin up  )
      -507.0825055 Ry(1s)       -57.8242188 Ry(2s)       -49.7860958 Ry(2p) 
        -5.4714121 Ry(3s)        -3.1285211 Ry(3p) 
   core level  (spin down)
      -507.0728003 Ry(1s)       -57.7222519 Ry(2s)       -49.7063113 Ry(2p) 
        -5.2798012 Ry(3s)        -2.9425195 Ry(3p) 
```
**valence charge in the cell** represents the angular momentum components of the valence bonds in the muffin tin sphere.

**total charge** does not correspond to 26, the total number of electrons in Fe. This is because electrons accumulate at the lattice gap position.

**valence charge** represents the total number of electrons in the muffin tin sphere.

**spin moment** represents the spin moment in the muffin tin sphere.

### Part10. Hyperfine structure
```start
hyperfine field of Fe
     -274.068 kG (core=  -219.153 kG  valence=   -54.915 kG  orbital=     0.000 kG )
   core contribution
      -18.434 kG(1s)     -491.698 kG(2s)      290.979 kG(3s)
   charge density at the nucleus
       11820.4209 (core=    11814.6730  valence=        5.7479 )
   core contribution
       10701.4235(1s)         972.7172(2s)         140.5324(3s)
```
**hyperfine field** indicates the magnetic field made by the electron at the position of the nucleus. This is the hyperfine field corresponding to the resonance frequencies in NMR etc. and the Mossbauer spectrum. 

**charge density at the nucleus** represents the density of electrons at the position of the atomic nucleus. This corresponds to isomer shifts in NMR etc.

### Part11. Information on calculations
```start
  sbtime report
  routine           1         2         3         4
  count           864       864       864        96
  cpu(sec)       3.60      1.19      1.32      0.13
```
**routine** in sbtime report is the information of specific routines. Time is equal to (real time) x (the number of threads).

```start
 OS: Linux
 Host: ru
 Machine: x86_64
 numcor: 36
 elapsed time         0.38 sec (  9 threads)
```
After displaying the operating system and machine information, the real time of the calculation and the number of threads are displayed.