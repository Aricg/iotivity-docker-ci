# iotivity-docker-ci

Evaluating docker for build.iotivity.org

## Clone the IoTivity Repo

```
git clone https://gerrit.iotivity.org/gerrit/iotivity /tmp/iotivity
```

## Pulldown Libraries
Use either rsync or cp.

### rsync
```
mkdir iotivity-extlibs-03272015/
gsutil -m rsync -d -r gs://iotivity-extlibs/iotivity-extlibs-03272015/ iotivity-extlibs-03272015/
chmod -R +x iotivity-extlibs-03272015/
```

### cp
```
gsutil cp gs://iotivity-extlibs/extlibs-03272015.tar.gz .
gsutil cp gs://iotivity-extlibs/extlibs-03272015.md5 .
md5sum -c extlibs-03272015.md5
tar xzf extlibs-03272015.tar.gz
```

## Build the Docker Image
```
docker build -t iotivity/build .
```

## Export the Workspace
This should be the full path to the iotivity repo.
```
export WORKSPACE="/tmp/iotivity"
```

## Run the Docker Image
```
docker run \
-v "$WORKSPACE":/root/iotivity \
-v "$PWD"/iotivity-extlibs-03272015:/root/extlibs \
-t iotivity/build
```


If you want to mess around in the container after it is built you can
jump into interactive mode.
```
docker run \
-v "$PWD"/iotivity-extlibs-03272015:/root/extlibs \
-i -t iotivity/build /bin/bash
```

TODO: Capture artifacts for valgrind results

