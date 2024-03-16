# Python Application Deployment with Prometheus Monitoring

This repository contains a Jenkins pipeline to deploy a Python application integrated with Prometheus for monitoring. The Python application is a simple Flask web server that exposes a "/metrics" endpoint to provide Prometheus metrics.

## Files Structure

- **app/**: Contains the Python application files.
  - **app.py**: Main Python file containing the Flask application with Prometheus metrics integration.
  - **Dockerfile**: Dockerfile for building the Python application image.
  - **requirements.txt**: Required Python packages.
- **k8s_resources/**: Kubernetes resource files.
  - **rbac.yaml**: Role-based access control definitions.
  - **deployment.yaml**: Deployment configuration for the Python application.
  - **service.yaml**: Kubernetes service configuration.

## Jenkins Pipeline

The Jenkins pipeline automates the deployment process as follows:

1. **Checkout Source**: Clones the repository from GitHub.
2. **Build image**: Builds the Docker image using the provided Dockerfile.
3. **Pushing Image**: Pushes the Docker image to Docker Hub.
4. **Deploying App to Kubernetes**: Deploys the application to Kubernetes using the provided Kubernetes resource files.

## Python Application Code Explanation

The `app.py` file contains the following functionalities:

- Imports necessary modules including Flask, Prometheus client, Kubernetes client, and threading.
- Defines Prometheus metrics such as Gauge and Counter.
- Initializes Flask app and sets up a route for the "/" endpoint.
- Implements Prometheus metrics for counting HTTP requests.
- Retrieves the total number of running pods in the Kubernetes cluster using the Kubernetes Python client.
- Starts a separate thread to continuously update the running pods metric.
- Runs the Flask app with a DispatcherMiddleware to expose Prometheus metrics on "/metrics" endpoint.

## Viewing Metrics on Grafana via Prometheus

To view application metrics on Grafana through Prometheus, follow these steps:

1. Access the Grafana dashboard.
2. Navigate to the home page of Grafana.
3. To explore metrics, create a new query:
   - Select the label "app".
   - Set the value to "python-app".
   - Optionally, configure the query to run every 5 seconds for real-time monitoring.

## Conclusion

This project demonstrates how to deploy a Python application integrated with Prometheus for monitoring in a Kubernetes environment using Jenkins pipeline automation. Follow the provided steps to deploy the application and view its metrics on Grafana via Prometheus.
