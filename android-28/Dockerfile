FROM openjdk:8-alpine
LABEL maintainer="Goooseman <goooseman@me.com>"

ENV SDK_TOOLS "4333796"
ENV BUILD_TOOLS "28.0.3"
ENV TARGET_SDK "28"
ENV ANDROID_HOME "/opt/sdk"
ENV GLIBC_VERSION "2.28-r0"
ENV NODE_VERSION "v10.14.2"
ENV NPM_VERSION "6.4.1"
ENV NODE_CONFIG_FLAGS "--fully-static"
ENV NODE_DEL_PKGS="libstdc++"
ENV NODE_RM_DIRS=/usr/include

# Install nodejs
RUN apk add --no-cache curl make gcc g++ python linux-headers binutils-gold gnupg libstdc++ && \
  for server in ipv4.pool.sks-keyservers.net keyserver.pgp.com ha.pool.sks-keyservers.net; do \
    gpg --keyserver $server --recv-keys \
      94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
      B9AE9905FFD7803F25714661B63B535A4C206CA9 \
      77984A986EBC2AA786BC0F66B01FBB92821C587A \
      71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
      FD3A5288F042B6850C66B31F09FE44734EB7990E \
      8FCCA13FEF1D0C2E91008E09770F7A9A5AE15600 \
      C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
      DD8F2338BAE7501E3DD5AC78C273792F7D83545D && break; \
  done && \
  curl -sfSLO https://nodejs.org/dist/${NODE_VERSION}/node-${NODE_VERSION}.tar.xz && \
  curl -sfSL https://nodejs.org/dist/${NODE_VERSION}/SHASUMS256.txt.asc | gpg --batch --decrypt | \
    grep " node-${NODE_VERSION}.tar.xz\$" | sha256sum -c | grep ': OK$' && \
  tar -xf node-${NODE_VERSION}.tar.xz && \
  cd node-${NODE_VERSION} && \
  ./configure --prefix=/usr ${NODE_CONFIG_FLAGS} && \
  make -j$(getconf _NPROCESSORS_ONLN) && \
  make install && \
  cd / && \
  if [ -z "$NODE_CONFIG_FLAGS" ]; then \
    if [ -n "$NPM_VERSION" ]; then \
      npm install -g npm@${NPM_VERSION}; \
    fi; \
    find /usr/lib/node_modules/npm -name test -o -name .bin -type d | xargs rm -rf; \
  fi && \
  apk del curl make gcc g++ python linux-headers binutils-gold gnupg ${NODE_DEL_PKGS} && \
  rm -rf ${NODE_RM_DIRS} /node-${NODE_VERSION}* /usr/share/man /tmp/* /var/cache/apk/* \
    /root/.npm /root/.node-gyp /root/.gnupg /usr/lib/node_modules/npm/man \
	/usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html /usr/lib/node_modules/npm/scripts

# Install ruby
RUN apk add --update --no-cache git ruby ruby-rdoc ruby-dev ruby-irb g++ make

# Install required dependencies
RUN apk add --no-cache --virtual=.build-dependencies wget unzip ca-certificates bash && \
	wget https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub -O /etc/apk/keys/sgerrand.rsa.pub && \
	wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk -O /tmp/glibc.apk && \
	wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-bin-${GLIBC_VERSION}.apk -O /tmp/glibc-bin.apk && \
	apk add --no-cache /tmp/glibc.apk /tmp/glibc-bin.apk && \
	rm -rf /tmp/* && \
	rm -rf /var/cache/apk/*

# Download and extract Android Tools
RUN wget http://dl.google.com/android/repository/sdk-tools-linux-${SDK_TOOLS}.zip -O /tmp/tools.zip && \
	mkdir -p ${ANDROID_HOME} && \
	unzip /tmp/tools.zip -d ${ANDROID_HOME} && \
	rm -v /tmp/tools.zip

# Install SDK Packages
RUN mkdir -p /root/.android/ && touch /root/.android/repositories.cfg && \
	yes | ${ANDROID_HOME}/tools/bin/sdkmanager "--licenses" && \
	${ANDROID_HOME}/tools/bin/sdkmanager "--update" && \
	${ANDROID_HOME}/tools/bin/sdkmanager "build-tools;${BUILD_TOOLS}" "platform-tools" "platforms;android-${TARGET_SDK}" "extras;android;m2repository" "extras;google;google_play_services" "extras;google;m2repository" "emulator"

# Install bundler and fastlane (even if you use different fastlane version, it is better to preinstall it to have all dependency gems ready)
RUN gem install bundle fastlane