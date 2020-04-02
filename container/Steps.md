# Quick Reference Commands

Quick reference commands used in this example for binging your custom model as docker image to train and run inference on SageMaker.  



## Permissions

Set permissions for files before testing locally

```
chmod +x kmeans/train
chmod +x kmeans/serve

```
## Build Image

```
docker build -t sage-kmeans .

```


## Train

After you have build locally, you can test the training process locally. This will also create a model artifact

`docker run --rm -v $(pwd)/local_test/test_dir:/opt/ml sage-kmeans train`


## Predict

Once you have the model artifact, you can make predictions locally by running the docker container

`docker run --rm -p 127.0.0.1:8080:8080 -v $(pwd)/local_test/test_dir:/opt/ml sage-kmeans serve`

`./predict.sh http://127.0.0.1:8080 payload.csv text/csv`


## ECR

After local testing has  complete successfully, you can push the image to ECR to be able to use it with SageMaker


Get ECR login

`aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 967669495843.dkr.ecr.us-east-1.amazonaws.com/sage-kmeans`

Build image

`docker build -t sage-kmeans .`

Tag image

`docker tag sage-kmeans:latest 967669495843.dkr.ecr.us-east-1.amazonaws.com/sage-kmeans:latest`

Push to ECR

`docker push 967669495843.dkr.ecr.us-east-1.amazonaws.com/sage-kmeans:latest`