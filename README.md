Soil Composition in Danum Valley
================

## Abstract

The goal of this analysis was to identify structures in the soil
composition of the Danum Valley, Malaysian Borneo in order to assist
Professor David Burslem, from the University of Aberdeen, in his
research on the underlying factors that influence plant biodiversity.
The elemental composition of soil is expected to have relationships that
were explored through a principal component analysis on this dataset.
Outliers had a heavy influence on the interpretation of this analysis.
Nevertheless, some previously known elemental relationships were
confirmed. Although spatial correlation was an expected conclusion, only
a single cluster of geographically close samples were observed in an
otherwise evenly distributed sample. Additionally, the analysis found
more interesting patterns when the results of the analysis were plotted
and examined visually, yielding the opportunity for further, more formal
analysis.

## Introduction

### Background

Tropical rainforests are ecosystems of high plant biodiversity (Meyers,
Mittermeier, Mittermeier, Kent , & da Fonseca , 2000). Previous research
explaining this biodiversity has been predominantly focused on
topological and environmental factors (Harms, Condit, Hubbell, & Foster,
2001). However, recent research has also incorporated the variation in
the soil components as an explanatory element for the same (John, et
al., 2007) . In the paper, “Soil Resources and Topography Shape Local
Tree Community Structure in Tropical Forests”, (Baldeck, et al., 2013)
the authors reported that soil contents accounted for a statistically
significant portion of the compositional variation. To improve the
comparability of elemental soil data for future research, one standard
data procedure was chosen for analyzing selected elements in the soil of
eight tropical forest plots around the world. The aim is to estimate the
amount of an element in soil that is available to the trees by using
different methods of extraction. The data set proposed comes from one of
those plots, the Danum Valley in Malaysian Borneo. The concentration of
each element was extracted from the soil sample from three hundred
different geographical locations within a fifty-hectare plot using
Barium Cloride. Elements selected were based on previous known
properties that affect soil fertility and plant growth.

### Objectives

Due to the complexity of ecological systems, we expect that studying the
combined effects of elements in the soil will help determine structures
in the data that summarize relationships between different variables
without making strong assumptions. Moreover, it is known that certain
elements are expected to be collinear, such as Magnesium and Calcium,
which have an expected ratio for healthy plant growth. However, there is
still uncertainty regarding the ratio in which other selected elements
need to be present to contribute to the variation. Furthermore, the data
presented comes from the same plot and thus has spatial patterns which
could mislead analysis by identifying relationships simply on the basis
of the spatial structure. These potential underlying relationships
between the variables in a multidimensional dataset make it viable for
multivariate analysis. A principle component analysis can help explain
plant biodiversity composition by grouping certain parts of the soil
data together and determining how it is internally related. This
anlaysis is done using R-Studio (R Core Team, 2018). The results of the
analysis will be shared with Professor David Burslem from the University
of Aberdeen to assist in his research on variation in plant distribution
structures and what affects the variation from place to place.

## Data Exploration

Graphical and numerical summaries of the entire dataset gave some keen
insights. The correlation plot below shows significant linear
relationships between many of the variables in the dataset. Thus, a
principal component analysis approach to assess the extent to which
these relationships contribute to the variation in soil samples is
appropriate.

<div class="figure" style="text-align: center">

<img src="README_files/figure-gfm/corrplot-1.png" alt="\label{fig:corrplot}Correlation Plot"  />
<p class="caption">
Correlation Plot
</p>

</div>

The boxplot of the scaled versions of the variables indicate the
differences in the variance of different variables used for the
analysis. It also helps in identifying outliers that might impact the
analysis. It should also be noted that the data is skewed.

<div class="figure" style="text-align: center">

<img src="README_files/figure-gfm/boxplot-1.png" alt="\label{fig:boxplot}Boxplot of all Variables"  />
<p class="caption">
Boxplot of all Variables
</p>

</div>

### The Dataset

The data had two sets of the same variables measured in different units.
The measurements were taken in cmolc/kg were used for the analysis
because measurements of total exchangeable bases and expected cation
exchange capacity were calculated in the same unit. Other variables in
the dataset included the percentage of base saturation,
calcium-magnesium ratio and the percentage of aluminum saturation. A
further look into the dataset along with discussions revealed the total
exchangeable cations were a linear sum of the basic cations measured in
the data. Consequently, the variable excluded from the analysis. The
final variables used for the entire analysis are summarized in the table
below.

