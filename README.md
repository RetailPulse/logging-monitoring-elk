# Deployment Steps
# 1. Delete Existing Namespace (if applicable)
# - kubectl delete namespace observability
#   kubectl wait namespace observability --for=delete --timeout=120s
# 2. Apply the Kubernetes Configuration
# - kubectl apply -f k8s-elk-observability.yaml
# 3. Verify the Deployment
# - kubectl get all -n observability
# 4. Check Filebeat is shipping logs to Elasticsearch
# - $FB = (kubectl -n observability get pods -l app=filebeat -o jsonpath='{.items[0].metadata.name}')
# - kubectl -n observability exec -it "$FB" -- sh -lc 'curl -s http://elasticsearch:9200/_cat/indices?v'
# filebeat index should be there
# health status index                                 uuid                   pri rep docs.count docs.deleted store.size pri.store.size dataset.size
# yellow open   .ds-filebeat-8.12.2-2025.09.08-000001 BpRmOWf_SmyYSnjtAoWEPA   1   1          0            0    367.2kb        367.2kb      367.2kb
# 5. Access Kibana UI
# - http://localhost:30601
# - create data view pattern "filebeat-*"
# - search "message:"\"service.name\":\"rp-report-service\"""
























[//]: # (# logging-monitoring-elk)

[//]: # (0&#41; After run docker compose up -d)

[//]: # (# wait until all containers are up and running)

[//]: # ()
[//]: # (1&#41; Reset the kibana_system password inside ES)

[//]: # (# open a shell on the ES container)

[//]: # (docker exec -it es bash)

[//]: # ()
[//]: # (# run the reset tool &#40;interactive&#41;)

[//]: # (bin/elasticsearch-reset-password -u kibana_system -i)

[//]: # (# type a new password, e.g. changeme)

[//]: # (# &#40;or use -b to auto-generate and copy it&#41;)

[//]: # ()
[//]: # (2&#41; Add APM Service integration in Kibana UI)
