<!-- Section 1: Logo and short code description-->  <!--  -->
  <h2 align="center">Lavielle et al., 2025,  -</h2>  <!-- Header tag -->
  <h3 align="center">PV Decision Making task</h3>  <!-- Header tag -->
  
  <p align="center">
   The PV Decision Making task is visual-guided bilateral choice task in an automated operant chamber system, allowing precise time framing of the perceptual decision-making processes, to determine the activity of PVIs in the central medial striatum (CMS) during decision-making.
    <br />
    <!-- TODO: change to the article link -->
    <a href="https://github.com/Burguiere-Lab/PV_Decision_Making"><strong> Link to article -TODO»</strong></a>
    <br />
  </p>
</div>

## Table of Contents 

- [1 System Requirements](#1-system-requirements)
- [2 Installation Guide](#2-installation-guide)
- [3 Description of Code's Functionality](#3-description-of-codes-functionality)
- [4 Instructions of Use](#4-instructions-of-use)
- [5 Citation](#5-citation)
- [6 License](#6-license)

## 1 System Requirements
* <b> MATLAB version: </b> The code was developped using Matlab R2017b.
* <b> Operating System: </b> The code was developped and tested under Windows 10.
* <b> MATLAB Toolboxes: </b> None
* <b> Arduino IDE version 1.8.8 </b>
* <b> Arduino IDE libraries: </b>
  Bridge (1.7.0), Esplora (1.0.4), Ethernet (2.0.0), Firmata (2.5.8), GSM (1.0.6), Keyboard (1.0.2), LiquidCrystal (1.0.7), Mouse (1.0.1)
  Robot Control (1.0.4), Robot IR Remote (2.0.0), Robot Motor (1.0.3), SD (1.2.3), Servo (1.1.3), SpacebrewYun (1.0.1), Stepper (1.1.3),
  Temboo (1.2.1), TFT (1.0.6), WiFi (1.2.7), WiFi101 (0.14.3), Adafruit GFX Library (1.2.5), Adafruit ILI9341 (1.0.12), Adafruit Motor Shield library (1.0.0),
  Adafruit Motor Shield V2 Library (1.0.5), Adafruit NeoMatrix (1.1.2), Adafruit NeoPixel (1.1.6), Adafruit SHARP Memory Display (1.0.6), Adafruit TFTLCD Library (1.0.2),
  CapacitiveSensor (0.5.1), FastCapacitiveSensor (1.0.6), Adafruit Circuit Playground (1.8.1).

<div align="right">[ <a href="#readme-top">↑ Back to top ↑</a> ]</div>

## 2 Installation Guide
<ol>
  <li> <a href="https://docs.github.com/fr/repositories/creating-and-managing-repositories/cloning-a-repository"> <strong> Clone </strong> </a> the repository to your local machine:
    <pre><code>git clone https://github.com/Burguiere-Lab/PV_Decision_Making</code></pre>
  </li>
  <li>Navigate to the cloned directory:
    <pre><code>cd PV_Decision_Making</code></pre>
  </li>
  <li> Add the project folder to your MATLAB path. You can do this in two ways:</li>

<h5>Using the MATLAB Command Window</h5>
    <ul>
        <li>Open MATLAB.</li>
        <li>In the Command Window, type the following command, replacing <code>yourpath</code> with the path to your project:
            <pre><code>addpath('yourpath');
savepath;</code></pre> </li>
    </ul>
<h5>Using the MATLAB Set Path Dialog</h5>
    <ul>
        <li>Open MATLAB.</li>
        <li>On the Home tab, in the Environment section, click Set Path.</li>
        <li>Click Add with Subfolders.</li>
        <li>Browse to the project folder and click OK.</li>
        <li>Click Save and then Close to save the changes.</li>
    </ul>
    <li> Install the Arduino IDE from the Arduino oficial website 
      <h5>Install the libraries using the Library Manager (recommended)</h5>
    <ul>
        <li> Open the Arduino IDE. </li>
         <li> Go to Tools > Manage Libraries... or click the Library Manager icon. </li>
         <li> In the Library Manager, search for the desired library. </li>
         <li> Click Install next to the library name. </li>
         </ul>
  </li>
</ol>
Typical install time:  20 min.
<div align="right">[ <a href="#readme-top">↑ Back to top ↑</a> ]</div>

## 3 Description of Code's Functionality

![Dependency Chart](/Flowcharts/DependencyChart.png)

<br> &rarr;  Please refer to the <b> flowcharts diagrams </b>  [folder](https://github.com/Burguiere-Lab/PV_Decision_Making/tree/main/Flowcharts) as it provides a detailed schematic description of the code's workflow. The complete description can be found in the Methods section.
<br> &diams; For more detailed information, users can refer to the in-code comments within the script and its functions.
The core functionality of the main script:
### INPUT 
#### EXCEL Configuration and initialization files
*  `config_ordi_4.xlsx ` - Configuration file of the experiment:  Defines the COMs establishing the USB connection between the computer and the Arduino Mega micro controller. Defines the pins on the Arduino Mega board associated with each variable.  
Defines the COMs establishing the USB connection between the computer and the Arduino Mega micro controller 
Defines the pins on the Arduino Mega board associated with each variable  
### Graphical User Interface
* `launcher.m` - First function that is called when ‘run’ is run, generates the launching window of the GUI
* `WiringConfig.m` - Converts and loads the information from the onfig_ordi_4.xlsx sheet into Matlab 
* `TaskParameters.m` - Defines the details to choose from in the Task Parameters tab in the launcher window 
* `MonitoringWindowGeneration.m` - Generates the monitoring window that allows real time tracking of the animals in the BEATbox 
* `MonitoringWindowRefreshDecisionPV.m` - Allows to update the Monitoring window in the Decision PV task to display the last actions in the task  
* `DialogInterface.m`- Generates the Dialog Interface that allows to see the animal information and control the task remotely 
* `DialogInterfaceSave.m` - Allows to save the changes made in the Dialog Interface  
### Main Files
* `luminance.m` - Main script for the box management. It first declares all the needed variables and initiates the dialog with the Arduinos Megas. It sequentially reads inputs from the BEATbox (getState.m), and manages outputs to the boxes accordingly (outputmanagement.m).  
* `getState.m` - This function gathers the state of each BEATbox to know which input hardware is on or off and thus know what the mouse is currently doing.
* `outputmanagement.m` - Manages the outputs in the  BEATboxes according to their states.
### Task: Decision PV
* `DecisionPVTask.m` - Function called in luminance. Depending on the value of box.Stage, this function redirects the task towards the appropriate stage of the task. 
* `DecisionPVStage1.m` - Training Stage 1: During this stage, the mouse learns that it can get pellets at the food dispenser. For that, pellets are automatically distributed every 60 seconds after the mouse nose-pokes (except for the 1st one). 
* `DecisionPVStage2.m` - Training Stage 2: During this stage, the mouse associates nose-poking in the food dispenser with food delivery. For each nose-poke in the food-well, a pellet is distributed.
![Stage1-2](/Flowcharts/1.png)
* `DecisionPVStage3.m` - Training Stage 3: During this stage, the mouse learns to associate the side nose-pokes next to the screen with food delivery. Each time the mouse breaks the IR beams in one of the side nose-pokes, the screens start blinking and a pellet is delivered in the food-well. The mouse has 15 seconds to retrieve the pellet and to validate the trial. Otherwise, the trial countdown is reset.
![Stage3](/Flowcharts/2.png)
* `DecisionPVStage5.m` - Stage 5: The task in which the animal makes bilateral choices based on a pair of visual stimuli that are presented during the cross of the tunnel in the BEATbox.
![Stage5](/Flowcharts/3.png)
* `DecisionPVStage4.m` - Stage 4: During this stage the animal receives bilateral optogenetic stimulation in stimulation trials
![Stage4](/Flowcharts/4.png)
* `tracesequence.m` - Psydo-randomized sequence of the stimuli presented to the animal, generated from Markov Chain - approximate algorithm.
### ARDUINO
* `Serial_Communication_Arduino_Mega` – Script for the Arduino mega board managing the input and output of the Arduino Unos in the BEATbox, and communicating wth Matlab.  
* `code_mangeoire_interruption` – Script for the Arduino Uno board managing the input and output in the food dispenser.  
* `Stimuli_Tasks_Arduino_Uno` - Script for the Arduino Uno board managing the input and output in the screen displaying the visual stimulus to the animal. 

Note: The Arduino scripts need to be manually uploaded to the Arduino boards via USB connection before the task can be run.  

### OUTPUT
A Monitoring Window and a Dialog interface will appear. The Monitoring Window provides real time tracking information about each mouse. The time spent in the task, the number of food rewards collected both in the last 24h and in total, the last action in the BEATbox and the according timestamp, and the Log of the animal’s behaviour in the task. The Dialog Interface allows to see the animal information, to reset the screen in the task as well as stop the task for one animal. All the data will be stored in the structure box in a .m file containing information about the animal identity, the task configuration, as well as information about each individual trial for each animal in the structure box.Data (stage, trial number, difficulty level, timestamps and names of all actions by the mouse, type of trial, decision-making duration, response time). 

<div align="right">[ <a href="#readme-top">↑ Back to top ↑</a> ]</div>

## 4 Instructions for Use

Ensure you added the project folder to your MATLAB path and set it as the current folder.  

Run the ‘run’ script in Matlab in the BEATbox_Code to use_fiber folder  

The graphical user interface (GUI) will open from the script ‘launcher’  

Select which BEATboxes you would like to run by ticking the boxes in the GUI 

Select the path in which you would like to store your data

In the tab ‘Wiring configuration’ you can load the excel configuration file config_ordi_4.xlsx     

In the tab ‘Task parameters’ enter the animal information and select the task configuration you would like to run  

Click Run in the GUI to initialize the communication between the Arduino Mega micro controller and Matlab and to start the task 


<div align="right">[ <a href="#readme-top">↑ Back to top ↑</a> ]</div>

## 5 Citation
If you use this code or data we kindly ask you to cite our work. 

- <b> Data: </b>
> (APA style) TODO

- <b> Article: </b> Lavielle et al: [DOI link](https://github.com/Burguiere-Lab/PV_Decision_Making)
> @article{Lavielle2025,
        title = {TODO},
        author = {TODO},
        journal = {TODO},
        year = {2025},
        url = { TODO }}


<div align="right">[ <a href="#readme-top">↑ Back to top ↑</a> ]</div>

## 6 License
todo
## 7 Credits
This code is inspired in the work done by Marine Euvrad and Guillaume Penderia (add citation)
Contributors: Oriana Lavielle and Anne Lorenz
