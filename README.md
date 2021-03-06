# MolEV
[![Header](https://github.com/CondaPereira/MolEV/blob/main/images/1.png "Header")](https://some-url.dev/)
--------------------------------------------------------------------------------
As follow is the work of team VE_CPU-iDEC this year:

- [MolEV](#molev)
	- [1.Micromolecular Model Setup](#1micromolecular-model-setup)
		- [1.Way to optimize our micromolcules](#1way-to-optimize-our-micromolcules)
			- [Notice:](#notice)
		- [2.QED function improvement](#2qed-function-improvement)
	- [2.Protein Model Setup](#2protein-model-setup)
	- [3.Work Timeline](#3work-timeline)

## 1.Micromolecular Model Setup  

Our model focuses on data extraction of three sets of data: the sum of bond lengths of molecules, the angle between two atoms, and the diagonal of parallelograms. The molecular information mentioned above is all in three dimensions, which can improve our docking model to some extent. In addition, the molecular 3D model we rendered is supported by blender.After counting these three sets of data we will convert them into HSV plots by a certain formula instead of RGB, and according to a lot of research, HSV is better than RGB in data science applications.  
<div align=center>
<img src="https://github.com/CondaPereira/MolEV/blob/main/images/molecule1.png" width="750">
</div>  

### 1.Way to optimize our micromolcules  
We will develop a deep learning based molecule generation framework and compare it with the optimized small molecule structures from the other two approaches and measure the accuracy of our model by this criterion, now we have mainly optimized the small molecule bulk structure of xtb at GFN2-xtb level and bulk small molecule optimization under the MMFF force field of RDkit, the model ConfEVG is still in the development stage and will be updated at a later stage.  
```ruby
#!/bin/bash

for ((i=1; i<=997; i++))
do
mkdir test_$i
mv test_$i.sdf /path/to/test_$i.sdf
done
```
#### Notice:

Of course, our model also encounters special cases, such as the following molecule with a ternary ring, in which case the model generates certain paradoxes in the theory, so we choose the middle atom Atom(Mid) among every three atoms as the vertex and create a spatial 3D vector with the two surrounding atoms.
<div align=center>
<img src="https://github.com/CondaPereira/MolEV/blob/main/images/rings.png" width="600">
</div>
The above is the optimization of the set of molecules that have not undergone high throughput screening. After the DDI design with MolEV, we will extract the ligand conformations with excellent scores and use quantum calculations to optimize their bond lengths for the next step of more specific quantum chemical calculations and calculate their physicochemical properties such as spectra.  
<div align=center>
<img src="https://github.com/CondaPereira/MolEV/blob/main/images/circuit.png" width="750">
</div>  

### 2.QED function improvement  

In the past QED function, the following indicators were used to fit the function, but of course the following indicators all conform to the form of asymmetric functions, showing specific distribution curves: molecular weight (MW), octanol-water distribution coefficient (ALOGP), number of hydrogen bond donors (HBD), number of hydrogen bond acceptors (HBA), molecular polar surface area (PSA), number of rotatable bonds (ROTB), number of aromatic rings (AROM), number of structural cues (ALERTS), to which we propose to add the solubility term (logP), which plays an important role in assessing the drug-forming properties of small molecules.  
<div align=center>
<img src="https://github.com/CondaPereira/MolEV/blob/main/images/CPDN.png" width="750">
</div>
And since ClogP satisfies the asymmetric distribution, it is consistent with the ADS fitting function given in the literature as follows.  

<p align="center">
<img src="https://latex.codecogs.com/svg.latex?\Large&space;d(x)=a+\frac{b}{1+exp(-\frac{x-c-\frac{d}{2}}{e})}\cdot[1-\frac{1}{1+exp(-\frac{x-c-\frac{d}{2}}{f})}]" title="\Large d(x)=a+\frac{b}{1+exp(-\frac{x-c-\frac{d}{2}}{e})}\cdot[1-\frac{1}{1+exp(-\frac{x-c-\frac{d}{2}}{f})}]" />
</p>

## 2.Protein Model Setup
The protein-based model is still under development, and the dataset we use is mainly from PDBbind and Uniprot, after which we will also extract the 3D information from the dataset for the target information as input to our model.  
PDBbind link: http://www.pdbbind.org.cn/quickpdb.php?quickpdb=5ho7  
Uniprot link: https://www.uniprot.org/uniprot/?query=Human&sort=score  

## 3.Work Timeline
