# multistagepythondocker
This repo helps in creating a multistage docker image using python.
This image can be uploaded to any cloud repository.
For example this image could be uploaded to AWS ECR and used to deploy on ECS-Fargate or lambda which runs this image.

Steps for creating docker image and push to ECR

Before building the image on local docker we have to create repository in ECR in AWS Console. 
<div>
  aws ecr create-repository --repository-name base-image
</div>
<div>
  aws ecr create-repository --repository-name sample-image
</div>

Execute the below command for pushing the image to ECR, this command is to get the command line, login and have proper credentials for the push operation of the local image to ECR.
<div>
  aws ecr get-login-password --region {region} | docker login --username AWS --password-stdin {account}.dkr.ecr.{region}.amazonaws.com
<div>

  Navigate to BaseImage folder - 
<div>
  docker build -t base-image:latest  .
</div>
<div>
  docker tag base-image:latest {account}.dkr.ecr.{region}.amazonaws.com/base-image:latest
</div>
<div>
  docker push {account}.dkr.ecr.{region}.amazonaws.com/base-image:latest
</div>

Navigate to MainImage folder -
cd MainImage
<div>
  docker build -t sampleimage:latest  .
</div>
<div>
  docker tag sampleimage:latest {account}.dkr.ecr.{region}.amazonaws.com/sampleimage:latest
</div>
<div>
  docker push {account}.dkr.ecr.{region}.amazonaws.com/sampleimage:latest
</div>
  
We have to use valid values at places of {account} - account id , {region} - region of aws resources.

We can write the proper business use case logic in samplefunction.py based on the requirement.
