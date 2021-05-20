
# Single-Family Zoning (SFZ) Map Portfolio 

### Purpose
This page is designed to showcase the portfolio of maps I created for my final project in GES 687. This project centered around mapping and analyzing single-family zoning restriction policies in the Baltimore region, as well as analyzing the relationship they have with various community outcomes. For this project, I chose to look at how widespread single-family zoning restrictions are in the Baltimore region, as well as looking at the relationship between these zoning restrictions and community demographcis such as median household income and educational attainment. The results of my project are shown below. 
<br><br/>
Scroll to the bottom of this page to view my analysis of the results and the sources used to obtain my data. 

---
### Write-Up 
Single-family zoning restrictions are zoning policies limiting residential development exclusively to detached, single-family homes (a good example is the traditional detached suburban home). There is heavy debate among whether these policies should exist because many theorize that these policies diminish access to these communities for households that are less likely to use detached single-family housing such as thsoe that are lower-income, multigenerational, and ethnic minorities. Many speculate that adding more mixed-use zoning can greatly improve the economic sustainability of communities, increase diversity, and decrease inequality. This paper will attempt to map this phenomenon by measuring the relationship existing between single-family zoning and various community demographics. For more information about single-family zoning 
<a href="https://www.tandfonline.com/doi/full/10.1080/01944363.2019.1651216" target="_blank">Click Here.</a>


### Methodology

The output for this project was created by taking data from various sources holding information on zoning regulations and community demographics, and then using various statistical software to visualize data into the maps shown below. <br><br/>
Obtaining data on zoning and community demographics were taken from the Maryland Department of Planning and the American Community Survey. Shapefiles on zoning was taken using the State Department of Assessments and Taxation (SDAT) dataset which contains data on most maryland properties detailing zoning and land use codes. Land-uses maps were converted into centroids to specifcally count the number of residential properties with single-family zoning restrictions in the Baltimore region. 
Community demographics such as race, income, and education were taken from the ACS survey, an annual survey that obtains data on millions of U.S. households. ACS data was loaded into R statistical software using the tidycensus program, and was then transformed into shapefiles that could be loaded into QGIS Mapping software. 
Once these shapefiles were created, both the demographic data and zoning maps data were loaded into QGIS and merged using the intersections command to create bivariate cholorpleth maps showing the relationship between single-family zoning, income, and educational attainment amongst the population. 

---

# Results


### [Full Single-Family Zoning Map](/project_probation/index)
This map shows the full display for all single-family zoned land in Central Maryland (measured by land-use data) 
<img src="images/Full Single-Family Zoning Map BMSA.png?raw=true"/>

---
### [Single-Family Zoning & Income Chloropleth Map](/project_probation/index)
This map displays the relationship between the proportion of single-family zoned properties in a census tract and the median household income of that area.
<img src="images/Chloroplethmap.png"/>

---
### [Single-Family Zoning & Educational Attainment Chlorlopleth Map](/project_probation/index) 
This chloropleth map displays the relationship between the proportion of single-family zoned properties in a census tract and the proportion of that census tract that has obtained a college degree. 
<img src="images/Single Family zoning and Education chloropleth.png"/>



---
### [Median House Price Map](/project_probation/index)
This map shows the median houseprice of the census tracts in the Baltimore region. 
<img src="images/housepricemap.png"/>

---
### [Baltimore City SFZ Map](/project_probation/index)
This map displays where single-family zoning restrictions exist in Baltimore City 
<img src="images/Baltcitymap.png?raw=true"/>

---
### [Baltimore County SFZ Map](/project_probation/index)
This map displays where single-family zoning restrictions exist in Baltimore County
<img src="images/Baltimorecountymap (2).png?raw=true"/>

---

### [Anne Arundel County SFZ Map](/project_probation/index)
This map displays where single-family zoning restrictions exist in Anne Arundel County
<img src="images/Arundelmap.png?raw=true"/>

---
### [Howard County Zoning Map](/project_pnw/index)
This map displays where single-family zoning restrictions exist in Howard County
<img src="images/Howardmap (2).png?raw=true"/>

---
### [Carroll County SFZ Map](/project_probation/index)
This map displays where single-family zoning restrictions exist in Carroll County
<img src="images/Carrollmap.png?raw=true"/>

---
### [Harford County SFZ Map](/project_probation/index)
This map displays where single-family zoning restrictions exist in Harford County
<img src="images/Harfordmap.png?raw=true"/>

---
### [Queen Anne's County SFZ Map](/project_probation/index)
This map displays where single-family zoning restrictions exist in Queen Anne's County
<img src="images/Queenannemap.png?raw=true"/>

---

### Analysis

Overall, the results of my research suggest that single-family zoning restrictions are not highly prevalent in the Baltimore region. Despite this, these zoning policies are still associated with higher income areas, indicating that these zoning policies significantly affect the income distributions of various communities in the region. Regression analysis using OLS and Fixed effects was also performed to gain a more in-depth understanding of the effect that single-family zoning has on communities in the region. It was found that single-family zoning not only singnificantly shifted the income distribution towards those with the highest incomes, but it was also found that these zoning policies were also associated with higher median house-prices and educational attainment. While more research would need to be performed to establish a causal realtionship between these community outcomes and single-family zoning (such as spatial regression analysis), it is clear that an association exists between single-family zoning restrictions and the characteristics that a community will have, potentially having large impacts on the culture, politics, and economy of an area. To view more information about this research 
<a href="https://github.com/jjustin1/jjustin1capstonepaper/blob/main/JustinJohnsonCapstoneGithub.pdf" target="_blank">Click Here.</a>


---

### Sources

<a href="https://planning.maryland.gov/Pages/OurProducts/DownloadFiles.aspx" target="_blank">Maryland SDAT (Zoning Data).</a>
<br><br/>
<a href="https://www.socialexplorer.com/data/ACS2019_5yr/metadata/?ds=ACS19_5yr" target="_blank">American Community Survey (Demographic Data).</a>
<br><br/>
<a href="https://github.com/jjustin1/GESFinalProject.io/blob/master/GESFinalprojectRmarkdown.pdf" target="_blank">Data Collection Process (Knitted R Markdown).</a>

