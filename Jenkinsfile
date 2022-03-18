pipeline{
      agent any
      parameters{
      string(name: 'DOCKER_ID', defaultValue: 'monika22')
    	string(name: 'DOCKER_REPO', defaultValue: 'test-assessment')
    	string(name: 'DOCKER_TAG', defaultValue: 'httpbin-assessment-8080')
      }
  stages{
    stage("SCM checkout"){
      steps{
            echo "Pulling...code"
            git branch: 'test', credentialsId: 'f66d7576-53da-42e8-bb7f-14af3e6668c5', url: 'https://github.com/MonikaSSahu/monika.git'
      }
      }
        stage('Build Docker image'){
              steps{
                    echo "build..image"
                    sh "docker build -t ${params.DOCKER_ID}/${params.DOCKER_REPO}:${params.DOCKER_TAG} ."
              }
        }
         stage('Push Docker image'){
              steps{
                    withDockerRegistry(credentialsId: 'dockerhub', url: '') {
                                    echo "Push the image to...Dockerhub "
                                    sh "docker push ${params.DOCKER_ID}/${params.DOCKER_REPO}:${params.DOCKER_TAG}"

                        }
                    }
        }
  }
 }
