ARG NODE_VERSION=26.10.0
ARG NODE_ENV=development

FROM node:${NODE_VERSION}-bookworm

# Install basic development tools
RUN apt-get update \
	&& apt-get install --yes --no-install-recommends zstd less man-db sudo \
	&& rm -rf /var/lib/apt/lists/*

# Install Ollama
RUN curl --fail --show-error --location --retry 5 --retry-all-errors \
	--retry-delay 2 https://ollama.com/install.sh | sh


# Install dotenvx
RUN curl -sfS https://dotenvx.sh/install.sh | sh



# Ensure default `node` user has access to `sudo`
ARG USERNAME=node
RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Set `DEVCONTAINER` environment variable to help with orientation
ENV DEVCONTAINER=true

# Set NODE_ENV from build argument (make it available for RUN commands)
ENV NODE_ENV=${NODE_ENV}
