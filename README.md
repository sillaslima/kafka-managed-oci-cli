```bash
# export envs
cp .env.example .env
nano .env  # adicione suas configurações


#Obter cluster-config-id:
CLUSTER_CONFIG_ID=$(oci kafka cluster-config list --compartment-id "$COMPARTMENT_ID" --query 'data.items[0].id' --raw-output 2>/dev/null)

source .env

echo "=== VERIFICAÇÃO DE VARIÁVEIS ===" && \
echo "COMPARTMENT_ID: ${COMPARTMENT_ID:-'NÃO DEFINIDA'}" && \
echo "SUBNET_ID: ${SUBNET_ID:-'NÃO DEFINIDA'}" && \
echo "DISPLAY_NAME: ${DISPLAY_NAME:-'NÃO DEFINIDA'}" && \
echo "CLUSTER_NAME: ${CLUSTER_NAME:-'NÃO DEFINIDA'}" && \
echo "KAFKA_VERSION: ${KAFKA_VERSION:-'NÃO DEFINIDA'}" && \
echo "CLUSTER_CONFIG_VERSION: ${CLUSTER_CONFIG_VERSION:-'NÃO DEFINIDA'}"&& \
echo "CLUSTER_TYPE: ${CLUSTER_TYPE:-'NÃO DEFINIDA'}" && \
echo "COORDINATION_TYPE: ${COORDINATION_TYPE:-'NÃO DEFINIDA'}" && \
echo "NODE_COUNT: ${NODE_COUNT:-'NÃO DEFINIDA'}" && \
echo "OCPU_COUNT: ${OCPU_COUNT:-'NÃO DEFINIDA'}" && \
echo "CLUSTER_CONFIG_ID: ${CLUSTER_CONFIG_ID:-'NÃO DEFINIDA'}" && \
echo "STORAGE_SIZE: ${STORAGE_SIZE:-'NÃO DEFINIDA'}" 



```


```bash
# create cluster
oci kafka cluster create \
  --compartment-id "$COMPARTMENT_ID" \
  --display-name "$DISPLAY_NAME" \
  --kafka-version "$KAFKA_VERSION" \
  --cluster-type "$CLUSTER_TYPE" \
  --coordination-type "$COORDINATION_TYPE" \
  --access-subnets file://access-subnets.json \
  --broker-shape file://broker-shape.json \
  --freeform-tags file://freeform-tags.json \
  --cluster-config-id "$CLUSTER_CONFIG_ID" \
  --cluster-config-version "$CLUSTER_CONFIG_VERSION" 
```