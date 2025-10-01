```bash
# export envs
cp .env.example .env
nano .env  # adicione suas configurações

source .env

echo "=== VERIFICAÇÃO DE VARIÁVEIS ===" && \
echo "COMPARTMENT_ID: ${COMPARTMENT_ID:-'NÃO DEFINIDA'}" && \
echo "DISPLAY_NAME: ${DISPLAY_NAME:-'NÃO DEFINIDA'}" && \
echo "KAFKA_VERSION: ${KAFKA_VERSION:-'NÃO DEFINIDA'}" && \
echo "CLUSTER_TYPE: ${CLUSTER_TYPE:-'NÃO DEFINIDA'}" && \
echo "COORDINATION_TYPE: ${COORDINATION_TYPE:-'NÃO DEFINIDA'}" && \
echo "CLUSTER_CONFIG_VERSION: ${CLUSTER_CONFIG_VERSION:-'NÃO DEFINIDA'}"

```

```bash
# create cluster
oci kafka cluster create \
  --compartment-id "$COMPARTMENT_ID" \
  --display-name "$DISPLAY_NAME" \
  --kafka-version "$KAFKA_VERSION" \
  --cluster-type "$CLUSTER_TYPE" \
  --coordination-type "$COORDINATION_TYPE" \
  --access-subnets file://./temp_kafka_json/access-subnets.json \
  --broker-shape file://./temp_kafka_json/broker-shape.json \
  --freeform-tags file://./temp_kafka_json/freeform-tags.json \
  --cluster-config-id "$CLUSTER_CONFIG_ID" \
  --cluster-config-version "$CLUSTER_CONFIG_VERSION" 
```