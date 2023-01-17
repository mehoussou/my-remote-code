
// registry = "public.ecr.aws/v3f8i0q6/backend-app"
// service = "backend-app"
// pipeline {
//     agent none
//   stages {
//     stage("Build Image"){
//         agent any
//         steps{
//             echo registry
//             echo 
//             echo  registry + "/" + service + ":rc-" + BUILD_NUMBER
//             sh " docker build . -t  ${registry}/${service}:rc-${BUILD_NUMBER}"
//         }
//     }
//     stage('Login to ecr') {
//         agent any
//         steps {
//             script{
//                 echo service
//                 withAWS(region:'us-east-2', credentials:'ecr-creds') {
//                     sh " aws ecr get-login-password | docker login  -u
// AWS --password-stdin  ${registry}"
//                 }
//             }
//         }
//     }
//     stage('push image') {
//         agent any
//         steps {
//             script{
//                 echo service
//                 withAWS(region:'us-east-2', credentials:'ecr-creds') {
//                     sh "docker push ${registry}/${service}:rc-${BUILD_NUMBER} "
//                 }
//             }
//         }
//     }
//     stage('deploy to ecs') {
//         agent any
//         steps {
//             script{

//             }
//         }
//     }
//     }
// }



pipeline {
    
    agent any
    
    environment {
        registry = "162816112568.dkr.ecr.us-east-2.amazonaws.com/my-code-chall"
        // registry = "public.ecr.aws/v3f8i0q6/frontend-app"
        
    }
    
    stages {

        // Cloning Git repo
        stage ('cloning Git') {
            steps {
                checkout checkout scmGit(branches: [[name: '*/code-challenge']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mehoussou/my-remote-code/tree/code-challenge']])
                
            }
        }

        //Build docker images
                      
        stage ('Docker Build') {
            steps {
                    script {
                        dockerImage = docker.build registry
                    }
                
            }
               
        }
        //Login and Push images to AWS ECR repository
        stage ('Docker Push') {
            steps {
                script {
                        sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 162816112568.dkr.ecr.us-east-2.amazonaws.com'
                        sh 'docker push 162816112568.dkr.ecr.us-east-2.amazonaws.com/my-code-chall:latest'
                }
            }

        }
        // Stopping Docker containers for cleaner Docker run
        stage ('Stop previous containers') {
            steps {
                sh 'docker ps -f name=backend-app -q | xargs --no-run-if-empty docker container stop'
                sh 'docker container ls -a -fname=backend-app -q | xargs -r docker container rm'
            }
        }
        // Run container from images built
        stage ('Docker run') {
            steps {
                script {
                    sh 'docker run -d -p 3000:3000 --rm --name backend-app 162816112568.dkr.ecr.us-east-2.amazonaws.com/my-code-chall:latest'
                }
            }
        }
    }
}






// registry = "public.ecr.aws/v3f8i0q6/backend-app"
// service = "backend-app"
// pipeline {
//     agent none

//   stages {
      
//         stage ('checkout') {
//             steps {
//                 checkout scmGit(branches: [[name: '*/mypublic']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mehoussou/my-code-remote']])
                
//             }
//         }
//     }
      
//     stage ("Build Image"){
//         agent any
//         steps{
//             echo registry
//             echo service
//             echo  registry + "/" + service + ":rc-" + BUILD_NUMBER
//             sh " docker build . -t  ${registry}/${service}:rc-${BUILD_NUMBER}"
//         }
//     }
//      stage('Login to ecr') {
//         agent any
//         steps {
//             script{
//                 echo service
//                 withAWS(region:'us-east-2', credentials:'ecr-creds') {
//                     sh " aws ecr get-login-password | docker login  -u AWS --password-stdin  ${registry}"
//                 }
//             }
//         }
//     }
//     stage('push image') {
//         agent any
//         steps {
//             script{
//                 echo service
//                 withAWS(region:'us-east-2', credentials:'ecr-creds') {
//                     sh "docker push ${registry}/${service}:rc-${BUILD_NUMBER} "
//                 }
//             }
//         }
//     }

//     stage('deploy to ecs') {
//         agent any
//         steps {
//             script {

//             }
//         }
//     }

//   }
    