# Week 1 - Introduction

### What is ML Ops?

* Set of practices for automating and working collaboratively to achieve specific goals/objectives
* E.g., objective: predict duration of taxi trip
* Stages of ML Project:
  * Design
  * Training (if ML is needed)
  * Operation
* Deployment - deploying service to API; customers interacting with API; part of operation stage 

### Running from the Cloud

If we are running an AWS remote instance, we can SSH into it from terminal using it's public IPv4 or public DNS address:

```python
ssh -i ~/.ssh/razer.pem ubuntu@34.248.245.41
```

In the above line, ```-i ``` refers to the path to the file. ```razer.pem``` is the SSH key-value file that is generated through AWS. It should be placed in the ```.ssh``` folder. 

Can also define a config file in `.ssh` folder:

```config
Host mlops-zoomcamp
     HostName xx.xxx.xxx.xx
     User ubuntu
     Identity File c:/Users/username/.ssh/razer.pem
     StrictHostKeyChecking no
```

Note that the IP address must be updated anytime the instance is restarted. 

Then we can run as follows:

```
ssh mlops-zoomcamp
```

### Setting up the Environment

### Step 1: Download and install the Anaconda distribution of Python

```
wget https://repo.anaconda.com/archive/Anaconda3-2022.05-Linux-x86_64.sh
bash Anaconda3-2022.05-Linux-x86_64.sh
```

### Step 2: Update existing packages

```
sudo apt update
```

### Step 3: Install Docker

```
sudo apt install docker.io
```

To run docker without `sudo`:

```
sudo groupadd docker
sudo usermod -aG docker $USER
```

### Step 4: Install Docker Compose

Install docker-compose in a separate directory

```
mkdir soft
cd soft
```

To get the latest release of Docker Compose, go to https://github.com/docker/compose and download the release for your OS.

```
wget https://github.com/docker/compose/releases/download/v2.5.0/docker-compose-linux-x86_64 -O docker-compose
```

Make it executable

```
chmod +x docker-compose
```

Add to the `soft` directory to `PATH`. Open the `.bashrc` file with `nano`:

```
nano ~/.bashrc
```

In `.bashrc`, add the following line:

```
export PATH="${HOME}/soft:${PATH}"
```

Save it and run the following to make sure the changes are applied:

```
source .bashrc
```

### Step 5: Run Docker

```
docker run hello-world
```



### ML Pipeline

* **ML Pipline = Load and Prepare Data -> Vectorize -> Train**

* Input can be

  ```
  train_data = '2022-01'
  val_data = '2022-02'
  ```

  

![image-20220522182842171](/home/kckuei/snap/typora/57/.config/Typora/typora-user-images/image-20220522182842171.png)

![image-20220522183130641](/home/kckuei/snap/typora/57/.config/Typora/typora-user-images/image-20220522183130641.png)

* Deployment
  * ML model gets deployed to web service; user interacts with API
  * Can have monitoring, manually, or fully automated (pipeline automatically re-trains on new data)
* ML Ops Maturity Levels
  * No ML -> Fully Automated ML

### ML Ops Maturity Level

[Reference Article](https://docs.microsoft.com/en-us/azure/architecture/example-scenario/mlops/mlops-maturity-model)

Framework for ML Ops Maturity Level

Way for thinking about different levels of maturity that may be applicable to projects.

* **Level 0: No MLOps**
  * No automation, all code in Juptyer
  * Data scientist working as an individual, hands off notebooks to engineers to implement
  * Stage: Proof of concept (POC)
* **Level 1: DevOps, No MLOps**
  * Some level of automation
  * Best engineering/DevOps practices 
  * Releases are automated (analogous to web-services)
  * Unit Tests, Integration Tests, CI/CD
  * Not 'ML-aware'
  * Ops Metrics
  * No experiment tracking, reproducability
  * DS seperated from engineers
  * Stage: POC -> Production ready
* **Level 2: Automated Training**
  * Training pipeline
  * Experiment tracking
  * Model registry
  * Low friction deployment
  * DS work/integrated with engineers
  * Stage: Multiple (2-3) models already working in production
* **Level 3: Automated Deployment**
  * Easy to deploy model
  * As simple as API call to ML Platform
  * Pipeline: Prepare data -> Train model -> Deploy model
  * A/B testing capabilities for comparing between ML versions
  * Model Monitoring
  * Stage: 5-6 use cases, model monitoring
* **Level 4:** **Full MLOps Automation**
  * Automatic training, retraining, deployment all-in-one
  * Drifted ML model -> correct pipeline -> re-deploy
  * May also incorporate A/B tests automatically 