FROM python:3.9-slim

ARG BOT_URL=https://github.com/lss233/chatgpt-mirai-qq-bot
ARG BOT_PATH=/app

ARG TSINGHUA_SOURCE=false

ADD ./tsinghua.sources.list /etc/apt/tsinghua.sources.list

WORKDIR $BOT_PATH

ENV DEBIAN_FRONTEND=noninteractive

RUN if [ $TSINGHUA_SOURCE = true ]; then \
        cp /etc/apt/tsinghua.sources.list /etc/apt/sources.list; \
    fi

RUN apt-get update && \
    apt install software-properties-common apt-transport-https wget ca-certificates gnupg2 -yq && \
    wget -qO /usr/share/keyrings/xpra-2022.gpg https://xpra.org/xpra-2022.gpg  && \
    echo deb [arch=amd64,arm64 signed-by=/usr/share/keyrings/xpra-2022.gpg] https://xpra.org/ bullseye main |  tee /etc/apt/sources.list.d/xpra.list && \
    wget -O- /usr/share/keyrings/google-chrome.gpg https://dl.google.com/linux/linux_signing_key.pub | gpg --dearmor --yes -o /usr/share/keyrings/google-chrome.gpg  && \
    echo deb [arch=amd64,arm64 signed-by=/usr/share/keyrings/google-chrome.gpg] http://dl.google.com/linux/chrome/deb/ stable main | tee -a /etc/apt/sources.list.d/google-chrome.list && \
    apt-get update && \
    apt install --no-install-recommends xpra xvfb libgl1-mesa-dri xauth google-chrome-stable xterm -yq
    
RUN apt-get install git -yq && \
    git clone $BOT_URL . && \
    pip install -r requirements.txt
    
RUN set -eux; \
    apt-get clean; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \
    rm -rf /var/lib/apt/lists/*

RUN cp docker/xpra.conf /etc/xpra/xpra.conf
RUN cp docker/start.sh ./start && chmod +x start

RUN ln -sf /proc/1/fd/1 /tmp/log.txt

CMD /app/start
