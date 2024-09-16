# Use the official VS Code R dev container as the base image
FROM rocker/r-ver:4.3.1

# Install basic utilities
RUN apt-get update && apt-get install -y \
    sudo \
    wget \
    git \
    locales \
    && rm -rf /var/lib/apt/lists/*

# Set locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Create a non-root user and add to sudoers
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Install Python and Conda
RUN apt-get update && apt-get install -y python3 python3-pip

# Install Miniconda
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /tmp/miniconda.sh && \
    bash /tmp/miniconda.sh -b -p /opt/conda && \
    rm /tmp/miniconda.sh && \
    chown -R $USERNAME /opt/conda

ENV PATH="/opt/conda/bin:${PATH}"

# Install R packages
RUN R -e "install.packages(c('languageserver', 'httpgd', 'jsonlite', 'remotes'))"

# Install renv
RUN R -e "install.packages('renv')"

# Install Quarto CLI
RUN wget https://github.com/quarto-dev/quarto-cli/releases/download/v1.3.433/quarto-1.3.433-linux-amd64.deb \
    && dpkg -i quarto-1.3.433-linux-amd64.deb \
    && rm quarto-1.3.433-linux-amd64.deb

# Install Python packages
RUN pip install --upgrade pip

# Set the user
USER $USERNAME

# Set the working directory
WORKDIR /workspaces/${localWorkspaceFolderBasename}

# Initialize conda for the vscode user
RUN conda init bash

# Ensure conda is initialized
SHELL ["/bin/bash", "-c"]

# Install Conda environments
COPY envs/ /tmp/envs/
RUN conda env create -f /tmp/envs/r_env.yaml && \
    conda env create -f /tmp/envs/quarto_env.yaml && \
    conda clean -a

# Activate default environment
RUN echo "conda activate r_env" >> ~/.bashrc

# Copy the project files
COPY . /workspaces/${localWorkspaceFolderBasename}

# Restore R packages with renv
RUN R -e "renv::restore()"

# Expose ports (optional)
EXPOSE 8787

# Command to execute when the container starts
CMD [ "sleep", "infinity" ]