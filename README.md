# Deploy ELK Stack for Observability in Kubernetes using Helm
# 1. Create observability namespace
# kubectl create namespace observability
# 2. Upgrade or install the helm chart
# helm upgrade --install elk ./elk-helm-chart -n observability --create-namespace
# 3. Verify the deployment
# kubectl get all -n observability
# 4. Check filebeat index in Elasticsearch
# kubectl -n observability run --rm -i --tty curlpod --image=curlimages/curl --restart=Never -- sh -c "curl -sS http://elasticsearch:9200/_cat/indices?v"
# .ds-filebeat-8.12.2 index should be there
# 5. Access Kibana UI
# http://localhost:30601
# 6. Create data view pattern "filebeat-*"
# 7. Search logs with query: message:"\"service.name\":\"rp-report-service\"

[//]: # (# Deployment Steps)

[//]: # (# 1. Delete Existing Namespace &#40;if applicable&#41;)

[//]: # (# - kubectl delete namespace observability)

[//]: # (#   kubectl wait namespace observability --for=delete --timeout=120s)

[//]: # (# 2. Apply the Kubernetes Configuration)

[//]: # (# - kubectl apply -f k8s-elk-observability.yaml)

[//]: # (# 3. Verify the Deployment)

[//]: # (# - kubectl get all -n observability)

[//]: # (# 4. Check Filebeat is shipping logs to Elasticsearch)

[//]: # (# - $FB = &#40;kubectl -n observability get pods -l app=filebeat -o jsonpath='{.items[0].metadata.name}'&#41;)

[//]: # (# - kubectl -n observability exec -it "$FB" -- sh -lc 'curl -s http://elasticsearch:9200/_cat/indices?v')

[//]: # (# filebeat index should be there)

[//]: # (# health status index                                 uuid                   pri rep docs.count docs.deleted store.size pri.store.size dataset.size)

[//]: # (# yellow open   .ds-filebeat-8.12.2-2025.09.08-000001 BpRmOWf_SmyYSnjtAoWEPA   1   1          0            0    367.2kb        367.2kb      367.2kb)

[//]: # (# 5. Access Kibana UI)

[//]: # (# - http://localhost:30601)

[//]: # (# - create data view pattern "filebeat-*")

[//]: # (# - search "message:"\"service.name\":\"rp-report-service\""")


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
