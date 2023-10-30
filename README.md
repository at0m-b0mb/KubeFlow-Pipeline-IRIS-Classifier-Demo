# KubeFlow-Pipeline-IRIS-Classifier-Demo

![KubeFlow Logo](https://www.red-gate.com/simple-talk/wp-content/uploads/2021/01/word-image-36.png)

## About
This project is a demonstration of a Kubeflow Pipeline for training and deploying an IRIS classifier model. It covers various components of the pipeline, from data preparation to model training and prediction.

## Instruction Video
[Watch the Instruction Video]()

## Project Links
- **GitHub Repository:** [KubeFlow-Pipeline-IRIS-Classifier-Demo](https://github.com/at0m-b0mb/)
- **LinkedIn Profile:** [Kailash Parshad on LinkedIn](https://www.linkedin.com/in/kailash-parshad/)

## Getting Started

### Prerequisites
Before running the Kubeflow pipeline, make sure you have the following prerequisites installed:
- Docker
- Minikube
- Kubernetes

### Installation
1. Add Docker's official GPG key:

    ```bash
    sudo apt-get update
    sudo apt-get install ca-certificates curl gnupg
    sudo install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg
    ```

2. Add the Docker repository to Apt sources:

    ```bash
    echo "deb [arch=\$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \$(. /etc/os-release && echo \$VERSION_CODENAME) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```

3. Update the package list:

    ```bash
    sudo apt-get update
    ```

4. Install Docker and related packages:

    ```bash
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```

5. Download and install Minikube:

    ```bash
    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
    sudo dpkg -i minikube_latest_amd64.deb
    ```

6. Start the Minikube cluster:

    ```bash
    sudo usermod -aG docker $USER && newgrp docker
    minikube start
    ```

7. Interact with the Kubernetes cluster:

    ```bash
    kubectl get po -A
    ```

8. Deploy Kubeflow Pipelines:

    ```bash
    export PIPELINE_VERSION=2.0.2
    kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/cluster-scoped-resources?ref=$PIPELINE_VERSION"
    kubectl wait --for condition=established --timeout=60s crd/applications.app.k8s.io
    kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/env/platform-agnostic-pns?ref=$PIPELINE_VERSION"
    ```

### Usage

1. Start a Minikube cluster, if not already running:

    ```bash
    minikube start
    ```

2. Verify that the Kubeflow Pipelines UI is accessible by port forwarding:

    ```bash
    kubectl port-forward -n kubeflow svc/ml-pipeline-ui 8080:80
    ```

3. Access the Kubeflow Pipeline: IRIS Classifier Model by following the link:

    [Kubeflow Pipeline: IRIS Classifier Model](https://github.com/at0m-b0mb/KubeFlow-Pipeline-IRIS-Classifier-Demo/blob/main/KubeFlow_Pipeline_IRIS_Classifier_Kailash.ipynb)

### Kubeflow Pipeline Creation
The Kubeflow pipeline creation work starts here. The compiled YAML file is also attached.

### Components
This project includes the following components for building and running the IRIS classifier model:

- `prepare_data`: Data preparation component
- `train_test_split`: Component for splitting data into training and testing sets
- `training_basic_classifier`: Model training component
- `predict_on_test_data`: Component for making predictions on the test data
- `predict_prob_on_test_data`: Component for predicting probabilities
- `get_metrics`: Component for calculating model metrics

### Pipeline Definition
The pipeline is defined in the code and can be customized as needed. It includes steps for data preparation, model training, and evaluation.

### Running the Pipeline
To run the pipeline, use the provided Python code and specify the data path. You can also customize the pipeline according to your requirements.

```python
# Define the pipeline
@dsl.pipeline(
   name='IRIS classifier Kubeflow Pipeline',
   description='IRIS classifier by Kailash'
)
def iris_classifier_pipeline(data_path: str):
    # Pipeline definition here
    # ...
```
##Experiment and Run
You can create an experiment and run the pipeline using the provided code.
```python
# Create an experiment and run the pipeline
experiment_name = 'iris_classifier_exp'
run_name = 'iris_classifier_run'
namespace = "kubeflow"
arguments = {"data_path": DATA_PATH}

kfp.compiler.Compiler().compile(pipeline_func, 'iris_classifier_pipeline.yaml')
run_result = client.create_run_from_pipeline_func(pipeline_func, experiment_name=experiment_name, run_name=run_name, arguments=arguments)
```
## Note: Please Refer the pdf, and Jupyter notebook for for full codes!
