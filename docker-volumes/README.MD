
# Creëer het netwerk en volumes
```
docker network create mijn_data_pipeline_netwerk
docker volume create raw_data_volume
docker volume create processed_data_volume
```

# Start de Data Generator container
```
docker run -d --name=data_generator \
  --network=mijn_data_pipeline_netwerk \
  -v raw_data_volume:/data/raw \
  busybox sh -c "while true; do echo 'nieuwe data' > /data/raw/data.txt; sleep 10; done"
```
# Start de Data Processor container
```
docker run -d --name=data_processor \
  --network=mijn_data_pipeline_netwerk \
  -v raw_data_volume:/data/raw \
  -v processed_data_volume:/data/processed \
  busybox sh -c "while true; do \
    if [ -f /data/raw/data.txt ]; then \
      cat /data/raw/data.txt | tr '[:lower:]' '[:upper:]' > /data/processed/processed_data.txt; \
      rm /data/raw/data.txt; \
    fi; \
    sleep 10; \
  done"
```
# Start de Data Storage container
```
docker run -d --name=data_storage \
  --network=mijn_data_pipeline_netwerk \
  -v processed_data_volume:/data/processed \
  busybox sh -c "while true; do \
    if [ -f /data/processed/processed_data.txt ]; then \
      cp /data/processed/processed_data.txt /data/processed/saved_data.txt; \
    fi; \
    sleep 10; \
  done"
```
# Inspect de verwerkte data 
```
docker exec -it data_storage cat /data/processed/saved_data.txt
```

Vult het resultaat in bij de opdracht
