FROM node:14.15.1-alpine

WORKDIR /opt/otterscan

RUN apk add --no-cache git && git clone  --recurse-submodules -j8 https://github.com/androolloyd/otterscan.git . \
&& npm install && npm run build
