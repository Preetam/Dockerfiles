FROM ubuntu:16.04

# gcc for cgo
RUN apt-get update && apt-get install -y --no-install-recommends \
#		g++ \
#		gcc \
#		libc6-dev \
		make \
		pkg-config \
		curl \
	&& rm -rf /var/lib/apt/lists/*

ENV GOLANG_VERSION 1.8.3
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go$GOLANG_VERSION.linux-amd64.tar.gz
ENV GOLANG_DOWNLOAD_SHA256 1862f4c3d3907e59b04a757cfda0ea7aa9ef39274af99a784f5be843c80c6772

RUN curl -k -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz \
	&& echo "$GOLANG_DOWNLOAD_SHA256  golang.tar.gz" | sha256sum -c - \
	&& tar -C /usr/local -xzf golang.tar.gz \
	&& rm golang.tar.gz

RUN apt-get update && apt-get install -y npm nodejs-legacy python-pip

RUN npm install -g uglifyjs clean-css-cli

RUN pip install boto3==1.3.0

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH
