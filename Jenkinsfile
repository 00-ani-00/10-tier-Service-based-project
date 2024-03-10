pipeline {
    agent any

    environment{
        SCANNER_HOME = tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/00-ani-00/10-tier-Service-based-project.git'
            }
        }
        stage('Static Code Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=10-Tier -Dsonar.projectName=10-Tier -Dsonar.java.binaries=. '''
                }
            }
        }
        
        stage('Building adservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/my-project/src/adservice/') {
                            sh 'docker build -t anilagad/adservice:latest .'
                            sh 'docker push anilagad/adservice:latest'
                            sh 'docker rmi anilagad/adservice:latest'
                        }
                    }
                }
            }
        }
        
        stage('Building cartservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/my-project/src/cartservice/src/') {
                            sh 'docker build -t anilagad/cartservice:latest .'
                            sh 'docker push anilagad/cartservice:latest'
                            sh 'docker rmi anilagad/cartservice:latest'
                        }
                    }
                }
            }
        }
        
        stage('Building checkoutservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/my-project/src/checkoutservice/') {
                            sh 'docker build -t anilagad/checkoutservice:latest .'
                            sh 'docker push anilagad/checkoutservice:latest'
                            sh 'docker rmi anilagad/checkoutservice:latest'
                        }
                    }
                }
            }
        }
        
        stage('Building currencyservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/my-project/src/currencyservice/') {
                            sh 'docker build -t anilagad/currencyservice:latest .'
                            sh 'docker push anilagad/currencyservice:latest'
                            sh 'docker rmi anilagad/currencyservice:latest'
                        }
                    }
                }
            }
        }
        
        stage('Building emailservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/my-project/src/emailservice/') {
                            sh 'docker build -t anilagad/emailservice:latest .'
                            sh 'docker push anilagad/emailservice:latest'
                            sh 'docker rmi anilagad/emailservice:latest'
                        }
                    }
                }
            }
        }
        
        stage('Building frontend') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/my-project/src/frontend/') {
                            sh 'docker build -t anilagad/frontend:latest .'
                            sh 'docker push anilagad/frontend:latest'
                            sh 'docker rmi anilagad/frontend:latest'
                        }
                    }
                }
            }
        }
        
        stage('Building loadgenerator') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/my-project/src/loadgenerator/') {
                            sh 'docker build -t anilagad/loadgenerator:latest .'
                            sh 'docker push anilagad/loadgenerator:latest'
                            sh 'docker rmi anilagad/loadgenerator:latest'
                        }
                    }
                }
            }
        }
        
        stage('Building paymentservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/my-project/src/paymentservice/') {
                            sh 'docker build -t anilagad/paymentservice:latest .'
                            sh 'docker push anilagad/paymentservice:latest'
                            sh 'docker rmi anilagad/paymentservice:latest'
                        }
                    }
                }
            }
        }
        
        stage('Building productcatalogservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/my-project/src/productcatalogservice/') {
                            sh 'docker build -t anilagad/productcatalogservice:latest .'
                            sh 'docker push anilagad/productcatalogservice:latest'
                            sh 'docker rmi anilagad/productcatalogservice:latest'
                        }
                    }
                }
            }
        }
        
        stage('Building recommendationservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/my-project/src/recommendationservice/') {
                            sh 'docker build -t anilagad/recommendationservice:latest .'
                            sh 'docker push anilagad/recommendationservice:latest'
                            sh 'docker rmi anilagad/recommendationservice:latest'
                        }
                    }
                }
            }
        }
        
        stage('Building shippingservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/my-project/src/shippingservice/') {
                            sh 'docker build -t anilagad/shippingservice:latest .'
                            sh 'docker push anilagad/shippingservice:latest'
                            sh 'docker rmi anilagad/shippingservice:latest'
                        }
                    }
                }
            }
        }
        
        stage('Deploy app to K8s') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'my-eks22', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://24DD716D951DF2F3919423F98EEDDA7D.gr7.eu-west-1.eks.amazonaws.com') {
                    cd '/var/lib/jenkins/workspace/my-project/k8s-manifests/'
                    sh 'kubectl apply -f deployment-service.yaml'
                    sh 'kubectl get pods'
                    sh 'kubectl get svc'
                }
            }
        }
        
    }
}
