FROM python:3.9-slim

CMD sh -c "\
mkdir -p /app/mirai/config/Console \
&& \
\
printf '\
accounts:\n\
  -\n\
    account: $QQ\n\
    password:\n\
      kind: PLAIN\n\
      value: $QQ_PASS\n\
    configuration:\n\
      protocol: $DEVICE\n\
' > /app/mirai/config/Console/AutoLogin.yml \
&& \
\
mkdir -p /app/mirai/config/net.mamoe.mirai-api-http \
&& \
\
printf '\
adapters:\n\
  - http\n\
  - ws\n\
debug: false\n\
enableVerify: false\n\
verifyKey: $API_KEY\n\
singleMode: false\n\
cacheSize: 4096\n\
persistenceFactory: \"built-in\"\n\
adapterSettings:\n\
  http:\n\
    host: mirai\n\
    port: 8080\n\
    cors: [\"*\"]\n\
    unreadQueueMaxSize: 100\n\
  ws:\n\
    host: mirai\n\
    port: 8080\n\
    reservedSyncId: -1\n\
' > /app/mirai/config/net.mamoe.mirai-api-http/setting.yml \
&& \
\
mkdir -p /app/chatgpt \
&& \
\
printf '\
{\n\
    \"mirai\": {\n\
        \"qq\": $QQ,\n\
        \"api_key\": \"$API_KEY\",\n\
        \"http_url\": \"http://mirai:8080\",\n\
        \"ws_url\": \"http://mirai:8080\"\n\
    },\n\
    \"openai\": {\n\
        \"session_token\": \"$SESSION_TOKEN\"\n\
    },\n\
    \"text_to_image\": {\n\
        \"font_size\": 30,\n\
        \"width\": 700,\n\
        \"font_path\": \"fonts/sarasa-mono-sc-regular.ttf\",\n\
        \"offset_x\": 50,\n\
        \"offset_y\": 50\n\
    }\n\
}\n\
' > /app/chatgpt/config.json"