<table>
<caption>
Variable Description
</caption>
<thead>
<tr>
<th style="text-align:left;">
Variable
</th>
<th style="text-align:left;">
Description
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
pH
</td>
<td style="text-align:left;">
Measure of Acidity or Alkalinity (7 is neutral)
</td>
</tr>
<tr>
<td style="text-align:left;">
Al.1
</td>
<td style="text-align:left;">
Aluminum (cmolc/kg)
</td>
</tr>
<tr>
<td style="text-align:left;">
Ca.1
</td>
<td style="text-align:left;">
Calcium (cmolc/kg)
</td>
</tr>
<tr>
<td style="text-align:left;">
Fe.1
</td>
<td style="text-align:left;">
Iron (cmolc/kg)
</td>
</tr>
<tr>
<td style="text-align:left;">
K.1
</td>
<td style="text-align:left;">
Potassium (cmolc/kg)
</td>
</tr>
<tr>
<td style="text-align:left;">
Mg.1
</td>
<td style="text-align:left;">
Magnesium (cmolc/kg)
</td>
</tr>
<tr>
<td style="text-align:left;">
Mn.1
</td>
<td style="text-align:left;">
Manganese (cmolc/kg)
</td>
</tr>
<tr>
<td style="text-align:left;">
Na.1
</td>
<td style="text-align:left;">
Sodium (cmolc/kg)
</td>
</tr>
<tr>
<td style="text-align:left;">
ECEC
</td>
<td style="text-align:left;">
Expected Cation Exchange Capacity
</td>
</tr>
<tr>
<td style="text-align:left;">
BS
</td>
<td style="text-align:left;">
Percentage of Base Saturation
</td>
</tr>
<tr>
<td style="text-align:left;">
Ca.Mg
</td>
<td style="text-align:left;">
Calcium-Magnesium Ratio
</td>
</tr>
<tr>
<td style="text-align:left;">
Al.Sat
</td>
<td style="text-align:left;">
Aluminum Saturation
</td>
</tr>
<tr>
<td style="text-align:left;">
Gx
</td>
<td style="text-align:left;">
Geographical- x-coordinate
</td>
</tr>
<tr>
<td style="text-align:left;">
Gy
</td>
<td style="text-align:left;">
Geographical- y-coordinate
</td>
</tr>
</tbody>
</table>

### Outliers

The first step was to create scatterplots to visualize the relationships
between different variables, which was only possible because the data
set had a small number of variables. The figure below shows that strong
outliers influence the relationship between iron and calcium. Similar
patterns are also seen when these elements are plotted with the other
covariates.

<div class="figure" style="text-align: center">

<img src="README_files/figure-gfm/scatterplot-1.png" alt="\label{fig:scatterplot}Calcium-Iron Scatterplot"  />
<p class="caption">
Calcium-Iron Scatterplot
</p>

</div>

Methods to eliminate these outliers were discussed and it was concluded
that there was no proper way to identify if the significantly high or
low concentration of an element in a sample was a clerical error or an
accurate outlying observation. Thus, no theoretical method could be
applied to exclude these from the dataset. The following methods of
outlier detection were considered –

• Removing any observation which lay above and below 2 standard
deviations of the mean of each element separately – this method was
eliminated as it led to a substantial loss of data.

• Removing the observations that contained the maximum concentration of
each element. This again was considered infeasible as not all elements
had concerning values.

• Finally, the two most concerning values were eliminated as they were
approximately double the value of their preceeding observation and could
likely be attributed to measurement or recording error. These
observations were sample 287, which had a really high calcium
concentration of 61.66 cmolc/kg, and 241, which had a iron concentration
of 2.42 cmolc/kg.

Removing the outliers reduced the dataset to 298 observations. The data
contained by the removed samples are geographically close to other
samples hence the loss of data can be considered negligible.

While there were still some concerning values it was concluded that many
of the outlier removal techniques did not widely impact the analysis,
thus retaining any other value might not significantly impact the
results of the analysis at the exploratory stage.

### Spatial Correlation

The soil samples from which these observations are obtained were taken
from the same geographical plot. Thus, it is not unreasonable to assume
that spatial patterns may be reflected in the principal component
analysis. To identify any patterns in the data attributed to spatial
dependency the following graphic was used. It maps the observations
according to their geographical coordinates.

