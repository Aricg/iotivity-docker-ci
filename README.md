# iotivity-docker-ci

Evaluating docker for build.iotivity.org

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
gsutil cp gs://iotivity-extlibs/extlibs-03272015.md5 .
md5sum extlibs-03272015.tar.gz; cat extlibs-03272015.md5
tar -xvf extlibs-03272015.tar.gz
```

Run build:
```
docker build -t iotivityslave .
docker run --workdir="/root"  -v "$(pwd)"/iotivity-extlibs-03272015:/root/extlibs -t iotivityslave bash -x BuildScript
```
Run build with hosts env variables
```
env > host_env; docker run --workdir="/root" --env-file="$(pwd)"/"host_env"   -v "$(pwd)"/iotivity-extlibs-03272015:/root/extlibs -i -t iotivityslave bash -x BuildScript
```


If you want to mess around in the container after it is built you can jump into interactive mode.
```
docker run --workdir="/root"  -v "$(pwd)"/iotivity-extlibs-03272015:/root/extlibs -i -t iotivityslave /bin/bash
```

TODO push jenkins ENV variables so we can pull the right refspec.

List of Build Parameters, really this is all we want to capture with env

GERRIT_EVENT_TYPE
GERRIT_EVENT_HASH
GERRIT_BRANCH
GERRIT_TOPIC
GERRIT_CHANGE_NUMBER
GERRIT_CHANGE_ID
GERRIT_PATCHSET_NUMBER
GERRIT_CHANGE_NUMBER
GERRIT_PATCHSET_REVISION
GERRIT_REFSPEC
GERRIT_PROJECT
GERRIT_CHANGE_NUMBER
GERRIT_CHANGE_SUBJECT
GERRIT_CHANGE_COMMIT_MESSAGE
GERRIT_CHANGE_URL
GERRIT_CHANGE_OWNER
GERRIT_CHANGE_OWNER_NAME
GERRIT_CHANGE_OWNER_EMAIL
GERRIT_PATCHSET_UPLOADER
GERRIT_PATCHSET_UPLOADER_NAME
GERRIT_PATCHSET_UPLOADER_EMAIL
GERRIT_EVENT_ACCOUNT
GERRIT_EVENT_ACCOUNT_NAME
GERRIT_EVENT_ACCOUNT_EMAIL
GERRIT_NAME
GERRIT_HOST
GERRIT_PORT
GERRIT_SCHEME
GERRIT_VERSION
