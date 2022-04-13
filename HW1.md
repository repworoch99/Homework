Homework 01
================
REP WOROCH

    ## Loading required package: airports

    ## Loading required package: cherryblossom

    ## Loading required package: usdata

    ## Loading required package: usethis

    ## 
    ## Attaching package: 'dplyr'

    ## The following object is masked from 'package:gridExtra':
    ## 
    ##     combine

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

1.  **Reverse-engineering the grammar of graphics.**  
    The plot shown in the article shows the differences between the
    different states’ testing and new cases between the months of June
    and July. The data used in the plots are the percentage change in
    testing and new cases (y-axis), and the time (June to July)
    (x-axis). Besides the above description mapping the data to the
    axes, the data are shown in a line graph, with color (yellow, green)
    mapped to the change in testing and the change in new cases. The
    coordinate system is cartesian. Additionally, there are labels
    representing the total percentage change in new cases and testing
    between June and July. The data are then faceted by state, with a
    label showing the state each plot represents. The plots are then
    separated by states which had more new cases than testing, and
    states which had more testing than new cases.

2.  **Road traffic accidents in
Edinburgh.**

<!-- end list -->

``` r
accidents$weekend = ifelse(accidents$day_of_week == "Saturday", "Weekend", "Weekday")
accidents$weekend = ifelse(accidents$day_of_week == "Sunday", "Weekend", "Weekday")
ggplot(accidents, aes(x = time)) +
  geom_density(aes(fill = severity), alpha = 0.5) +
  facet_wrap(facets = vars(weekend), ncol = 1) +
  labs(
    title = "Number of accidents throughout the day", 
    subtitle = "By day of week and severity", 
    x = "Time of day", 
    y = "Density",
    color = "Severity"
  ) +
  scale_fill_viridis_d()
```

![](HW1_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

3.  **NYC marathon winners.**

4.  **US counties.**

## a.

``` r
ggplot(county) +
  geom_point(aes(x = median_edu, y = median_hh_income)) +
  geom_boxplot(aes(x = smoking_ban, y = pop2017))
```

    ## Warning: Removed 580 rows containing missing values (stat_boxplot).

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](HW1_files/figure-gfm/unnamed-chunk-4-1.png)<!-- --> The code above
creates both a scatterplot and boxplot from the county dataset. The
scatterplot plots median education level (median\_edu) on the x-axis,
and median household income (median\_hh\_income) on the y-axis. The
boxplot plots what type of smoking ban was in place in 2010
(smoking\_ban) on the x-axis, and the population for the county in 2017.
The output of the code combines the categories for median education
level and smoking ban status on the x-axis. The y values map both the
median household income and the population. The axes are labelled using
the scatterplot values. The resulting plot does not work for many
reasons, one being that the two individual plots are overlayed on top of
each other. Another fundamental issue is that y-axis is using the values
for population which are larger than the values for median household
income, thus the intended visual effects of the median household income
plot are eliminated.

## b.

