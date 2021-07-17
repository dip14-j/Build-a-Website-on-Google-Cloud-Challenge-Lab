# Build-a-Website-on-Google-Cloud-Challenge-Lab
This challenge lab tests your skills and knowledge from the labs in the Building Websites on Google Cloud Quest. You should be familiar with the content of these labs before attempting this lab.'
Overview
Task 1: Download the monolith code and build your container
Task 2: Create a kubernetes cluster and deploy the application
Task 3: Create a containerized version of your Microservices
Task 4: Deploy the new microservices
Task 5: Configure the Frontend microservice
Task 6: Create a containerized version of the Frontend microservice
Task 7: Deploy the Frontend microservice
Task 1: Download the monolith code and build your container
git clone https://github.com/googlecodelabs/monolith-to-microservices.git

cd ~/monolith-to-microservices
./setup.sh

cd ~/monolith-to-microservices/monolith
npm start

gcloud services enable cloudbuild.googleapis.com
gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/fancytest:1.0.0 .

Task 2: Create a kubernetes cluster and deploy the application
gcloud config set compute/zone us-central1-a
gcloud services enable container.googleapis.com
gcloud container clusters create fancy-cluster --num-nodes 3

kubectl create deployment fancytest --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/fancytest:1.0.0
kubectl expose deployment fancytest --type=LoadBalancer --port 80 --target-port 8080

Task 3: Create a containerized version of your Microservices
cd ~/monolith-to-microservices/microservices/src/orders
gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/orders:1.0.0 .

cd ~/monolith-to-microservices/microservices/src/products
gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/products:1.0.0 .

Task 4: Deploy the new microservices
kubectl create deployment orders --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/orders:1.0.0
kubectl expose deployment orders --type=LoadBalancer --port 80 --target-port 8081

kubectl create deployment products --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/products:1.0.0
kubectl expose deployment products --type=LoadBalancer --port 80 --target-port 8082

Task 5: Configure the Frontend microservice
cd ~/monolith-to-microservices/react-app
nano .env

Task 6: Create a containerized version of the Frontend microservice
cd ~/monolith-to-microservices/microservices/src/frontend
gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/frontend:1.0.0 .

Task 7: Deploy the Frontend microservice
kubectl create deployment frontend --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/frontend:1.0.0

kubectl expose deployment frontend --type=LoadBalancer --port 80 --target-port 8080

Congratulations, you're all done with the lab 😄


 
![gcp](https://user-images.githubusercontent.com/73305491/126037760-297421f8-a7d2-4b02-be8f-8a756385979f.jpg)

 
 
 
 
 
 
 
 
