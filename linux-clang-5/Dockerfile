ARG REV=latest
FROM mbgl/${REV}:linux

# --------------------------------------------------------------------------------------------------
# Install common packages

COPY *.list /etc/apt/sources.list.d/
COPY *.gpg /tmp/
RUN set -eu \
 && (find /tmp/*.gpg | xargs -n1 apt-key add) \
 && rm /tmp/*.gpg

RUN set -eu \
 && apt-get update \
 && apt-get -y install clang-5.0 \
 && rm -rf /var/lib/apt/lists/*

# --------------------------------------------------------------------------------------------------
# Set environment variables

ENV CC="clang-5.0" \
    CXX="clang++-5.0"
