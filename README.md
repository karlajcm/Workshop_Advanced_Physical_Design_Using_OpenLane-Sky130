# Workshop_Advanced_Physical_Design_Using_OpenLane-Sky130


# Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK

## SKY130_D1_SK3 - Get familiar to open-source EDA tools

## SKY_L1 - OpenLANE Directory structure in detail

Inside the next path we will find 3 files: skywater-pdk, open-pdks, sky130A. As it’s shown below.

```jsx
$cd /Desktop/work/tools/openlane_working_dir/pdks
```

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled.png)

- skywater-pdk → It has all the files related to the pdk: timing libraries, cell files, etc.
- open-pdks → Foundry files that are not made for Open-EDA Tools. These were processed so that free tools can open them.
- sky130A → It has two folders:
    - libs.ref → Specifically for technology (sky130_fd_sc_hvl, sky130_fd_pr_rf, ect). We will be working specifically with sky130_fd_sc_hd
    - libs.tech → Specifically for tools (klayout, ngspice, netgen, magic, etc)

<aside>
📌 Take care: OpenLane is not a tool, it is a flow which contains many Open-source EDA Tools.

</aside>

---

## SKY_L2 - Design Preparation Step

To launch OpenLane Flow, we have to open a terminal and type the next commands:

```jsx
$cd /Desktop/work/tools/openlane_working_dir/openlane

$docker

$./flow.tcl -interactive
```

Then, OpenLane is launched:

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%201.png)

We will need to input all the packages required:

```jsx
$package require openlane 0.9
```

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%202.png)

In another terminal, we go to the next path:

```jsx
$cd Desktop/work/tools/openlane_working_dir/openlane/designs
```

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%203.png)

We open **picorv32a** file. And we type:

```jsx
$less config.tcl
```

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%204.png)

Later we configure the design in the terminal in which we open OpenLane.

```jsx
$prep -design picorv32a
```

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%205.png)

Here what it’s doing is combining the 2 files (the design and the configuration file). This can be confirmed by going to the path, where a folder called "runs" should appear:

```jsx
$cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a
```

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%206.png)

---

## SKY_L3 - Review files after design prep and run synthesis

Later we open **runs** file. We will find a file with the date on which the commands were run to create the **runs file**.

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%207.png)

Opening the ***date*** file…

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%208.png)

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%209.png)

All folders will be empty except "tmp". If we open it, for example, we can open the file "merged.lef" with…

```jsx
$less merged.lef
```

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2010.png)

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2011.png)

Back in the date folder, we can open **config.tcl**. This file shows which parameters are taken into account for the run.

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2012.png)

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2013.png)

Back in the openlane flow we type:

```jsx
$run_synthesis
```

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2014.png)

---

## SKY_L5 - Steps to characterize synthesis results

Among the things that we can see as a result is.... Chip area.

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2015.png)

In addition, in the statistics we can see... Number of cells and number of flip-flops (sky130_fd_sc_dfxtp_2)

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2016.png)

We can calculate Flop Ratio…

$$
FlopRatio = \frac{No.ofFlipFlops}{No.ofCells}
$$

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2017.png)

Going back to the date folder, we can go to the results folder: "results" and open the "synthesis" folder. There we will find the synthesized netlist. Called... "picorv32a.synthesis.v", where you can see that the abc has done all the mapping.

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2018.png)

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2019.png)

Going back to the date folder, we can enter the reports folder: "reports", and then the "synthesis" folder. We can open the most recent one which will correspond to the "stat report" → "yosys_2.stat.rpt"

```jsx
$less 1-yosys_4.stat.rpt
```

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2020.png)

![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2021.png)

We can also review other reports…

- less opensta.rpt
    
    ![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2022.png)
    
- less opensta_main.timing.rpt
    
    ![Untitled](Day%201%20a881c85ccd0049e892fda7e0c9aaeb3e/Untitled%2023.png)
    

<aside>
💡 Take care: To return to the terminal, after entering the command "less (file)", press the Q key.

</aside>

---
---
# Day 2 - Good floorplan vs bad floorplan and introduction to library cells

## SKY130_D2_SK1 - Chip Floor planning considerations

