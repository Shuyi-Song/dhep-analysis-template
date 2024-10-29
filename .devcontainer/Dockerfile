# Base Dev Container Image for R with Tidyverse. More info: https://github.com/rocker-org/devcontainer-images/pkgs/container/devcontainer%2Ftidyverse
# Available R versions: 4, 4.1, 4.0
ARG VARIANT="4.2"
FROM ghcr.io/rocker-org/devcontainer/tidyverse:${VARIANT}

# Install required R packages
RUN install2.r --error --skipinstalled -n -1 \
        statip \
        patchwork \
        paletteer \
        here \
        doParallel \
        janitor \
        vip \
        ranger \
        palmerpenguins \
        skimr \
        nnet \
        kernlab \
        plotly \
        factoextra \
        cluster \
        tidymodels \
        markdown \
        ottr \
        tidyverse \
        haven \
        knitr \
        rmarkdown \
        quarto \
        renv \
        grf \
        xgboost \
        caret \
        SuperLearner \
        MatchIt \
        lmtest \
        sandwich \
        broom \
        ggiraph \
        data.table \
        plm \
        did \
        CausalImpact \
        glmnet \
        ggplot2 \
        stargazer \
        gt \
        dplyr \
        modelsummary \
        gtsummary \
        estimatr \
        fixest \
        marginaleffects \
    && rm -rf /tmp/downloaded_packages \
    && R -q -e 'remotes::install_github("https://github.com/dcomtois/summarytools/tree/0-8-9")'

# Install additional Dev Container features
# Quarto CLI for R Markdown documents
RUN apt-get update && \
    apt-get install -y --no-install-recommends quarto-cli && \
    rm -rf /var/lib/apt/lists/*

# JupyterLab installation with IRkernel
RUN R -e "install.packages('IRkernel')" && \
    R -e "IRkernel::installspec(user = FALSE)" && \
    pip install jupyterlab

# Setup renv cache
ENV RENV_PATHS_CACHE="/renv/cache"
VOLUME /renv/cache

# Copy requirements.txt for Python packages
COPY requirements.txt /tmp/pip-tmp/
RUN python3 -m pip --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt

# Start RStudio Server as a post-attach command
CMD ["sudo", "rstudio-server", "start"]
