pipeline {
        agent {label 'docker'}
        environment {
                happytripImage = ''
                registry = "vmady/myrepo"
                registryCredential = 'docker-hub-credentials'
        }
                stages {
                        stage('build') {
                                steps {
                                        script {
                                                happytripImage = docker.build registry + ":$BUILD_NUMBER"
                                        }
                                        //sh "docker build ."
                                          //happytripImage = sh "docker build -t happytrip:${BUILD_NUMBER} ."
                                        //sh "docker push "
                                        //dir('Code') {
                                          //              echo 'Hello Maven, Executing build'
                                            //            sh 'mvn clean package -Dv=${BUILD_NUMBER}'
                                                        
                                        //} 
                                }                      
                        }
                        stage('Deploy Image') {
                                                steps{
                                                        script {
                                                                docker.withRegistry( '', registryCredential ) {
                                                                        happytripImage.push()
                                                                }
                                                        }
                                                }
                         }
                        stage('Remove Unused docker image') {
                                                steps{
                                                        sh "docker rmi $registry:$BUILD_NUMBER"
                                                }
                        }
                        stage('Artifactory'){
                                        steps { 
                                                dir('Code') {
                                                                echo 'creating Artifacts'         
                                                                archiveArtifacts 'target/*.war'
                                                                echo 'Artifact created'
                                                }
                                        }
                        }
                }
        
}
