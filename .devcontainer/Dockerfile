# [Choice] Node.js version (use -bullseye variants on local arm64/Apple Silicon): 18, 16, 14, 18-bullseye, 16-bullseye, 14-bullseye, 18-buster, 16-buster, 14-buster
ARG VARIANT=16-bullseye
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:0-${VARIANT}

# [Optional] Uncomment this section to install additional OS packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends chromium \
# Clean up
   && apt-get autoremove -y \
   && apt-get clean -y \
   && rm -rf /var/lib/apt/lists/*

# [Optional] Uncomment if you want to install an additional version of node using nvm
# ARG EXTRA_NODE_VERSION=10
# RUN su node -c "source /usr/local/share/nvm/nvm.sh && nvm install ${EXTRA_NODE_VERSION}"

# Install gauge and gauge plugins
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN curl -SsL https://downloads.gauge.org/stable | sh \
    && su node -c "gauge install html-report" \
    && su node -c "gauge install screenshot" \
    && su node -c "gauge install js"

# [Optional] Uncomment if you want to install more global node modules
RUN su node -c "npm install -g @stoplight/prism-cli"
