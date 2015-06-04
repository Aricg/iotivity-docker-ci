# iotivity-docker-ci

Evaluating docker for build.opnfv.org

Get libs, choose rsync or cp

rsync:
```
mkdir iotivity-extlibs-03272015/
gsutil rsync -d -r -p gs://iotivity-extlibs/iotivity-extlibs-03272015/ iotivity-extlibs-03272015/
chmod -R +x iotivity-extlibs-03272015/
```

cp:
```
gsutil cp gs://iotivity-extlibs/extlibs-03272015.tar.gz .
tar -xvf extlibs-03272015.tar.gz
```

Run build:
```
docker build -t iotivityslave .
docker run --workdir="/root"  -v "$(pwd)"/iotivity-extlibs-03272015:/root/extlibs -t iotivityslave bash -x BuildScript
```

If you want to mess around in the container after it is built you can jump into interactive mode.
```
docker run --workdir="/root"  -v "$(pwd)"/iotivity-extlibs-03272015:/root/extlibs -i -t iotivityslave /bin/bash
```

TODO push jenkins ENV variables so we can pull the right refspec.
TODO artifacts.
