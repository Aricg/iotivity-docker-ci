# iotivity-docker-ci

mkdir iotivity-extlibs-03272015/
gsutil rsync -d -r -p gs://iotivity-extlibs/iotivity-extlibs-03272015/ iotivity-extlibs-03272015/
chmod -R +x iotivity-extlibs-03272015/
docker build -t iotivityslave .
docker run --workdir="/root"  -v "$(pwd)"/iotivity-extlibs-03272015:/root/extlibs -t iotivityslave bash -x BuildScript
