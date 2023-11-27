## debezium-connector

We should prepare the kubernetes deployments files here for deploying the debezium connector with peroper configuration

### Explanation:

- **Deployment**:
  - Defines a Deployment for Debezium Connect.
  - The container image is set to `quay.io/debezium/connect:2.4`.
  - Container port `8083` is exposed for HTTP access to the Connect REST API.
  - Environment variables are set based on your Docker command.
  - Additional environment variables `BOOTSTRAP_SERVERS` and `DATABASE_HOST` are defined to point to the Kafka and MySQL services. Replace `kafka-service` and `mysql-service` with the actual names of your Kafka and MySQL services in Kubernetes.

- **Service**:
  - Defines a Service to expose Debezium Connect within the Kubernetes cluster.
  - The service is of type `ClusterIP`, making it accessible within the cluster.

### Additional Considerations:

- **Kafka and MySQL Services**: Ensure that the Kafka and MySQL services are correctly running in your Kubernetes environment and that their service names match the values specified in `BOOTSTRAP_SERVERS` and `DATABASE_HOST`.
- **Security and Configuration**: For a production environment, you might need to handle security, configuration, and secret management more robustly.
- **Resource Allocation**: Depending on your workload, consider specifying resource requests and limits for the Debezium Connect container.
