FROM ubuntu

RUN apt-get update
RUN apt-get install -y python3.8
RUN apt install -y curl gpg
RUN curl https://repo.anaconda.com/pkgs/misc/gpgkeys/anaconda.asc | gpg --dearmor > conda.gpg
RUN install -o root -g root -m 644 conda.gpg /usr/share/keyrings/conda-archive-keyring.gpg
RUN gpg --keyring /usr/share/keyrings/conda-archive-keyring.gpg --no-default-keyring --fingerprint 34161F5BF5EB1D4BFBBB8F0A8AEB4F8B29D82806
RUN echo "deb [arch=amd64 signed-by=/usr/share/keyrings/conda-archive-keyring.gpg] https://repo.anaconda.com/pkgs/misc/debrepo/conda stable main" > /etc/apt/sources.list.d/conda.list
RUN echo "deb [arch=amd64 signed-by=/usr/share/keyrings/conda-archive-keyring.gpg] https://repo.anaconda.com/pkgs/misc/debrepo/conda stable main" | tee -a /etc/apt/sources.list.d/conda.list
RUN apt-get update
RUN apt install conda
ENV PATH=$PATH:/opt/conda/bin
RUN . /opt/conda/etc/profile.d/conda.sh && conda activate base
RUN conda install -n base -c conda-forge mamba
RUN mamba install -c conda-forge -c bioconda -y -n base snakemake

ENTRYPOINT ["snakemake"]
