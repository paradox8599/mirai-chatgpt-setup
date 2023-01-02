FROM openjdk:17-jdk-alpine

ARG MCL_URL=https://github.com/iTXTech/mirai-console-loader/releases/download/v2.1.2/mcl-2.1.2.zip
ARG MCL_PATH=/mirai

WORKDIR $MCL_PATH

RUN printf "#!/bin/sh\n\
wget -O $MCL_PATH/mcl.zip $MCL_URL\n\
unzip $MCL_PATH/mcl.zip\n\
rm $MCL_PATH/mcl.zip\n\
chmod +x $MCL_PATH/mcl\n\
$MCL_PATH/mcl --update-package net.mamoe:mirai-api-http --channel stable-v2 --type plugin\n\
$MCL_PATH/mcl --update-package xyz.cssxsh.mirai:mirai-device-generator --channel stable --type plugin\n\
" > /bin/mirai_dl && chmod a+x /bin/mirai_dl

RUN printf "#!/bin/sh\n\
$MCL_PATH//mcl\n\
" > /bin/start && chmod a+x /bin/start

RUN printf "#!/bin/sh\n\
mirai_dl && start\n\
" > /bin/setup && chmod a+x /bin/setup

RUN printf "#!/bin/sh\n\
echo stop | $MCL_PATH//mcl --update\n\
" > /bin/update && chmod a+x /bin/update

RUN printf "#!/bin/sh\n\
sed 's/https:\/\/maven.aliyun.com\/repository\/public/https:\/\/repo.maven.apache.org\/maven2/g' $MCL_PATH//config.json > $MCL_PATH//config.json\n\
" > /bin/maven_apache && chmod a+x /bin/maven_apache

RUN printf "#!/bin/sh\n\
sed 's/https:\/\/repo.maven.apache.org\/maven2/https:\/\/maven.aliyun.com\/repository\/public/g' $MCL_PATH//config.json > $MCL_PATH//config.json\n\
" > /bin/maven_aliyun && chmod a+x /bin/maven_aliyun

CMD /mirai/mcl