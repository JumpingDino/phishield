FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

RUN apt-get update \
  && apt-get install -y build-essential git dnsutils net-tools iputils-ping netcat libcurl4-openssl-dev libssl-dev socat ca-certificates curl gnupg

RUN curl -fsSL https://deb.nodesource.com/setup_lts.x | bash - \
  && apt-get install -y nodejs \
  && corepack enable

RUN npm install -g npm@latest

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg \
  && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null \
  && apt-get update \
  && apt-get install -y docker-ce

RUN apt-get install -y python3 python3-pip python3-dev python3-venv python-is-python3 libnss3

RUN curl -sSL https://install.python-poetry.org | POETRY_HOME=/home/vscode/.poetry python -
RUN cp /home/vscode/.poetry/bin/poetry /usr/local/bin/

RUN pip install hatch

RUN curl -SL https://github.com/docker/compose/releases/download/v2.23.0/docker-compose-linux-x86_64 -o /usr/bin/docker-compose \
  && chmod +x /usr/bin/docker-compose \
  && usermod -aG docker vscode

RUN npm install --global pm2

RUN curl -1sLf 'https://dl.cloudsmith.io/public/evilmartians/lefthook/setup.deb.sh' | sudo -E bash \
  && sudo apt install lefthook

RUN chown -R vscode:vscode /home/vscode