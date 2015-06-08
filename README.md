# iotivity-docker-ci

Evaluating docker for build.iotivity.org

## Pulldown Libraries
Use either rsync or cp.

### rsync
```
mkdir iotivity-extlibs-03272015/
gsutil -m rsync -d -r -p gs://iotivity-extlibs/iotivity-extlibs-03272015/ iotivity-extlibs-03272015/
chmod -R +x iotivity-extlibs-03272015/
```

### cp
```
gsutil cp gs://iotivity-extlibs/extlibs-03272015.tar.gz .
gsutil cp gs://iotivity-extlibs/extlibs-03272015.md5 .
md5sum extlibs-03272015.tar.gz extlibs-03272015.md5
tar -xvf extlibs-03272015.tar.gz
```

## Build the Docker Image
```
docker build -t iotivity/build .
```

## Run the Docker Image
```
export WORKSPACE="/path/to/iotiviy/repo"
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

