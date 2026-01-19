library(tidyverse)

Function 1: Clean Column Names
clean_survey_names <- function(data) {
  data %>%
    rename_with(~ tolower(gsub("[.]", "_", .x))) %>%
    rename_with(~ gsub("\\s+", "_", .x))
}

Function 2: Recode Missing Values
recode_survey_missing <- function(x) {
  x[x %in% c(98, 99, "DK", "Refused")] <- NA
  return(x)
}