``` r
#Plot A
ggplot(county, aes(x = homeownership, y = poverty)) +
  geom_point() +
  labs(title = "Plot A")
```

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](HW1_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
#Plot B
ggplot(county, aes(x = homeownership, y = poverty)) +
  geom_point() +
  geom_smooth(se = F) +
  labs(title = "Plot B")
```

    ## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'

    ## Warning: Removed 2 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](HW1_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
#Plot C
ggplot(county, aes(x = homeownership, y = poverty)) +
  geom_point() +
  geom_smooth(se = F, aes(linetype = metro), color = "green") +
  labs(title = "Plot C") +
  guides(linetype = FALSE)
```

    ## Warning: `guides(<scale> = FALSE)` is deprecated. Please use `guides(<scale> =
    ## "none")` instead.

    ## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'

    ## Warning: Removed 2 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](HW1_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
#Plot D
ggplot(county, aes(x = homeownership, y = poverty)) +
  geom_smooth(se = F, aes(linetype = metro), color = "blue") +
  geom_point() +
  labs(title = "Plot D") +
  guides(linetype = FALSE)
```

    ## Warning: `guides(<scale> = FALSE)` is deprecated. Please use `guides(<scale> =
    ## "none")` instead.

    ## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'

    ## Warning: Removed 2 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](HW1_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

``` r
#Plot E
ggplot(county, aes(x = homeownership, y = poverty, color = metro)) +
  geom_point() +
  geom_smooth(se = F, aes(linetype = metro), color = "blue") +
  labs(title = "Plot E")
```

    ## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'

    ## Warning: Removed 2 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](HW1_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
#Plot F
ggplot(county, aes(x = homeownership, y = poverty, color = metro)) +
  geom_point() +
  geom_smooth(se = F, aes(linetype = metro, color = metro)) +
  labs(title = "Plot F") +
  guides(linetype = FALSE)
```

    ## Warning: `guides(<scale> = FALSE)` is deprecated. Please use `guides(<scale> =
    ## "none")` instead.

    ## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'

    ## Warning: Removed 2 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](HW1_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

``` r
#Plot G
ggplot(county, aes(x = homeownership, y = poverty)) +
  geom_point(aes(color = metro)) +
  geom_smooth(se = F) +
  labs(title = "Plot G") +
  guides(linetype = FALSE)
```

    ## Warning: `guides(<scale> = FALSE)` is deprecated. Please use `guides(<scale> =
    ## "none")` instead.

    ## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'

    ## Warning: Removed 2 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](HW1_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

``` r
#Plot H
ggplot(county, aes(x = homeownership, y = poverty)) +
  geom_point(aes(color = metro)) +
  labs(title = "Plot H")
```

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](HW1_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

5.  **Napoleon’s march.** The following code is not my own, and was
    taken from a very informative guide on how to recreate the Minard
    plot using ggplot2. The guide I used can be found here:
    <http://euclid.psych.yorku.ca/www/psy6135/tutorials/Minard.html>

<!-- end list -->

``` r
breaks <- c(1, 2, 3) * 10^5 #a variable for defining the breaks in the graph
ggplot(Minard.troops, aes(long, lat)) + #the basic structure for the plot, using Minard.troops data and mapping long to the x-axis and lat to the y-axis
        geom_path(aes(size = survivors, colour = direction, group = group), #adding a geom_path with the size mapped to survivors, color to advancing or retreating, and grouped based on main battle versus diverted troops
                  lineend="round") + #rounded line ends
    scale_size("Survivors", range = c(1,10), #c(0.5, 15), #scaling the size to the number of survivors
               breaks=breaks, labels=scales::comma(breaks)) + #adding the breaks variable to map to the breaks in the grid
    scale_color_manual("Direction", #mapping the color to a manual scale specified by the direction (advancing or retreating)
                       values = c("red", "black"), 
                       labels=c("Advance", "Retreat")) 
```

![](HW1_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

``` r
plot_troops <- last_plot() #saves the last plot as a variable "plot_troops"
plot_troops + geom_text(data = Minard.cities, aes(label = city), size = 3) #adding text values of the cities and changing the size
```

![](HW1_files/figure-gfm/unnamed-chunk-13-2.png)<!-- -->

``` r
#the following code adjusts the position of the labels to ensure they do not overlap with points (I don't fully understand this but thought it was a nice touch so I included it)
if (!require(ggrepel)) {install.packages("ggrepel"); require(ggrepel)}
```

    ## Loading required package: ggrepel

``` r
library(ggrepel)
plot_troops +   
    geom_point(data = Minard.cities) +
    geom_text_repel(data = Minard.cities, aes(label = city))
```

![](HW1_files/figure-gfm/unnamed-chunk-13-3.png)<!-- -->

``` r
plot_troops_cities <- last_plot()

#removes the labels and legend, as well as ggplot theme elements
plot_troops_cities +
  coord_cartesian(xlim = c(24, 38)) +
  labs(x = NULL, y = NULL) +
  guides(color = FALSE, size = FALSE) +
  theme_void()
```

    ## Warning: `guides(<scale> = FALSE)` is deprecated. Please use `guides(<scale> =
    ## "none")` instead.

![](HW1_files/figure-gfm/unnamed-chunk-13-4.png)<!-- -->

``` r
plot_troops_cities_fixed <- last_plot()

#joins the temperature text with the date as in Minard's version
Minard.temp <- Minard.temp %>%
    mutate(label = paste0(temp, "° ", date)) 
head(Minard.temp$label)
```

    ## [1] "0° Oct18"   "0° Oct24"   "-9° Nov09"  "-21° Nov14" "-11° NA"   
    ## [6] "-20° Nov28"

``` r
#creates the temperature plot
ggplot(Minard.temp, aes(long, temp)) + #maps longitude to temperature
    geom_path(color="blue", size=1.5) + #geom_path() with a grey color and size
    geom_point(size=1) + #adds points
  geom_text_repel(aes(label=label), size=2.5) #adjust labels
```

![](HW1_files/figure-gfm/unnamed-chunk-13-5.png)<!-- -->

``` r
plot_temp <- last_plot()

plot_temp + 
  coord_cartesian(xlim = c(24, 38)) + #changes coordinates of temperature plot
  labs(x = NULL, y="Temperature") + #removes labels
  theme_bw() + #the below code removes ticks and grids to get it to the style of Minard
  theme(panel.grid.major.x = element_blank(),
        panel.grid.minor.x = element_blank(),
        panel.grid.minor.y = element_blank(),
        axis.text.x = element_blank(), axis.ticks = element_blank(),
        panel.border = element_blank())
```

![](HW1_files/figure-gfm/unnamed-chunk-13-6.png)<!-- -->

``` r
plot_temp_fixed <- last_plot()

#joins the two graphs (troops and temperature together with specified dimensions)
grid.arrange(plot_troops_cities_fixed, plot_temp_fixed, nrow=2, heights=c(3.5, 1.2))
grid.rect(width = .99, height = .99, gp = gpar(lwd = 2, col = "gray", fill = NA))
```

![](HW1_files/figure-gfm/unnamed-chunk-13-7.png)<!-- -->

From the guide, I changed the colors of the top and bottom plots (troops
and temperatures).
