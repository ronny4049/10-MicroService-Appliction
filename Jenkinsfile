pipeline {
    agent any
    environment {
        SCANNER_HOME = tool 'sonarqube'
    }
    stages {
        stage('Git check out') {
            steps {
                git branch: 'main', url: 'https://github.com/ronny4049/10-MicroService-Appliction.git'
            }
        }
        stage('Sonarqube') {
            steps {
                withSonarQubeEnv('Sonarqube-conf') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=10-Tier -Dsonar.projectName=10-Tier -Dsonar.java.binaries=. '''
                }
            }
        }
        stage('Ad Service') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10-tier/src/adservice/') {
                            sh "docker build -t ranjandalai4049/ad-service:latest ."
                            sh "docker push ranjandalai4049/ad-service:latest"
						    sh " docker rmi ranjandalai4049/ad-service:latest"

                    }

                   }
                }
            }
        }
        stage('cartservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/cartservice/src/') {
                                 sh "docker build -t ranjandalai4049/cartservice:latest ."
                                 sh "docker push ranjandalai4049/cartservice:latest"
								 sh " docker rmi ranjandalai4049/cartservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('checkoutservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/checkoutservice/') {
                                 sh "docker build -t ranjandalai4049/checkoutservice:latest ."
                                 sh "docker push ranjandalai4049/checkoutservice:latest"
								 sh " docker rmi ranjandalai4049/checkoutservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('currencyservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/currencyservice/') {
                                 sh "docker build -t ranjandalai4049/currencyservice:latest ."
                                 sh "docker push ranjandalai4049/currencyservice:latest"
								 sh " docker rmi ranjandalai4049/currencyservice:latest"
                        }
                    }
                }
            }
        }
        
		stage('emailservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/emailservice/') {
                                 sh "docker build -t ranjandalai4049/emailservice:latest ."
                                 sh "docker push ranjandalai4049/emailservice:latest"
								 sh " docker rmi ranjandalai4049/emailservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('frontend') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/frontend/') {
                                 sh "docker build -t ranjandalai4049/frontend:latest ."
                                 sh "docker push ranjandalai4049/frontend:latest"
								 sh " docker rmi ranjandalai4049/frontend:latest"
                        }
                    }
                }
            }
        }
		
		stage('loadgenerator') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/loadgenerator/') {
                                 sh "docker build -t ranjandalai4049/loadgenerator:latest ."
                                 sh "docker push ranjandalai4049/loadgenerator:latest"
								 sh " docker rmi ranjandalai4049/loadgenerator:latest"
                        }
                    }
                }
            }
        }
		
		stage('paymentservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/paymentservice/') {
                                 sh "docker build -t ranjandalai4049/paymentservice:latest ."
                                 sh "docker push ranjandalai4049/paymentservice:latest"
								  sh " docker rmi ranjandalai4049/paymentservice:latest"
                        }
                    }
                }
            }
        }
        
		stage('productcatalogservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/productcatalogservice/') {
                                 sh "docker build -t ranjandalai4049/productcatalogservice:latest ."
                                 sh "docker push ranjandalai4049/productcatalogservice:latest"
								 sh " docker rmi ranjandalai4049/productcatalogservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('recommendationservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/recommendationservice/') {
                                 sh "docker build -t ranjandalai4049/recommendationservice:latest ."
                                 sh "docker push ranjandalai4049/recommendationservice:latest"
								 sh " docker rmi ranjandalai4049/recommendationservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('shippingservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/shippingservice/') {
                                 sh "docker build -t ranjandalai4049/shippingservice:latest ."
                                 sh "docker push ranjandalai4049/shippingservice:latest"
								 sh " docker rmi ranjandalai4049/shippingservice:latest"
                        }
                    }
                }
            }
        }
        
        
        	stage('K8-Deploy') {
            steps {
                    withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'randemo1', contextName: '', credentialsId: 'kubernetes', namespace: 'webapps', serverUrl: 'https://9D430BD269526B99186C04829EBD8C0B.gr7.ap-south-1.eks.amazonaws.com']]) {
                         sh 'kubectl apply -f deployment-service.yml'
                         sh 'kubectl get pods '
                         sh 'kubectl get svc'
                }
            }
        }
        
    }
}
