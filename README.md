# hello-wolfi

## Setup

Install Docker https://docs.docker.com/get-docker/.

```
git clone https://github.com/jamonation/hello-wolfi.git

cd hello-wolfi

docker pull ghcr.io/wolfi-dev/sdk
```

## Scanning

```
grype node

grype cgr.dev/chainguard/node
```

## Docker

```
cd python-web-app-docker

docker build -t wolfi/hello-python .

docker run --rm -i -t -p 8080:8080 wolfi/hello-python:latest
```

## Wolfi

```
cd ../python-web-app-wolfi

docker build -t wolfi/hello-wolfi .

docker run --rm -i -t -p 8080:8080 wolfi/hello-wolfi:latest
```

## apko + melange

```
cd ../python-web-app-apko-melange

docker run --rm -i -t -v $PWD:/work --privileged ghcr.io/wolfi-dev/sdk

cd /work

melange keygen

melange build --arch host --signing-key melange.rsa

apko build --arch host --debug apko.yaml wolfi/hello-apko-melange image.tar --keyring-append melange.rsa.pub

exit

docker load < image.tar

docker run --rm -i -t -p 8080:8080 wolfi/hello-apko-melange:latest-amd64
docker run --rm -i -t -p 8080:8080 wolfi/hello-apko-melange:latest-aarch64
```
