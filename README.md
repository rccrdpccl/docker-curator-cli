# Curator-cli

Docker image for curator_cli.

```
docker run --rm ricc/curator-cli:0.1.0 --help
```

https://www.elastic.co/guide/en/elasticsearch/client/curator/current/singleton-cli.html


### Example

```
docker run --rm curatorcli --dry-run --use_ssl --host "https://myelasticsearch" delete_indices --filter_list '[{"filtertype":"age","source":"creation_date","direction":"older","unit":"days","unit_count":1},{"filtertype":"pattern","kind":"prefix","value":"logstash-alert","exclude":"True"}]'
```

### Run every 24 hours in docker swarm mode

To run curator once a day for the next 10 years.
```
docker service create --name docker-curator \
      --reserve-memory 50m \
      --container-label com.monitoring.group=ops-infrastructure \
      --mode global \
      --restart-delay 86400s \
      --restart-max-attempts 3650 \
      ricc/curator-cli:0.1.0  --use_ssl --host "https://myelasticsearch" delete_indices --filter_list '[{"filtertype":"age","source":"creation_date","direction":"older","unit":"days","unit_count":1},{"filtertype":"pattern","kind":"prefix","value":"logstash-alert","exclude":"True"}]'
```
