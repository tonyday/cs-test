FROM ruby:3

ARG USERNAME=devcontainer
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Install basic development tools
RUN apt update && \
    apt install -y \
    less \
    man-db  \
    postgresql  \
    sudo \
    vim \
    zsh

RUN service postgresql start
ENV DB_CMD="create user ${USERNAME} with createdb;"
RUN su postgres -c 'psql -c ${DB_CMD}'

RUN gem update --system

# Set up unprivileged local user
RUN groupadd --gid $USER_GID $USERNAME \
    && groupadd bundler \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME --shell /bin/bash --groups bundler \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Set unprivileged user as default user
USER $USERNAME

RUN curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh

# Set `DEVCONTAINER` environment variable to help with orientation
ENV DEVCONTAINER=true
