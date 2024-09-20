FROM ghcr.io/rocker-org/devcontainer/r-ver:4

# Install system dependencies if any
RUN apt-get update && apt-get install -y \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev

# Install R packages
RUN R -e "install.packages(c('tidyverse', 'haven', 'knitr', 'rmarkdown', 'quarto'), repos='https://cran.rstudio.com/')"

# Add any other customizations here