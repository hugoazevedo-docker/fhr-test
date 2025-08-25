FROM demonstrationorg/dhi-fhr-node-python-debian:22.18.0-debian13-dev_fhrcodepspace

# Fix missing ldconfig cache for VS Code Server
USER root
RUN ldconfig
USER vscode
