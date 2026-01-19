# Script: Survey Data Cleaning Utilities
# Author: Dipanjan Adhikary
# Description: Helper functions to clean raw survey datasets (e.g., DHS, MICS)
# Dependencies: tidyverse

library(tidyverse)

# Standardize Column Names
# Converts all column names to lowercase snake_case for consistency
# @param data A dataframe
# @return A dataframe with cleaned names
clean_survey_names <- function(data) {
  data %>%
    rename_with(~ tolower(gsub("[.]", "_", .x))) %>%
    rename_with(~ gsub("\\s+", "_", .x))
}

# Recode Missing Values
# Converts common survey codes for "Don't Know" or "Refused" to NA
# @param x A vector or column
# @param missing_codes A vector of values to be treated as NA (default: 98, 99)
recode_survey_missing <- function(x, missing_codes = c(98, 99, "DK", "Refused")) {
  x[x %in% missing_codes] <- NA
  return(x)
}

# Example Usage (Commented out):
# cleaned_df <- raw_data %>%
#   clean_survey_names() %>%
#   mutate(age = recode_survey_missing(age, c(999)))