<div class="figure" style="text-align: center">

<img src="README_files/figure-gfm/spatial-1.png" alt="\label{fig:spatial}Relative Geographical Location of Sampled Points - The size of the circle represents the y-coordinate, thus an increase in the size reflects an increase in the y-coordinate and the color represents the x-coordinate, an increase in the x-coordinate is classified by a change in color from black to blue"  />
<p class="caption">
Relative Geographical Location of Sampled Points - The size of the
circle represents the y-coordinate, thus an increase in the size
reflects an increase in the y-coordinate and the color represents the
x-coordinate, an increase in the x-coordinate is classified by a change
in color from black to blue
</p>

</div>

## The Analysis

The final data matrix that was subjected to principal component analysis
consisted of the following variables, calcium, aluminum, sodium,
potassium, magnesium, manganese, iron, expected cation exchange
capacity, calcium-magnesium ratio, base saturation and pH. While most
variables were measured in the same unit their range was widely
different from each other since the proportion of each element in the
soil is different. This called for scaling of the data and thus the
analysis was conducted on the correlation matrix.

<div class="figure" style="text-align: center">

<img src="README_files/figure-gfm/scree-1.png" alt="\label{fig:scree}Scree plot of the squared deviation from the principal component analysis which indicates the importance of each component"  />
<p class="caption">
Scree plot of the squared deviation from the principal component
analysis which indicates the importance of each component
</p>

</div>

In order to decide which component to interpret the scree plot was used.
Seven principal components seem to be explaining most of the variance in
the data. Even so, this is still a high number of components and the
scree plot does suggest a decline in the overall percentage of variation
explained before this point. Thus, using Kaiser’s Criteria (components
with squared deviance &gt; 1) only the first three components were
deemed important. These explained approximately 71% of the variation in
the data thus offering a valuable insight into the majority trends in
the data.

<div class="figure" style="text-align: center">

<img src="README_files/figure-gfm/network-1.png" alt="\label{fig:network}Network graph of original variables and their contribution to the new variables - red represents a negative relationship and blue represents a positive relationship"  />
<p class="caption">
Network graph of original variables and their contribution to the new
variables - red represents a negative relationship and blue represents a
positive relationship
</p>

</div>

The selected components or new variables were then put through the
process of reification. From the figure above it is difficult to
pinpoint exactly which variables have a high influence on which selected
principal component. Thus, two methods were considered to decide a
cut-off for the variables with high enough coefficient values to be
interpreted. The first of these was the equilibrium criteria (1/the
number of variables in the data). The second method, called Mardia’s
Criterion (sets the cut off at 0.7 times the largest coefficient in the
new variables), agreed on similar variables. In principal component 3
Mardia’s criteria identified the contribution of iron as the most
significant but agreed with the equilibrium criteria by the removal of
three outliers. Thus, a reasonable balance between the two methods was
used to select the important variables on the basis of the method of
interpretation.

## Results and Discussion

Direct interpretation of the new axis indicated the following results.
The first variable primarily showed a trend between variables measuring
the pH of the soil, expected cation exchange, base saturation, aluminum,
calcium and magnesium. Clearly, high values of calcium and magnesium
indicate a high expected cation exchange capacity (Mengel, 2019). The
soil is on average acidic to neutral since the range of values lie
between 7 and 4. Presence of high levels of aluminum, indicate lower pH
and hence higher acidity of the soil. High levels of base saturation
indicate the presence of high levels of exchangeable base cations that
is calcium and magnesium and low levels of aluminum.

These relationships are expected and documented and most likely pointing
towards the pH of the soil (Spargo, Allen, & Kariuki, 2013). Thus, high
percentage of base saturation, cation exchange capacity, pH, calcium and
magnesium will be associated with high values of the new observations or
scores while high levels of aluminum will be associated with low values
in the new observations. An interesting discovery was the indication of
a bipolar relationship between the expected cation exchange capacity and
aluminum, since aluminum is an exchangeable cation. This maybe the
result of the strong relationships between the other variables or the
amphoteric nature of aluminum.

Taking a look at the second new variable suggested that low levels of
magnesium, manganese and sodium indicate a higher calcium-magnesium
ratio in the soil. The direct relation between magnesium and manganese
is another questionable conclusion as these elements are known to be
inversely related while the calcium-magnesium ratio and manganese
relationship is not surprising (Maas, Moore, & Mason, 1969). Going up
the observations in the second component would show a decrease in these
elements in the new observations but an increase in the
calcium-magnesium ratio.

