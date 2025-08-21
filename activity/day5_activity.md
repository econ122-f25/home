Day 5: Data Visualization In-Class Activity
================
Econ 122
2025-08-21

## Introduction 🚀

Welcome to your Day 5 in-class activity! Today, you’ll apply the data
visualization concepts we’ve covered, focusing on `ggplot2` for common
plots and basic geographic mapping. This activity is designed to be
self-directed and should take approximately **40 minutes**.

Work through the exercises at your own pace. If you get stuck, refer
back to the lecture slides or use R’s help documentation
(`?function_name`). Don’t worry about getting everything perfect; the
goal is to practice and explore!

------------------------------------------------------------------------

## Setup: Load Libraries and Data 🛠️

First, ensure you have all the necessary packages installed. If you
haven’t already, run `install.packages()` for `ggplot2`, `sf`,
`rnaturalearth`, `rnaturalearthdata`, and `scales`. For filtering data,
you’ll also need `dplyr`.

Then, run the following R chunk to load the libraries and the `mtcars`
and `economics` datasets, which we’ll use for plotting. We’ll also load
US states and river data for the mapping section.

``` r
# Set output width for better readability in Markdown
options(htmltools.dir.version = FALSE, width = 80)

# Load essential libraries
library(ggplot2)
library(sf)
library(rnaturalearth)
library(rnaturalearthdata) # This package provides the data for ne_countries() and other Natural Earth data
library(scales) # For formatting numbers in plots
library(dplyr) # For data manipulation, including filtering

# Load built-in datasets
data(mtcars)
data(economics)

# Load US map data for mapping exercises using ne_states
# Get states/provinces data for the United States using ne_download()
all_states_high_res <- ne_download(
  scale = 10,
  type = "states",
  category = "cultural",
  returnclass = "sf"
)

# Define the states to exclude (Alaska and Hawaii)
exclude_states <- c("Alaska", "Hawaii")

# Filter for the United States based on the 'admin' column (country name)
us_map_full <- all_states_high_res[all_states_high_res$admin == "United States of America", ]

# Filter for the continental United States based on the 'name' column (state name)
us_map <- us_map_full[!us_map_full$name %in% exclude_states, ]

#download state population data
population_data_raw <- read.csv('https://raw.githubusercontent.com/mgelman/data/master/ACS2016.csv')

# Clean and prepare the population data (need to rename variables to match map data)
us_population_data <- population_data_raw %>% select(name = region, population = PopSize)

# Merge population data into the us_map sf object
us_map <- left_join(us_map, us_population_data, by = "name")
```

------------------------------------------------------------------------

## Part 1: `ggplot2` Basics (20 minutes) 📊

In this section, you’ll create various common plot types using `ggplot2`
and practice mapping aesthetics.

### Exercise 1.1: Scatter Plot - Engine Displacement vs. Horsepower

Create a scatter plot showing the relationship between `disp` (engine
displacement) and `hp` (horsepower) from the `mtcars` dataset.

- Use `geom_point()`.
- Add appropriate `labs()` for title and axis labels.
- Use `theme_classic()`.

``` r
# Your code here for Exercise 1.1
```

### Exercise 1.2: Histogram - Rear Axle Ratio Distribution

Create a histogram of `drat` (rear axle ratio) from the `mtcars`
dataset.

- Set the `binwidth` to 0.2.
- Choose a `fill` color and `color` for the borders.
- Add a title and axis labels.

``` r
# Your code here for Exercise 1.2
```

### Exercise 1.3: Bar Chart - Engine Type and Transmission

Create a bar chart showing the count of cars based on `vs` (engine type:
V-engine or straight engine) and `am` (transmission type: automatic or
manual) in `mtcars`.

- Map `vs` to the x-axis (as a factor).
- Map `am` to the `fill` aesthetic.
- Use `position = "stack"` to stack bars.
- Add a title and axis labels.
- Customize fill colors using `scale_fill_manual()`.

``` r
# Your code here for Exercise 1.3
```

### Exercise 1.4: Line Plot - Personal Savings Rate Over Time

Create a line plot of `psavert` (personal savings rate) over `date` from
the `economics` dataset.

- Add a `geom_line()`.
- Overlay a smooth trend line using
  `geom_smooth(method = "gam", se = TRUE)` (Generalized Additive Model).
- Add appropriate titles and labels.

``` r
# Your code here for Exercise 1.4
```

------------------------------------------------------------------------

## Part 2: Geographic Mapping (15 minutes) 🗺️

Now, let’s explore basic static mapping using `sf` and `ggplot2`,
focusing on the **Continental United States**.

### Exercise 2.1: Basic Continental US Map

Create a basic map of the Continental United States using the `us_map`
object loaded in the setup.

- Use `geom_sf()`.
- Set `fill` to a light color (e.g., “lightskyblue”) and `color` to a
  darker outline (e.g., “darkblue”).
- Use `theme_void()` for a clean map background.
- Add a title.

``` r
# Your code here for Exercise 2.1
```

### Exercise 2.2: Choropleth Map of Continental US State Population

Create a choropleth map of the estimated US state population for the
continental US using the **`population`** column from the `us_map`
object. Population data is often skewed, so a logarithmic transformation
can help visualize variations more clearly.

- Map `population` to the `fill` aesthetic.
- Use `scale_fill_viridis_c(option = "cividis", trans = "log10")` for
  the color scale.
- Add `labels = scales::comma` to the scale for readable numbers.
- Include a clear title and legend title.

``` r
# Your code here for Exercise 2.2
```

### Exercise 2.3: Adding Major Continental US Rivers to the Map

Overlay major rivers onto your Continental US states map to visualize
linear spatial features within the country.

- Recreate a basic Continental US map (similar to 2.1).
- **Download world river data using `ne_download()` and filter it to
  Continental US state boundaries.**
- Add a `geom_sf()` layer for the river data.
- Choose a distinct `color` and `size` for the river lines.

``` r
# Hints for downloading and filtering river data:
# 1. Use `ne_download()` from `rnaturalearth`. Look for `type = "rivers_lake_centerlines"` and `category = "physical"`. Remember to set `returnclass = "sf"`.
#    Assign the result to a variable like `world_rivers_downloaded`.

# 2. To filter these global rivers to only the continental US, use `st_intersection()` from `sf`.
#    This function takes two spatial objects and returns their overlapping parts.
#    You'll intersect your `world_rivers_downloaded` with the `us_map` object (already loaded).
#    Assign the result to a variable like `us_rivers_filtered`.

# Your code here for Exercise 2.3
# world_rivers_downloaded <- ...
# us_rivers_filtered <- ...
```

------------------------------------------------------------------------

## Wrap-up & Discussion Points 💬

Take a few minutes to review your plots and consider the following
questions. We’ll discuss these as a class.

1.  Which plot type did you find most challenging or confusing to create
    with the new examples, and why?
2.  How did using different aesthetic mappings (like `fill` for
    engine/transmission types) help you understand the car data better?
3.  For the choropleth map of **Continental US State Population**, did
    the `cividis` color scheme with the logarithmic transformation make
    the variations clearer? Why or why not?
4.  What’s one new `ggplot2` function or concept you learned today that
    you think will be most useful for your future data analysis?
5.  Think of a real-world dataset you’ve encountered. Which of the
    visualization techniques practiced today would be most suitable for
    exploring it, and and why?

------------------------------------------------------------------------
