# Base image with R version 4 from Rocker's GitHub Container Registry
FROM ghcr.io/rocker-org/devcontainer/r-ver:4

# Install system dependencies and Git for version control
RUN apt-get update && apt-get install -y \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev \
    git \
    python3 \
    python3-pip

# Install R packages for data analysis, causal machine learning, and reporting
RUN R -e "install.packages(c( \
    'tidyverse', 'haven', 'knitr', 'rmarkdown', 'quarto', 'renv', \
    'grf', 'xgboost', 'caret', 'SuperLearner', 'MatchIt', 'lmtest', \
    'sandwich', 'broom', 'ggiraph', 'data.table', 'plm', 'did', \
    'CausalImpact', 'glmnet', 'ggplot2', 'stargazer', 'gt' , 'dplyr', 'modelsummary' ,\
    'gtsummary', 'estimatr', 'fixest', 'marginaleffects'
    ), repos='https://cran.rstudio.com/')"

# Add any additional Python packages for data analysis if necessary
RUN pip3 install numpy pandas scikit-learn matplotlib

# Add any other customizations here

# Expose port 8787 for RStudio Server access
EXPOSE 8787
