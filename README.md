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

The next figures give you the opportunity to get a closer look over the *target buildings*.

<br>
<br>

<p align="center"><img src="img/target_buildings.PNG" width=40%></img>&emsp;<img src="img/target_buildings_2.PNG" width=50.3%></img></p>

<br>
<br>

## Requirements:

- An installed version of [Rhino 7](https://www.rhino3d.com/) with the following tools:
  - [Grasshopper](https://www.grasshopper3d.com/)
  - [LadyBug](https://www.ladybug.tools/ladybug.html)


<br>
<br>

## Workflow:
The process depicted in this workflow computes the Direct Sun Hour values calculated for March 21st (0.5 min temporal resolution) over a grid of points (0.1m resolution) placed over every window in the target buildings (see figure in *Input data* section). . Finally, this implementation also takes into consideration how including or excluding more detailed facade objects such as balconies and balcony railings affects daylight access (i.e., total hours of direct sunlight per grid point on March 21st). The position of the Sun during that time of the year is estimated based on the latitude for that particular area. The applied methodology is described in the following steps:

<br>

<ins><b>Step 1:</ins></b> Get the latitude of your study area by first importing a Solemna weather data file over the closest location to the study area and the adding a Ladybug Import Location module. In this case, the study area is located in Malmö, Southern Sweden and the weather file for Copenhagen (Denmark) is is chosen as it is closest to this location. <br><br>
<ins><b>Step 2:</ins></b>  <br><br>
<ins><b>Step 3:</ins></b>  <br><br>
<ins><b>Step 4:</ins></b>  <br><br>
<ins><b>Step 5:</ins></b>  <br><br>
<ins><b>Step 6:</ins></b>  <br><br>
<ins><b>Step 7:</ins></b>  <br><br>
<ins><b>Step 8:</ins></b>  <br><br>
<ins><b>Step 9:</ins></b>  <br><br>
<ins><b>Step 10:</ins></b> <br><br>

<img src="img/DSH_gh_flowchart2.png"></img>

<br>
<br>


## Output:
The computed Direct Sun Hours for every point in the grid is presented in the Rhino environment as a visual output while the corresponding values along with the grid-point coordinates the refer to are exported to 2 panels inside the Rhino Grasshopper environment. The panel contents can be exported to txt-files and imported to GIS environments for further processing.

<p align="center"><img src="img//Direct_Solar_Hours_output.PNG" width=30%></img></p>

<br>
<br>
<br>
<br>

<p align="center"><img src="img//DSH_output_raw.png" width=70%></img></p>

<br>
<br>
<br>
<br>

## References:

EN 12665:2018, Light and lighting — Basic terms and criteria for specifying lighting requirements.
<br>

Ladybug Rhino Grasshopper plugins: https://www.ladybug.tools/ladybug.html#solaraccess

<br>
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
