# Simulations Folder Organisation

## Cases ABL_ NREL5MW
All the cases conducted to test the ABL and multimegawatt turbine simulations in CFDHub

### Caso9
- Functioning precursor case run on CFDHub

### Caso13
- Functioning successor case run on CFDHub

### PrecursorPC
- Trial precursor run on my personal PC to troubleshoot problems with the one run in CFDHub

### SuccessorPC
- Trial successor run on my personal PC run to troubleshoot problems with the one run in CFDHub

### CFD_SIMS
- Excel containing a record of all the simulation data and changes between simulations

### Changes successorPC
- Changes performed to successorPC in order to make it work after the obtained error (attached).

## Cases Mowito (new polars)
All to do with the simulations conducted with the new QBlade polars and Reynolds interpolation

### Cases for GCI
- The three cases (coarse, medium, and fine) that were used to perform the grid convergence index procedure with increasing grid discretization. `Fine_final` is the fine simulation with the ALM nacelle shown in the thesis.

### Cases for video
- Cases run for 5.5 seconds used to obtain video of Q-criterion contours to show in the presentation. Run only 5.5 seconds since it produces a huge amount of data and stopped very often for going over the limit (100GB).

### Fixed_Surge_Sway
- Folder containing the final fixed surge and sway simulations presented in the thesis all with the nacelle implemented with snappyHexMesh.

### Old
- Old trials not of interest.

### Polars
- All to do with the aerodynamic data obtained with Qblade.

### Useful Matlab Scripts:
- **Platform motion**: Script used to calculate the forcing matrix and reduced system properties of the system based on user-defined parameters.
- **Probes_schematic**: Script to create a 3D view of probes location.
- **Residuals**: Script to create trend of residuals (obtained by running `foamLog [simulation log file name]` command in the logs folder of any simulation).
- **Probes Generator**: Script to automatically create the text files for a grid of OpenFOAM probes with user-defined parameters.
- **GCI**: Script to calculate grid convergence index parameters based on simulation data.
- **LES_IQ**: Scripts to calculate LES_IQ criterion based on .csv files obtained with the plotOverLine function of Paraview.

## Cases Mowito (old polars)
All to do with the simulations conducted with the original polars and no Reynolds interpolation. Not recommended to take these as reference. Many things were changed as new simulations were performed. Instead refer to "new polars" folder.

### Experimental Data
- Folder containing the shared experimental data.

### OpenFAST Model_Original
- Folder containing the original OpenFAST model of the Mowito.

### Mowito_sims
- Excel containing a record of all the simulation data and changes between simulations up to `Mowito_Fixed_17 Surge_1 and Sway_1`.

## Cases Sebastiano
Reference cases from Sebastiano.

## Useful Commands
Document with some useful commands to handle simulation runs in CFDHub.

# How to Navigate Simulation Folders (applies to "new polars" folder simulations)
The simulation folders contain all the necessary data to re-run them again in CFDHub and all the data they produced. 

#### Folder Structure
- **0.original**: Contains the initial conditions and boundary conditions for all variables.
- **Constant**: Most important file inside: `turbineArrayProperties`.
- **Time Folder** (normally `18.00006`): Contains the reconstructed processor fields for that time performed with the `reconstructPar -time 18.000006` command.
- **Logs Folder**: Contains all the log files for the simulation. Additionally, it contains another logs folder inside which has all the residuals and trends output by the command `foamLog [logfilename]`.
- **Mowito**: The OpenFAST model.
- **Postprocessing**: Probes and `turbineProperties` folder.
- **System**: Simulation control folder.
- **Tools**: Folder containing the post-processing tools used in the simulations. It is based on the post-processing tool of Sebastiano Stipa with some add-ons and changes implemented by us to adjust to the different simulation type and post-processing techniques used.
-	**a.foam**: file to view the domain in Paraview
-	**Mowito.0.fst**: OpenFAST input file
-	**Mowito.0.out**: OpenFAST output file
-	**Runscript.solve** and **runscript.preprocess**: files used to run the preprocessing stage and solving stages of the run
-	**setup file**
-	**sim.log**: file containing the time taken by the simulation to finish.

# Structure of the Tools folder 
The Tools folder inside each simulation folder is the post-processing tool developed by Sebastiano Stipa and Roberto Pratico for their master thesis. It was subsequently modified by us to add the capability of post-processing laminar uniform inflow simulations with the MoWiTO wind turbine model. It is made up by the sum of all Matlab scripts and functions used to post-process the simulation data and store the outputs (plots, graphs, tables, strucutures…) used later in our thesis. 
**Note**: as of 10/06/24, running the PFTPostProcessing script produces all the simulation data presented in the thesis corresponding to the specific simulation folder in which it is in. 


### Data
- **ExpData**: Matlab structures containing Milan and Oldenburg probes data.
- **PFT**: Folder containing probes and OpenFAST data of the simulation if run with `pisoFoamTurbine` solver.
- **WPS**: Folder containing probes and OpenFAST data of the simulation if run with `windPlantSolver` solver.
### Include
Folder containing all the matlab functions necessary to run the top-folder scripts.

### Postprocessing
#### - **Plots/FAST**: OpenFAST outputs produced by `fastPostProcessing` script.
#### - **Plots/probes**: Outputs produced by `PFTPostProcessing` or `WPSPostProcessing` scripts.
 - **avgTimeHistory**: Instantaneous average velocity within the rotor average vs simulation time.
 - **Comparison**: Percentage gain plots between cases (e.g. sway vs fixed).
 - **Contours**: Instantaneous wind fields.
 - **Correlations**: Cross-correlations of velocity components.
 - **Cross-probes**: Velocity and TI horizontal profiles vs experimental data.
 - **Stream-probes**: Velocity and TI vertical profiles vs experimental data.
 - **RotorAvgs**: Time-average of rotor averaged velocity at the sampled streamwise distances vs experimental data.
 - **Spectra**: Power spectral density of streamwise velocity fluctuations.

### Scripts
- **ABLPostProcessing**: Postprocessing script used for ABL simulations with `ABLSolver` (e.g. Sebastiano’s case16 or caso9).
- **Acquisition**: Script used to acquire the simulation and OpenFAST data and store it in structures and arrays readable by Matlab. Adjusts automatically if `windPlantSolver`, `ABLSolver`, or `pisoFoamTurbine` solver are used.
- **FastPostProcessing**: Script used to produce all the OpenFAST-related outputs.
- **ImagePostProcessing** (not used in our thesis)
- **PFTPostProcessing**: Script used to produce all the outputs in `postprocessing/Plots/Probes` folder if the `pisoFoamTurbine.ALMAdvancedOpenFAST` solver is used.
- **RMS_ERROR**: Script used to calculate all the NRMSE within the rotor area for the simulations conducted and the experimental data.
- **WPSPostProcessing**: script used to produce all the outputs in postprocessing/Plots/Probes folder if the windPlantSolver solver is used.
