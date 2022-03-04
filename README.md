# r-workshop
Repo for R workshop
This Repo is for my R learning workshop
We use the following data from the Santa Barbara Coastal Term Ecological Research and National  Oceanic and Atmospheric Administration in our analyses
#load tidyverse and readxl
library(tidyverse)
library(readxl)
library(here) #here() starts at Y:/R/r-workshop
#load excel file from data folder
ca_np <- read_csv(here("data", "ca_np.csv"))
ci_np <- read_excel(here("data", "ci_np.xlsx"))
#create a line graph of visitors to Channel Islands National Park
ggplot(data = ci_np, aes(x = year, y = visitors)) +
  geom_line()
#store the first line as object gg_base so that we don’t need to retype it each time:
gg_base <- ggplot(data = ci_np, aes(x = year, y = visitors))
#e.g.use the stored variable and change plot style
gg_base +
  geom_point()
#changing the aesthetics
gg_base +
  geom_line(
    color = "tan2",
    linetype = "solid"
  )
#changing the aesthetics based on values
gg_base + 
  geom_point(
    aes(size = visitors,
        color = visitors),
    alpha = 0.5
  )
#adding title and axis labels
gg_base +
  geom_line(linetype = "dotted") +
  theme_minimal() +
  labs(
    x = "Year",
    y = "Annual park visitors",
    title = "Channel Islands NP Visitation",
    subtitle = "(1963 - 2016)"
  )
#combining two graph components
gg_base +
  geom_line(color = "black") +
  geom_point(color = "orange",
             aes(size = year),
             alpha = 0.5)
#multiple series
ggplot(data = ca_np, aes(x = year, y = visitors, group = park_name)) +
  geom_line()  
  gg_np <- ggplot(data = ca_np, aes(x = year, y = visitors, group = park_name))
#faceting groups
gg_np +
  geom_line(show.legend = FALSE) +
  theme_light() + 
  labs(x = "year", y = "annual visitors") +
  facet_wrap(~ park_name)
#export graph
ggsave(here("figures", "np_graph.jpg"), dpi = 180, width = 8, height = 7)