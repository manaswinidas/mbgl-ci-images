ARG REV=latest
FROM mbgl/${REV}:java

ENV ANDROID_NDK_HOME=/android/sdk/ndk-bundle \
    ANDROID_HOME=/android/sdk \
    GRADLE_OPTS=-Dorg.gradle.daemon=false

# --------------------------------------------------------------------------------------------------
# Install Android SDK

WORKDIR /android/sdk

# Use most recent version from https://developer.android.com/studio/index.html#command-tools
# and update the checksum.
RUN set -eu \
 && curl -L --retry 3 https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip -o tools.zip \
 && (echo "444e22ce8ca0f67353bda4b85175ed3731cae3ffa695ca18119cbacef1c1bea0  tools.zip" | sha256sum -c) \
 && unzip -q tools.zip && rm tools.zip

# --------------------------------------------------------------------------------------------------
# Install Android NDK

# Use desired version from https://developer.android.com/ndk/downloads/index.html
# and update the checksum.
RUN set -eu \
 && curl -L --retry 3 https://dl.google.com/android/repository/android-ndk-r17-linux-x86_64.zip -o ndk.zip \
 && (echo "1d886a64483adf3f3a3e3aaf7ac5084184006ac7  ndk.zip" | sha1sum -c) \
 && unzip -q ndk.zip && rm ndk.zip && mv android-ndk-r* ndk-bundle

# --------------------------------------------------------------------------------------------------
# Install dependencies and build tools

RUN set -eu \
 && mkdir -p "${ANDROID_HOME}/licenses" \
 && echo "d56f5187479451eabf01fb78af6dfcb131a6481e" > "${ANDROID_HOME}/licenses/android-sdk-license" \
 && tools/bin/sdkmanager \
        "platform-tools" \
        "platforms;android-26" \
        "build-tools;26.0.3" \
        "platforms;android-27" \
        "build-tools;27.0.3" \
        "platforms;android-P" \
        "build-tools;28.0.0-rc2" \
        "extras;android;m2repository" \
        "patcher;v4" \
        "extras;google;m2repository" \
        "extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2" \
        "cmake;3.6.4111459" \
 && rm -rf "${ANDROID_HOME}/licenses"

WORKDIR /src