Finally, the third component indicated a direct relation between iron
and manganese in the soil. Thus, a decrease in both is observed when
going down observations in the third new variable. These conclusions are
on the basis of the matrix of loadings that can be viewed in the
appendix of the report.

<div class="figure" style="text-align: center">

<img src="README_files/figure-gfm/biplot1-1.png" alt="\label{fig:biplot1}Biplot of component one and two - Closer the arrow of the old variable is to an axis, the higher its contribution to the axis. The length of the arrow indicates the importance of the variable in the construction of the new axis."  />
<p class="caption">
Biplot of component one and two - Closer the arrow of the old variable
is to an axis, the higher its contribution to the axis. The length of
the arrow indicates the importance of the variable in the construction
of the new axis.
</p>

</div>

The plot above show the old variables and their relative contribution to
each new variable in relation with each other. While these plots mostly
align with the findings from the chosen criteria, they indicate an equal
contribution of calcium-magnesium ratio in determining the first two new
components. The relatively high correlation between this ratio and the
first two principal components also reiterates these findings. Thus,
there might be more to explore in the relationship between the ratio and
the new variables. Similar plots with the other two variables confirm
the dependency of the components on the variables they were originally
attributed to.

These figures also raise concerns about certain outlying points that
might impact the analysis depending on their importance. These are
observation number 122, 210, 219, 220 and to a point 278. While two of
these are measured close to each other, the rest are randomly scattered
as seen in the plot below. These would be interesting to explore through
further analysis.

<div class="figure" style="text-align: center">

<img src="README_files/figure-gfm/outlier2-1.png" alt="\label{fig:outlier2}Geographical position of points that have a potentially high impact on the analysis. These points are highlighted in red"  />
<p class="caption">
Geographical position of points that have a potentially high impact on
the analysis. These points are highlighted in red
</p>

</div>

Reduced space plots were another way of exploring the different
relationships. They were used for the detection of any spatial
structures identified by the analysis. The figure below uses the
relative position of the data according to the index given above in the
spatial correlation section. There seems to be some spatial correlation
in the negative values of the first component and near the center of the
second since the size and color of the circles are similar. Otherwise
the variation is evenly spread across both components even though a
large number of values lie in the cluster that indicate the spatial
correlation. This clustering might be attributed to the first component
as the second and third component plotted together do not show such
patterns but the third and first do. The graphs also shows some
explorable relationship between the new components.

<div class="figure" style="text-align: center">

<img src="README_files/figure-gfm/RSP1-1.png" alt="\label{fig:RSP1}Reduced Space Plot - A scatterplot of the new observations plotted on the first two components reflecting the geographical locations of the points. The circled values are the one spatially close to each other"  />
<p class="caption">
Reduced Space Plot - A scatterplot of the new observations plotted on
the first two components reflecting the geographical locations of the
points. The circled values are the one spatially close to each other
</p>

</div>

<div class="figure" style="text-align: center">

<img src="README_files/figure-gfm/RSP3 -1.png" alt="\label{fig:RSP3}Reduced Space Plot - A scatterplot of the new observations plotted on the first and third component reflecting the geographical locations of the points"  />
<p class="caption">
Reduced Space Plot - A scatterplot of the new observations plotted on
the first and third component reflecting the geographical locations of
the points
</p>

</div>

<div class="figure" style="text-align: center">

<img src="README_files/figure-gfm/RSP4-1.png" alt="\label{fig:RSP4}Reduced Space Plots - Scatterplot of the new observations plotted on the first and second components reflecting their relationship with Aluminum Saturation."  />
<p class="caption">
Reduced Space Plots - Scatterplot of the new observations plotted on the
first and second components reflecting their relationship with Aluminum
Saturation.
</p>

</div>

Finally, the new observations were plotted with the help of aluminum
saturation. The plot below indicates a fall in aluminum saturation as
the values in component one rises. This might be an indication of a
bipolar relationship between the expected cation exchangeable capacity,
or just a reiteration of the already known perfect correlation between
base saturation and aluminum saturation. A cluster of higher aluminum
saturation values are also observed while plotting the second and third
component. Another potential relationship that might be explored. The
third and first component did not reveal anything other than what we
concluded from the first two plots.

