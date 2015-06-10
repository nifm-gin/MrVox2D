# README #

MrVox2D is a toolkit writen in Matlab to simulate the Magnetic Resonance 
signal

### What is MrVox2D for? ###

* MrVox2D is for simulating the MR complex signal given:
    1. a voxel with a user-defined microstructure
    2. a MR pulse sequence  
* MrVox is designed with versatility in mind and user can control:
    1. the geometry of the voxel (size, number of blood vessels and cells, their size, their spacing, etc.)
    2. the MR-related properties of the different compartments (T1, T2, M0, susceptibility)
    3. the magnetic field and its variation over the voxel dimension
    4. the water diffusion  
* MrVox2D is particularly designed to generate dictionaries of MR signals with varying input properties (blood volume, vessel size). 
For example, it has been used succesfully in the vascluar fingerprinting framework 
[(Christen et al. NeuroImage 20014)](http://www.sciencedirect.com/science/article/pii/S1053811913012019)
* **Specifically**: The voxel is considered as a 2D plane and the magnetic inclusions (e.g. vessels) are disks randomly spread in this 2D plane. Voxel and sequence parameters are defined in a text file. MR sequence is passed as a function of the simulator. Perturbation of the magnetic field by the susceptibility inclusions are considered. Diffusion is modeled by convolution of a gaussian kernel and can be hindered to compartment walls. Even though the simulation is 2D, the MR signal is similar to the one obtained in a 3D voxel with isotropic vessel orientation when the number of vessels is "high enough" [(Pannetier et al. Plos. 2014)](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0057636).
* **Limitations**: The simulation of the proton diffusion is modeled by a convolution kernel and the computation is performed in the Fourier domain. The related aliasing effect have some consequences: 
    1. The geometry lattice must be periodic
    2. When applying gradient, their strenght must be such that the dephasing over the voxel extend during the simulation step time dt must be modulo 2 x pi.
 
### How do I get set up? ###

* Add mrvox/ to your matlab path
* Check out the example in example.m
* Start tinkering with your own stuff
* Examples of configuration files for the voxel and MR sequences can be found in config/.
* The two main use cases are:

    * **Single/simple use**: to run the simulator on a voxel/sequence:
```
#!matlab
[Sa, Sphi] = VoxelSim2D_do_one('config/voxpar_single.txt','config/seqpar_GESFIDE.txt')
```

* or:
    * **Dictionary use**: to generate a dictionary of MR signal by varying any parameters defined as an array in the Model structure of the configuration file (Model.phy, Model.vox or Model.geo):
```
#!matlab
Dico = GenLookUp2D('config/voxpar_dico.txt','config/seqpar_GESFIDE.txt')
```

* **Deployment**: Dictionary generation is highly parrallelizable and the code
provides a support for using Matlab Discributed Computing Server (MDCS). Server
configuration must be defined in the configuration file (see config/cluster_info.txt for an example).
The example file is compatible with Matlab R2011b and the code will likely need an update
to be use with newer version. The code can also be compiled using Matlab compiler and deployed with another scheduler


### Contribution guidelines ###

Through the issues tracker 

### Who do I talk to? ###

Nicolas Pannetier, UCSF - VAMC SF
Norbert Schuff, UCSF - VAMC SF

### License ###

MrVox2D is licensed under the terms of the BSD license. Please see the License file in the repository