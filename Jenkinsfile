pipeline{
      agent any
      parameters{
      string(name: 'DOCKER_ID', defaultValue: 'monika22')
    	string(name: 'DOCKER_REPO', defaultValue: 'test-assessment')
    	string(name: 'DOCKER_TAG', defaultValue: 'httpbin-assessment-01')
           
      string(name: 'web_name', defaultValue: 'snapdeal')
      
      }
  stages{
    stage("SCM checkout"){
      steps{
            echo "Pulling...code"
            git branch: 'test-deploy', credentialsId: 'f66d7576-53da-42e8-bb7f-14af3e6668c5', url: 'https://github.com/MonikaSSahu/monika.git'
      }
      }
        stage('Deployment'){
              steps{
                   //To connect to the kubernetes cluster provide k8's credentials and project-name 
                  // As per security concerns not mentioning gcloud actual credentials
                 //After deployment I removed the webhook
                //sh "gcloud container clusters get-credentials k8-cluster --zone asia-south1-a --project project-name"
              sh "sed -i 's/tagVersion/${params.DOCKER_TAG}/g' httpbin-deployment.yaml"
		  sh "sed -i 's/dockerId/${params.DOCKER_ID}/g' httpbin-deployment.yaml"
		  sh "sed -i 's/dockerRepo/${params.DOCKER_REPO}/g' httpbin-deployment.yaml"
		  
		  sh "sed -i 's/web_name/${params.web_name}/g' httpbin-deployment.yaml"
		  
		  sh "sed -i 's/web_name/${params.web_name}/g' httpbin-service.yaml"
		  sh "sed -i 's/web_name/${params.web_name}/g' httpbin-service.yaml"   
                    
               script{
              try{
                sh "kubectl create -f httpbin-deployment.yaml"
                sh "kubectl create -f httpbin-service.yaml"
              } catch(error){
                sh "kubectl apply -f httpbin-deployment.yaml"
                sh "kubectl apply -f httpbin-service.yaml"
              }
            }
                   
              }
        }
  }
 }
