
## Permissions

```
chmod +x kmeans/train
chmod +x kmeans/serve

```
## Build Image

`docker build -t sage-kmeans .`


## Train

`docker run --rm -v $(pwd)/local_test/test_dir:/opt/ml sage-kmeans train`


## Predict

`docker run --rm -p 127.0.0.1:8080:8080 -v $(pwd)/local_test/test_dir:/opt/ml sage-kmeans serve`

`./predict.sh http://127.0.0.1:8080 payload.csv text/csv`


## ECR

Push image to ECR

* Get ECR login
* Build image
* Push to ECR