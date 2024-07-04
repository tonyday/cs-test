FROM ruby:3

ARG USERNAME=tonydev
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Install basic development tools
RUN apt update && \
    apt install -y \
    less \
    man-db  \
    sudo \
    vim \
    zsh

# Set up unprivileged local user
RUN groupadd --gid $USER_GID $USERNAME \
    && groupadd bundler \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME --shell /bin/bash --groups bundler \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Set unprivileged user as default user
USER $USERNAME

RUN curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh

# Keep the container alive for eva
ENTRYPOINT ["tail", "-f", "/dev/null"]
