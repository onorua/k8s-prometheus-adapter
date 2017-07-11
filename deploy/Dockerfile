FROM golang:1.8 
COPY . /go/src/github.com/directxman12/k8s-prometheus-adapter
RUN curl https://glide.sh/get | sh \
    &&  cd /go/src/github.com/directxman12/k8s-prometheus-adapter \
    && glide install -v
RUN CGO_ENABLED=0 go build -a -tags netgo -o /build/adapter github.com/directxman12/k8s-prometheus-adapter/cmd/adapter

FROM BASEIMAGE
COPY --from=0 /build/adapter /
USER 1001:1001
ENTRYPOINT ["/adapter"]
