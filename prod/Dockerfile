FROM alpine:3.7

LABEL com.github.jechase.application="aws-s3-proxy" \
      com.github.jechase.usage="docker run -d -p 8080:80 -e AWS_S3_BUCKET jechas01/s3-proxy" \
      com.github.jechase.license="MIT"

ENV AWS_REGION=us-east-1 \
    APP_PORT=80

RUN apk add --no-cache ca-certificates

RUN apk --no-cache add --virtual build-dependencies gcc musl-dev go git \
    && export GOPATH=/go \
    && export PATH=$GOPATH/bin:$PATH \
    && mkdir $GOPATH \
    && chmod -R 777 $GOPATH \
    && go get -u github.com/jechase/aws-s3-proxy \
    && cd /go/src/github.com/jechase/aws-s3-proxy \
    && go build -ldflags "-s -w" \
    && mv aws-s3-proxy /usr/bin \
    && apk del --purge -r build-dependencies \
    && rm -rf /go

EXPOSE 80

CMD ["aws-s3-proxy"]
