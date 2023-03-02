# Direct Sun Hours
The Grasshopper script-file included in this repository is used for computing the direct sun hours on windows and balcony doors of a set of buildings in a neighbourhood. Some of the buildings in the study area are represented in high level of detail (equivalent to [CityGML LOD4](https://www.sciencedirect.com/science/article/pii/S0198971516300436?via%3Dihub)), while others are represented in a lower level of detail (equivalent to [CityGML LOD2](https://www.sciencedirect.com/science/article/pii/S0198971516300436?via%3Dihub)). The goal is to examine how including or excluding obstructing gemmetries (e.g. balconies, balcony railings, etc.) of buildings represented in a high level of detail affect the results of daylight metric simulations such as the Sunlight Exposure (here expressed as direct sun hours).

<br>
<br>

## Direct Sunlight Exposure (definition):
Sunlight exposure is regulated by the Swedish Standard, which is based on the European Standard [EN 17037 - *Daylight in Buildings*](https://velcdn.azureedge.net/~/media/marketing/ee/professional/28mai2019%20seminar/veluxen17037tallinn28052019.pdf), and states that at minimum one room in an apartment has to receive at least 1.5 hours of direct sunlight on one day between February 1st and March 21st of a year.

<br>
<br>

## Input data:
- 3D city model including detailed building exterior information (equivalent to [CityGML LOD4](https://www.sciencedirect.com/science/article/pii/S0198971516300436?via%3Dihub)) like e.g. windows, balconies, balcony railings, etc. 

<br>

The below figure depicts a example of a 3D city model that can be used as input. The windows of the *target buildings* for which we are going to compute the direct sun hours for, are highlighted in yellow.

<br>
<p align="center"><img src="img/SE_study_area.PNG" width=70%></img></p>


<br>
<br>

The next figure gives you the opportunity to get a closer look over the *target buildings*.

<br>
<br>

<p align="center"><img src="img/target_buildings.PNG" width=40%></img></p>

<br>
<br>

## Requirements:

- An installed version of [Rhino 7](https://www.rhino3d.com/) with the following tools:
  - [Grasshopper](https://www.grasshopper3d.com/)
  - [LadyBug](https://www.ladybug.tools/ladybug.html)


<br>
<br>

## Workflow:
The process depicted in this workflow computes the mean & median Daylight Factor values over a grid of points (0.2m resolution) placed 0.8m above the floor area of a living room on different floors. The aforementioned process also calculates the min and max DF-values of a room along with the % of the floor area that complies to the daylight requirement stated in the [Swedish legislation (DF > 1%)](https://www.boverket.se/globalassets/publikationer/dokument/2019/bbr-2011-6-tom-2018-4-english-2.pdf). This implementation considers the effect of including or excluding building facade geometries (e.g. balconies, balcony railings, etc.) that may obstruct daylight access in densily built urban environments. Finally, this implementation also takes into consideration how using different building facade materials and colours affects daylight access.

<br>

<ins><b>Step 1:</ins></b> Add the geometries (Geometry Pipeline) of the room (walls, ceiling, floor, windows, eaves) <br><br>
<ins><b>Step 2:</ins></b> Add the geometries (Geometry Pipeline) of the obstructions (e.g. ground, building facades of surrounding buildings, balconies of surrounding buildings, balcony railings of surrounding buildings) <br><br>
<ins><b>Step 3:</ins></b> Add a slider and a panel with the standard height value of a floor (2.79m). Include a multiplier to combine the slider and the floor height values to obtain the elevation coordinates (z-coord) of the different room-related geometries from floor to floor. <br><br>
<ins><b>Step 4:</ins></b> Add one Climate Studio *LightingMaterial* module per obstructing geometry to pick an appropriate material and colour with specific spectral properties. <br><br>
<ins><b>Step 5:</ins></b> Add one Climate Studio *LightingMaterial* module for every room-related geometry and pick an appropriate material and colour.<br><br>
<ins><b>Step 6:</ins></b> Add a Climate Studio *SceneLayer* module to construct a Scene Layer for daylight simulation, one for every geometry.<br><br>
<ins><b>Step 7:</ins></b> Add a sensor grid (using the Climate Studio *SensorGrid* module) with 0.2m resolution and placed 0.8m above a room floor surface.<br><br>
<ins><b>Step 8:</ins></b> Add a *Boolean Toggle* in combination with two *Cull Pattern* modules to control when balcony and balcony railing geometries are to be included as obstructions in the DF-computation and when not. <br><br>
<ins><b>Step 9:</ins></b> Add Climate Studio *DaylightModel* to prepare the scene for running the DF daylight simulation.<br><br>
<ins><b>Step 10:</ins></b> Add a Climate Studio *Daylight* module and select *Daylight Factor* as the chosen standard to run the corresponding daylight . <br><br>

<img src="img/DSH_gh_flowchart.png"></img>

<br>
<br>


## Output:
The computed Daylight Factor for every point in the grid is presented in the Rhino environment as a visual output while the corresponding mean and median DF-values along with the percentage of the room's floor area complying to the DF>=1% requirement are exported to a panel inside the Rhino Grasshopper environment.

<p align="center"><img src="img//Direct_Solar_Hours_output.PNG" width=30%></img></p>

<br>
<br>



## References:


<br>


<br>
<br>



## License
Copyright 2023 Sustainable3DCities <br><br><br>
The 3-Clause BSD License <br>
https://opensource.org/licenses/BSD-3-Clause <br>
<br><br><br>
Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
