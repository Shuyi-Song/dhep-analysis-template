FROM docker.io/library/ubuntu:latest

ENV R_VERSION="devel"
ENV R_HOME="/usr/local/lib/R"
ENV TZ="Etc/UTC"

COPY scripts/install_R_source.sh /rocker_scripts/install_R_source.sh
RUN /rocker_scripts/install_R_source.sh

ENV CRAN="https://cloud.r-project.org"
ENV LANG=en_US.UTF-8

COPY scripts/bin/ /rocker_scripts/bin/
COPY scripts/setup_R.sh /rocker_scripts/setup_R.sh
RUN /rocker_scripts/setup_R.sh

CMD ["R"]

COPY scripts /rocker_scripts

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
FROM rocker/r-ver:4
RUN /rocker_scripts/install_quarto.sh