<div class="figure" style="text-align: center">

<img src="README_files/figure-gfm/RSP5-1.png" alt="\label{fig:RSP5}Reduced Space Plots - Scatterplot of the new observations plotted on the second and third components reflecting their relationship with Aluminum Saturation."  />
<p class="caption">
Reduced Space Plots - Scatterplot of the new observations plotted on the
second and third components reflecting their relationship with Aluminum
Saturation.
</p>

</div>

## Conclusion

The result of the analysis should be interpreted bearing in mind that
the underlying assumptions - symmetry in the data and equality of
variance are violated which, does not really affect the analysis but is
worth noting. The aim of the analysis was to find relationships in the
soil composition that could help explain variation in the biodiversity
of rainforests. Some interesting relationships presented themselves
throughout the analysis such as the spatial dependency in certain areas
and the linear patterns in the scatterplots of the new observations. The
outliers not removed from the analysis are also worth exploring through
further analysis. The meaning of the relationships brought out from the
new components would require further details about soil composition and
healthy plant growth.

# References

• Mengel, D. B. (2019). Fundamentals of Soil Cation Exchange Capacity
(CEC). Retrieved from www.extension.purdue.edu:
<https://www.extension.purdue.edu/extmedia/ay/ay-238.html>

• Spargo, J., Allen, T., & Kariuki, S. (2013, July 1). Interpreting Your
Soil Test Results. Retrieved from ag.umass.edu:
<https://ag.umass.edu/soil-plant-nutrient-testing-laboratory/fact-sheets/interpreting-your-soil-test-results>

• Meyers, N., Mittermeier, R. A., Mittermeier, C. G., Kent , J., & da
Fonseca , G. A. (2000). Biodiversity hotspots for conservation
priorities. Nature, 403, 853–858.

• Baldeck, C. A., Harms, K. E., Yavitt, J. B., John, R., Turner, B.,
Valencia, R., & Navarrete, H. (2013). Soil Resources and Topography
Shape Local Tree Community Structure in Tropical Forests. Proceedings of
the Royal Society B: Biological Sciences.

• John, R., Dalling, J. W., Harms, K. E., Yavitt, J. B., Stallard, R.
F., Mirabello, M., & Hubbell, S. P. (2007). Soil Nutrients Influence
Spatial Distributions of Tropical Tree Species. Proceedings of the
National Academy of Sciences, 864–69.

• Harms, K. E., Condit, R., Hubbell, S. P., & Foster, R. B. (2001).
Habitat Associations of Trees and Shrubs in a 50-Ha Neotropical Forest
Plot. Journal of Ecology, 947–59.

• Maas, E. V., Moore, D. P., & Mason, B. J. (1969). Influence of calcium
and magnesium on manganese absorption. Plant physiology, 44(6), 796–800.

• R Core Team (2018). R: A language and environment for statistical
computing. R Foundation for Statistical Computing, Vienna, Austria. URL
<https://www.R-project.org/>.

• Hadley Wickham (2017). tidyverse: Easily Install and Load the
‘Tidyverse’. R package version 1.2.1.
<https://CRAN.R-project.org/package=tidyverse>

• Taiyun Wei and Viliam Simko (2017). R package “corrplot”:
Visualization of a Correlation Matrix (Version 0.84). Available from
<https://github.com/taiyun/corrplot>

• Yuan Tang, Masaaki Horikoshi, and Wenxuan Li. “ggfortify: Unified
Interface to Visualize Statistical Result of Popular R Packages.” The R
Journal 8.2 (2016): 478-489.

• Sacha Epskamp, Angelique O. J. Cramer, Lourens J. Waldorp, Verena D.
Schmittmann, Denny Borsboom (2012). qgraph: Network Visualizations of
Relationships in Psychometric Data. Journal of Statistical Software,
48(4), 1-18. URL <http://www.jstatsoft.org/v48/i04/>.

• Korkmaz S, Goksuluk D, Zararsiz G. MVN: An R Package for Assessing
Multivariate Normality. The R Journal. 2014 6(2):151-162.

• Hao Zhu (2019). kableExtra: Construct Complex Table with ‘kable’ and
Pipe Syntax. R package version 1.1.0.
<https://CRAN.R-project.org/package=kableExtra>
