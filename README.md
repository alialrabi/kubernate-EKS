
    *Install aws cli
       -https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html

    *Install kubectl cli
       -https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html


    *Login to aws region
        1-aws ecr get-login-password --region us-east-1 //COPY TOKEN
        2-sudo  docker login -u AWS -p TOKEN https://xxxxxxxxx.dkr.ecr.us-east-1.amazonaws.com
        
     *Connect to EKS cluster
       -Make connection
         aws eks --region REGION-CODE update-kubeconfig --name CLUSTER-NAME
       -Test your configuration.
         kubectl get svc
       -You should see .kube folder in home folder 


    *Push docker image to ECR
      -Create repository
         -https://console.aws.amazon.com/ecr/create-repository?region=us-east-1
      -Create tag
         -docker tag microserivce:latest xxxxxxxxxxx.dkr.ecr.us-east-1.amazonaws.com/microservice:latest
      -Push image
         -docker push xxxxxxxxxx.dkr.ecr.us-east-1.amazonaws.com/microservice:latest


    *Create EKS cluster with required configuration.
      -https://console.aws.amazon.com/eks/home?region=us-east-1#/cluster-create
      -open cluster page and create node with required configuration



    *Most used kubectl command
      -kubectl get pods                  //get pods 
      -kubectl get deploy                //get deployments
      -kubectl get service               //get services
      -kubectl get replicaset            //get replicaset 
      -kubectl get all                   //get all
      -kubectl create -f deployment.yml  //create pod and deploy microservice 
      -kubectl apply -f deployment.yml  //Apply changes in pod
      -kubectl logs PODNAME        //get pod logs
      -kubectl describe pod PODNAME        //describe pod
      -kubectl describe deploy DEPLOYNAME  //describe deploy
      -kubectl describe service SERVICENAME  //describe service
      -kubectl get node                      //get nodes in the cluster
      -kubectl delete pod PODNAME        //delete pod
      -kubectl delete deploy DEPLOYNAME  //delete deploy 
      
      
      *Setup EKS admin dashboard 
      
       -run the following comands in terminal
         kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.3.6/components.yaml   //Deploy the Metrics Server
         kubectl get deployment metrics-server -n kube-system //Verify that the metrics-server deployment is running 
         kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta8/aio/deploy/recommended.yaml //Deploy the dashboard
         kubectl apply -f eks-admin-service-account.yml   //eks-admin-service-account.yml found in git repository 
         kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep eks-admin | awk '{print $1}')  //copy token from output

       -open in the browser   
         http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#!/login
         
         
       -Choose Token, paste the copyed token from the previous command into the Token field, and choose SIGN IN.

  


  





