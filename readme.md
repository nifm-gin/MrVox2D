# README #

MrVox is a toolkit writen in Matlab to simulate the Magnetic Resonance 
signal


### What is MrVox for? ###

* MrVox is for simulating the MR complex signal given:
    1. a voxel with a user-defined microstructure
    2. a MR pulse sequence  
* MrVox is designed with versatility in mind and user can control:
    1. the geometry of the voxel (size, number of blood vessels and cells, their size, their spacing, etc.)
    2. the MR-related properties of the different compartments (T1, T2, M0, susceptibility)
    3. the magnetic field and its variation over the voxel dimension
    4. the water diffusion  
* MrVox is particularly designed to generate dictionaries of MR signals with varying input properties (blood volume, vessel size). 
For example, it has been used succesfully in the vascluar fingerprinting framework 
[(Christen et al. NeuroImage 20014)](http://www.sciencedirect.com/science/article/pii/S1053811913012019)
* **Specifically**: The voxel is considered as a 2D plane and the magnetic inclusions (e.g. vessels) 
are disks randomly spread in the 2D plane. Voxel and sequence parameters are defined in a text file.
MR sequence is passed as a function of the simulator.

### How do I get set up? ###

* Add mrvox/ to your matlab path
* run example to check if everything is working:
```
#!matlab
>>example
```
* open example.m and VoxelSim2D_do_one to start tinkering your own stuff
* Examples of configuration files for the voxel and MR sequences can be found in config/.
* The two main use cases are:

    * **Single/simple use**:
```
#!matlab
[Sa, Sphi] = VoxelSim2D_do_one('config/voxpar_single.txt','config/seqpar_GESFIDE.txt')
```

* or:
    * **Dictionary use**: Any parameters X in the structure Model.phy, Model.vox or Model.geo with size(X,2) > 1 will be considered for dictionary building.
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

* Through the issues tracker 

### Who do I talk to? ###

* Nicolas Pannetier, Thomas Christen