### SKY_L6 - Steps to run floorplan using OpenLANE

1. After the synthesis…. The next step is Floorplan. In this step we set the die area, the core area, the aspect ratio, the utilization factor; we place the input and output cells, do the power distribution network and macro placement. 
    
    <aside>
    💡 Take care: Standard Cells Placement happens in Placement Stage. Not in Floorplan.
    
    </aside>
    
2. First…Go to the path…
    
    ```jsx
    $Desktop/work/tools/openlane_working_dir/openlane/configuration
    ```
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled.png)
    
3. Open README file…
    
    ```jsx
    $less README.md
    ```
    
4. Inside the file, you will see the variables required for each process (Synthesis, Floorplanning). These variables have default values, but you can set them.
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%201.png)
    
5. If we go back to configuration folder, and we open floorplan.tcl to see again default values
    
    ```jsx
    $less floorplan.tcl
    ```
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%202.png)
    
6. In another terminal go to the next path and open config.tcl
    
    ```jsx
    $cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a
    ```
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%203.png)
    
7. In the terminal in which we run the synthesis… Type:
    
    ```jsx
    $run_floorplan
    ```
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%204.png)
    

---

### SKY_L7 - Review floorplan files and steps to view floorplan

1. To analize the results go to the next path:
    
    ```jsx
    $cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs
    ```
    
2. See the latest file generated
    
    ```jsx
    $cd latest file
    
    $cd logs/floorplan
    
    $less 4-ioPlacer.log
    ```
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%205.png)
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%206.png)
    
3. Go back to…
    
    ```jsx
    $cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/*latest file*
    
    $less config.tcl
    ```
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%207.png)
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%208.png)
    
4. Go back to the terminal and open sky130A_sky130_fd_sc_hd_config.tcl
    
    ```jsx
    $cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a
    
    $less sky130A_sky130_fd_sc_hd_config.tcl
    ```
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%209.png)
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%2010.png)
    
5. You have finished Floorplan step. How the floorplan looks like?
    
    ```jsx
    $cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/*latest file*/results/floorplan 
    
    $ls -ltr
    
    $less picorv32a.floorplan.def
    ```
    
    And you must open “.def” file
    
6. Here you can see the area of your complete die. (a b) (c d)
    - a → lower left X value [database units]
    - b → lower left Y value [database units]
    - c → upper right X value [database units]
    - d → upper right Y value [database units]
    
    UNITS DISTANCE MICRONS 1000 → It means 1u = 1000 [database units]
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%2011.png)
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%2012.png)
    
    <aside>
    📌 The area of the die is = 0.443587212 [microns]
    
    </aside>
    
7. To see the actual layout after floorplan, we have to go to the next path and open Magic.
    
    ```jsx
    $Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/*latest file*/results/floorplan
    
    $magic -T /home/**USER**/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
    ```
    
8. Magic is opening.

![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%2013.png)

---

### SKY_L8 - Review floorplan layout in Magic

1. Maximize Magic window.
2.  To select the entire layout press S on your keyboard and then press V to center the layout.
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%2014.png)
    
3. To zoom part of the layout you must form a box → Left mouse click and right mouse click. Then press Z on your keyboard.
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%2015.png)
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%2016.png)
    
4. To select a certain block in layout, move the mouse over it and press S.
5. Select a horizontal pin. And type “what” in the tkcon window. The result indicates the layer of the pin. 
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%2017.png)
    
6. Seelect a vertical pin. And type “what” in the tkcon window. The result indicates the layer of the pin.
    
    ![Untitled](Day%202%20226b907d8c7c4964a339e934466876d3/Untitled%2018.png)
    
7. To quit Magic… File - Quit - Yes
---
---

# Day 3 - Design library cell using Magic Layout and ngspice characterization

## SKY130_D3_SK1 - Labs for CMOS inverter ngspice simulations

### SKY_L0 - IO placer revision

 The design we have been working on has equidistant pins.

We can configurate this….

### IO placer :

It’s an Open-source EDA tool which is used to place the IOs around the core.

### How?

1) Go to the next path:

```jsx
$cd /Desktop/work/tools/openlane_working_dir/openlane/configuration

$less README.md
```

