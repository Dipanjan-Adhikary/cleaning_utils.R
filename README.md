# Function to clean column names
clean_survey_names <- function(data) {
  janitor::clean_names(data)
}
