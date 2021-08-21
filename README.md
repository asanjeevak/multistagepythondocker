# multistagepythondocker
This repo helps in creating a multistage docker image using python.
This image can be uploaded to any cloud repository.
For example this image could be uploaded to AWS ECR and used to deploy on ECS-Fargate or lambda which runs this image.

Steps for creating docker image and push to ECR

Before building the image on local docker we have to create repository in ECR in AWS Console. 
aws ecr create-repository --repository-name base-image
aws ecr create-repository --repository-name sample-image

Execute the below command for pushing the image to ECR, this command is to get the command line, login and have proper credentials for the push operation of the local image to ECR.
aws ecr get-login-password --region {region} | docker login --username AWS --password-stdin {account}.dkr.ecr.{region}.amazonaws.com

Navigate to BaseImage folder - 
docker build -t base-image:latest  .
docker tag base-image:latest {account}.dkr.ecr.{region}.amazonaws.com/base-image:latest
docker push {account}.dkr.ecr.{region}.amazonaws.com/base-image:latest

Before building the image on local docker we have to create repository in ECR in AWS Console. 
aws ecr create-repository --repository-name base-image

Navigate to MainImage folder -
cd MainImage
docker build -t sampleimage:latest  .
docker tag sampleimage:latest {account}.dkr.ecr.{region}.amazonaws.com/sampleimage:latest
docker push {account}.dkr.ecr.{region}.amazonaws.com/sampleimage:latest

We have to use valid values at places of {account} - account id , {region} - region of aws resources.