<aside>
📌 README file has the description of all the variables

</aside>

2) Go back and open floorplan.tcl

```jsx
$cd /Desktop/work/tools/openlane_working_dir/openlane/configuration

$less floorplan.tcl
```

We can see FP_IO_MODE is set to 1…

```jsx
set ::env(FP_IO_MODE) 1; # 0 matching mode - 1 random equidistant mode
```

In the terminal in which we launched OpenLane…

```jsx
$set ::env(FP_IO_MODE) 2

$run_floorplan
```

In another terminal…

```jsx
$Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/fecha/results/floorplan

$ls

$magic -T /home/**USER**/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

<aside>
📌 Take care: This process must be before placement. It’s to configure the floorplan in another way.

</aside>

---

### SKY_L5 - Lab steps to git clone vsdstdcelldesign

Go to the next path and type the next command to get the git …

```jsx
$cd Desktop/work/tools/openlane_working_dir/openlane/

$git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```

When the process ends…

```jsx
$ls -ltr

$cd vsdstdcelldesig

$ls -ltr
```

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled.png)

If we look into these files, we will realize that tech file isn’t in this directory. So, we need to copy it.

Open a new terminal and go to the path in which is the tech file for Magic…

```jsx
$ cd Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/

$ls -ltr
```

The tech file is…. “***sky130A.tech***”

For copy the file do this…

```jsx
$cp sky130A.tech /home/USER/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesig/
```

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%201.png)

Now, if we go to the next path Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesig (the path in the first terminal)… We will see the “***sky130A.tech***” file.

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%202.png)

We can open Magic…

```jsx
$cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesig

$magic -T sky130A.tech sky130_inv.mag &
```

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%203.png)

Then, we will see this design in Magic…

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%204.png)

---

## SKY130_D3_SK2 - Inception of Layout Â CMOS fabrication process

### SKY_L8 - Lab introduction to Sky130 basic layers layout and LEF using inverter

LEF is used for placement. Placement doesn’t need information about th logic of the circuit. It just need information about metal layers. 

LEF only shows information about all the metal layers.

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%205.png)

---

### SKY_L9 - Lab steps to create std cell layout and extract spice netlist

A part of an STD Cell of an inverter has been erased…

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%206.png)

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%207.png)

This shows errors in DRC. After set the corresponding layers the DRC is correct and free of errors.

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%208.png)

**How to extract to SPICE…**

In terminal tkcon…

```jsx
$pwd
```

 It shows a ***path***…

```jsx
extract all
```

The file is… sky130_inv.ext

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%209.png)

In a terminal we go to the ***path*** indicated before…

```jsx
$cd /Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

$ls -ltr
```

There will be the file sky130_inv.ext

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%2010.png)

Go back to **tckon terminal** and type: This command will extract all the parasitic capacitances…

```jsx
$ext2spice cthresh 0 rthresh 0
$ext2spice
```

It will show… “exttospice finished”

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%2011.png)

In the terminal we opened earlier, we have to go to the ***path:***

```jsx
$cd /Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

$ls -ltr
```

There will be the file sky130_inv.spice

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%2012.png)

To see the SPICE…

```jsx
$vim sky130_inv.spice
```

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%2013.png)

---

## SKY130_D3_SK3 - Sky130 Tech File Labs

### SKY_L1 - Lab steps to create final SPICE deck using Sky130 tech

To see the dimensions of the minimum box size…

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%2014.png)

In another terminal, go to…

```jsx
$cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesig/libs/

$ls -ltr
```

It should be contain the next 2 files… “pshort.lib” and “nshort.lib”

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%2015.png)

Change multiple parameters in vim file for a transient simulation…

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%2016.png)

To run simulation with ngspice… From a terminal… /openlane/vsdstdcelldesign

```jsx
ngspice sky130_inv.spice
```

---

### SKY_L2 - Lab steps to characterize inverter using sky130 model files

In ngspice, we could plot output vs time, and plot the input signal…

```jsx
plot y vs time a
```

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%2017.png)

![Untitled](Day%203%2087604c13907e41d790f08714cdaa8e9d/Untitled%2018.png)

---

---
