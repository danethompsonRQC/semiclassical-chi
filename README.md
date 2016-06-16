# semiclassical-chi
Python code for automating a semi-classical chi calculation through HFSS simulations.  
This code calculates the chi frequency shift of a qubit in the presence of a coupled readout resonator.  
The initial code for this was written by Michael Scheer in summer 2015.

## Prerequisites
1. Windows 7, 8.1, 10, Server2008, or Server2012 64-bit computer. A linux install is also possible, but is not covered here.
2. HFSS 2016 (17.1) installation on the local machine (this version is current as of 6/15/2016)
  + Copy HFSS 17.1 (ELECTRONICS_171_WINX64.zip) to your local disk from: `\\10.1.10.5\INSTALLS\ANSYS\V2016\`
    + This may require setting up the INSTALLS folder as a network location
    + `Start > Computer > Right click in middle of window > Add a Network Location > Next > Choose custom network location > Next > \\10.1.10.5\INSTALLS > Next > Next > Finish`
    + Browse to `Ansys\V2016` to find the `ELECTRONICS_171_WINX64.zip` file and copy to your local disk (this might take 10-15 minutes)
  + Use winzip or 7zip to extract the .zip file to a folder
  + Open the extracted folder and execute `autorun.exe` to install
  + During install, set the license server to `10.1.10.5`
3. An HFSS license must be available to run the code.  As of June 2016, we have 7 GUI licenses and 6 solvers.
4. Git installation on the local machine
  + Download Git from `https://git-scm.com/downloads`. Choose `Windows` or `Download for Windows`.
  + Install Git by executing the installer.  Choose `Use Git from Bash only` and defaults for the rest

## Adding the Git Repository   
1. In Windows, create a directory location where the Git repository should be created, for example `C:/REPOS/`
2. Open Git Bash
3. In Git Bash, change to the directory created in step 1: `cd C:/REPOS/`
4. Type: `git clone git@github.com:rigetticomputing/semiclassical_chi.git`
    + Now you have the repository containing all parts of the semiclassical_chi project.

## HFSS Project Requirements
  Here are the HFSS project/design requirements:
+ The user has created a driven design in HFSS which is currently open
+ The design's name is of the form `1_Name` where Name can be any desired string
+ The design has one or two ports which are rectangles
+ The first port (alphabetically by the name of the object representing the port) is the qubit port
+ The sides of the ports are parallel to the x,y,z axes.
+ The variable names L_qubit and L_resonator are unused.

The HFSS project should have one of the following configurations:
  1. Two port model:
    + Port1: Transmon qubit junction location (the name must be first alphabetically)
    + Port2: Lumped inductance for the linear readout resonator represented by a rectangular lumped port rather than by physical geometry such as a meander or spiral
  2. One port model:
    + Port1: Transmon qubit junction location (the name must be first alphabetically)

## Creating Button Push Execution in HFSS
  1. Open HFSS
  2. Go to Tools>External Tools
  3. Add a new script
    + Menu text: Classical Chi
    + Command: C:\Program Files\AnsysEM\AnsysEM17.1\Win64\common\IronPython\ipy64.exe
    + Arguments: ClassicalChi.py
    + Initial directory: C:\REPOS\semiclassical_chi\Python (assuming you put the semiclassical_chi code in C:\REPOS\)
  4. Go to Tools>Customize
  5. In Toolbars click new and create a new toolbar. Drag the toolbar to the top of the HFSS window.
  6. In Categories, scroll all the way to the bottom and click “User Tools”
  7. The first user tool on the right should correspond to Classical Chi. Grab it and pull it to the HFSS toolbar you just made at the top of the screen.

Now clicking the button you just created should run the python code!

## Running From the Command Line
+ Navigate into the folder in Git Bash and run it there
+ Type “cd ~/Documents/BruneRepo/HFSS/Python”
+ Type “C:\Program Files\AnsysEM\AnsysEM16.0\Win64\common\IronPython\ipy64.exe ClassicalChi.py”




