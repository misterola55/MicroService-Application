pipeline {
    agent any
    environment {
        SCANNER_HOME = tool 'sonar-scanner'

   }

    stages {
            stage('SonarQube') {
             steps {
                withSonarQubeEnv('sonar') {
                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=Microservice_Deployment -Dsonar.ProjectName=Microservice_Deployment -Dsonar.java.binaries=.'''
                }
            }
        }
            stage('adservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir('/var/lib/jenkins/workspace/Microservice_Deployment/src/adservice/') {
                        sh "docker build -t misterola/adservice:latest ."
                        sh "docker push misterola/adservice:latest"
                        sh "docker rmi misterola/adservice:latest"
                    }
                }
            }
        }
            }
            stage('cartservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/cartservice/src/") {
                        sh "docker build -t misterola/cartservice:latest ."
                        sh "docker push misterola/cartservice:latest"
                        sh "docker rmi misterola/cartservice:latest"
                    }
                }
            }
        }
       }
            stage('checkoutservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/checkoutservice/") {
                        sh "docker build -t misterola/checkoutservice:latest ."
                        sh "docker push misterola/checkoutservice:latest"
                        sh "docker rmi misterola/checkoutservice:latest"
                    }
                }
            }
        }
            }
            stage('currencyservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/currencyservice/") {
                        sh "docker build -t misterola/currencyservice:latest ."
                        sh "docker push misterola/currencyservice:latest"
                        sh "docker rmi misterola/currencyservice:latest"
                    }
                }
            }
        }

            }
            stage('emailservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/emailservice/") {
                        sh "docker build -t misterola/emailservice:latest ."
                        sh "docker push misterola/emailservice:latest"
                        sh "docker rmi misterola/emailservice:latest"
                    }
                }
            }
        }
            }
            stage('frontend') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/frontend/") {
                        sh "docker build -t misterola/frontend:latest ."
                        sh "docker push misterola/frontend:latest"
                        sh "docker rmi misterola/frontend:latest"
                    }
                }
            }
        }
            }
            stage('loadgenerator') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/loadgenerator/") {
                        sh "docker build -t misterola/loadgenerator:latest ."
                        sh "docker push misterola/loadgenerator:latest"
                        sh "docker rmi misterola/loadgenerator:latest"
                    }
                }
            }
        }
            }
             stage('paymentservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/paymentservice/") {
                        sh "docker build -t misterola/paymentservice:latest ."
                        sh "docker push misterola/paymentservice:latest"
                        sh "docker rmi misterola/paymentservice:latest"
                    }
                }
            }
        }
             }
             stage('productcatalogservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/productcatalogservice/") {
                        sh "docker build -t misterola/productcatalogservice:latest ."
                        sh "docker push misterola/productcatalogservice:latest"
                        sh "docker rmi misterola/productcatalogservice:latest"
                    }
                }
            }
        }
             }
             stage('recommendationservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/recommendationservice/") {
                        sh "docker build -t misterola/recommendationservice:latest ."
                        sh "docker push misterola/recommendationservice:latest"
                        sh "docker rmi misterola/recommendationservice:latest"
                    }
                }
            }
        }
             }
             stage('shippingservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/shippingservice/") {
                        sh "docker build -t misterola/shippingservice:latest ."
                        sh "docker push misterola/shippingservice:latest"
                        sh "docker rmi misterola/shippingservice:latest"
                    }
                }
            }
        }
    }

              stage('EKS-Deployment') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'myAppp-eks-cluster', contextName: '', credentialsId: 'k8s', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://9729FE731B742891984A200A1CD08C05.gr7.us-east-1.eks.amazonaws.com') {
                    sh 'kubectl apply -f deployment-service.yaml'
                    sh 'kubectl get pods'
                    sh 'kubectl get svc'

                }
                }
            }
        }
   }
