# jira-insight-object-count-prometheus-grafana


**Create file insight_obj_node.sh**
```bash

sudo vim /usr/local/sbin/insight_obj_node.sh
sudo chmod +x /usr/local/sbin/insight_obj_node.sh
sudo chmod 700 /usr/local/sbin/insight_obj_node.sh
```

**Insert into insight_obj_node.sh**
```bash
#!/bin/bash
###########
# Author: Ildar Khusyainov
# Email: ihusainov@gmail.com
# Description: Count of insight schema objects 
###########
 
PROMDIR="/var/lib/node_exporter/textfile_collector"
PROMFILE="${PROMDIR}/insight_obj_node01."
 
TMP_FILE=$(mktemp)
 
trap "rm -f ${TMP_FILE}" EXIT KILL SIGTERM TERM SIGKILL

counts=($( curl -S -GET -H "Content-Type: application/json" 'http://admin:adminpass@192.168.0.10:8082/rest/insight/latest/objectschema/list' | jq  -r  '.objectschemas[].objectCount'  ))

>${PROMFILE}$$

echo -e "# HELP My Rules \n# TYPE insight_obj_my_rules gauge\ninsight_obj_my_rules ${counts[@]:0:1}" >> ${PROMFILE}$$
echo -e "# HELP Call Center \n# TYPE insight_obj_call_center gauge\ninsight_obj_call_center ${counts[@]:1:1}" >> ${PROMFILE}$$
echo -e "# HELP Super Account \n# TYPE insight_obj_super_account gauge\ninsight_obj_super_account ${counts[@]:2:1}" >> ${PROMFILE}$$
echo -e "# HELP Mon Control \n# TYPE insight_obj_mon_control gauge\ninsight_obj_mon_control ${counts[@]:3:1}" >> ${PROMFILE}$$
 
mv ${PROMFILE}$$ ${PROMFILE}prom
```

**Get info from jira insight**
```bash
curl -S -GET -vvv -H "Content-Type: application/json" 'http://admin:adminpass!@192.168.0.10:8082/rest/insight/latest/objectschema/list' | jq  -r  '.objectschemas[].objectCount'
curl -S -GET -vvv -H "Content-Type: application/json" 'http://admin:adminpass!@192.168.0.10:8082/rest/insight/latest/objectschema/list' | jq -c -r '.objectschemas | [.[] | {id: .id, name: .name, objectCount: .objectCount}]'
curl -S -GET -vvv -H "Content-Type: application/json" 'http://admin:adminpass!@192.168.0.10:8082/rest/insight/latest/objectschema/list' | jq  -S '.objectschemas | [.[] | { id: .id, objectCount: .objectCount}] | keys_unsorted[] as $key|"export \($key)=\(.[$key])"'

```



