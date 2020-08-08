# IBM Event Streams Demo Producer / Consumer

## Running Locally

```
# Set relavent environment variables for convenience

export KAFKA_BOOTSTRAP_SERVERS=<BOOTSTRAP-SERVER-LIST>
export KAFKA_API_KEY=<API_KEY>
export CERT_PATH=./es-cert.jks
export kafka_client_id_custom=<CUSTOM-CLIENT-ID>
export kafka_group_id_custom=<CUSTOM-GROUP-ID>

# Build
gradle clean && gradle build

# Run Producer
java -jar build/libs/kafka-java-console-sample-2.0.jar $KAFKA_BOOTSTRAP_SERVERS $KAFKA_API_KEY -producer -topic single-partition-demo-topic

# Separate Window - Run Consumer(s)
java -jar build/libs/kafka-java-console-sample-2.0.jar $KAFKA_BOOTSTRAP_SERVERS $KAFKA_API_KEY -consumer -topic single-partition-demo-topic
```



## To run on Openshift
```
# Use existing or new namespace
oc project eventstreams

# Change to the directory of the yaml
cd oc-deploy 

# Point to es-cert.jks file to create the secret
oc create secret generic demo-es-jks --from-file=es-cert.jks=/path-to/es-cert.jks --type=opaque

# Edit the secret and configure bootstrap server and api key
oc apply -f demo-es-secret.yaml

# Apply the deployment - change argument of topic as needed in args
oc apply -f kafka-java-console-sample.yaml
```

## Prebuilt image is available here
https://hub.docker.com/r/cstsui/ibm-kafka-console
