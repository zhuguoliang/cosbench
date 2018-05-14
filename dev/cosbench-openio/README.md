# OpenIO COSBench plugin

The plugin implements basic storage functions (create/delete containers and create/get/ delete objects).

## Configuration

Elements to set in workload config parameter:

* `ns`: name of the namespace
* `account`: the account in which the plugin will work
* `proxyd-url`: the URL of the OpenIO proxyd service of your namespace
* *for erasure coding* `ecd-url`: URL of an ECD service

See workload example [here](../../release/conf/openio-config-sample.xml).


## Updating the plugin

```bash
PREV=$((cd dev/cosbench-openio && /bin/ls -1 -v openio-api-* ) | tail -n 1)
mvn dependency:copy -Dartifact=io.openio.sds:openio-api:LATEST -DoutputDirectory=dev/cosbench-openio/
LATEST=$((cd dev/cosbench-openio && /bin/ls -1 -v openio-api-* ) | tail -n 1)
sed -e "s/openio-api-.*\.jar/${LATEST}/g" dev/cosbench-openio/META-INF/MANIFEST.MF dev/cosbench-openio/.classpath dev/cosbench-openio/build.properties
rm -f "dev/cosbench-openio/${PREV}"
```