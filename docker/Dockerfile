
FROM nvcr.io/nvidia/pytorch:22.08-py3

# Install basic packages
RUN export DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC && \
    apt-get update && \
    apt-get install -y vim git cmake tmux python3-pip;

# Install Git LFS
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash && \
    apt-get install git-lfs && \
    git lfs install;

# Install Habitat
RUN git clone --recursive https://github.com/centml/habitat && \
    pushd habitat && \
    git lfs pull && \
    popd;
    
RUN habitat/analyzer/install-dev.sh

# Install Skyline backend
RUN git clone https://github.com/CentML/skyline.git && \
    cd skyline && \
    pip install protobuf==3.18.1 && \
    pip install .;

# Install Skyline to the default location
RUN ln -s /opt/conda/bin/skyline /usr/bin/skyline;

# Install VSCode server
COPY skyline-vscode-0.0.1.vsix /workspace
RUN curl -fsSL https://code-server.dev/install.sh | sh && \
    code-server --install-extension skyline-vscode-0.0.1.vsix
COPY config.yaml /root/.config/code-server/config.yaml

# Install Jupyter
RUN pip install jupyter;
run pip install torch_tb_profiler
run pip install ipywidgets==7.7.1

RUN code-server --install-extension  ms-python.python
ADD auto_hfta-0.0.1-cp38-cp38-linux_x86_64.whl  auto_hfta-0.0.1-cp38-cp38-linux_x86_64.whl 
RUN pip install auto_hfta-0.0.1-cp38-cp38-linux_x86_64.whl && rm auto_hfta-0.0.1-cp38-cp38-linux_x86_64.whl 

# Setup demo environment
ENTRYPOINT ["bash", "entry.sh"]
