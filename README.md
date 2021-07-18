# GSP319 : Build a Website on Google Cloud: Challenge Lab

# Overview
In a challenge lab you’re given a scenario and a set of tasks. Instead of following step-by-step instructions, you will use the skills learned from the labs in the quest to figure out how to complete the tasks on your own! An automated scoring system (shown on this page) will provide feedback on whether you have completed your tasks correctly.

When you take a challenge lab, you will not be taught new Google Cloud concepts. You are expected to extend your learned skills, like changing default values and reading and researching error messages to fix your own mistakes.

To score 100% you must successfully complete all tasks within the time period!


# Task 1: Download the monolith code and build your container
    git clone https://github.com/googlecodelabs/monolith-to-microservices.git

    cd ~/monolith-to-microservices
    ./setup.sh

    cd ~/monolith-to-microservices/monolith
    npm start

    gcloud services enable cloudbuild.googleapis.com
    gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/fancytest:1.0.0 .


# Task 2: Create a kubernetes cluster and deploy the application
    gcloud config set compute/zone us-central1-a
    gcloud services enable container.googleapis.com
    gcloud container clusters create fancy-cluster --num-nodes 3

    kubectl create deployment fancytest --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/fancytest:1.0.0
    kubectl expose deployment fancytest --type=LoadBalancer --port 80 --target-port 8080



# Task 3: Create a containerized version of your Microservices
    {cd ~/monolith-to-microservices/microservices/src/orders
    gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/orders:1.0.0 .

    cd ~/monolith-to-microservices/microservices/src/products
    gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/products:1.0.0 .
}

# Task 4: Deploy the new microservices
    {kubectl create deployment orders --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/orders:1.0.0
    kubectl expose deployment orders --type=LoadBalancer --port 80 --target-port 8081

    kubectl create deployment products --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/products:1.0.0
    kubectl expose deployment products --type=LoadBalancer --port 80 --target-port 8082
}

# Task 5: Configure the Frontend microservice
    {cd ~/monolith-to-microservices/react-app
    nano .env
}


# Task 6: Create a containerized version of the Frontend microservice
    {cd ~/monolith-to-microservices/microservices/src/frontend
    gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/frontend:1.0.0 .
}


# Task 7: Deploy the Frontend microservice
    {kubectl create deployment frontend --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/frontend:1.0.0

    kubectl expose deployment frontend --type=LoadBalancer --port 80 --target-port 8080
}

# Congratulations, you're all done with the lab 😄

 

 
 
 
 
 
 
 
 
