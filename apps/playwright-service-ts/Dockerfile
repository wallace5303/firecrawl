FROM node:18-slim

WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install

COPY . .

ENV PLAYWRIGHT_BROWSERS_PATH=/tmp/.cache

# 1. 替换 Debian 官方源为 阿里云镜像（国内稳定，解决503）
RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list.d/debian.sources \
    && apt-get update -y
    
# Install Playwright dependencies
RUN npx playwright install chromium --with-deps

RUN npm run build

ARG PORT
ENV PORT=${PORT}

EXPOSE ${PORT}

CMD [ "npm", "start" ]
