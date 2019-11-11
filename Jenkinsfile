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
                                        //sh "docker build ."
                                          happytripImage = sh "docker build -t happytrip:${BUILD_NUMBER} ."
                                        //sh "docker push "
                                        //dir('Code') {
                                          //              echo 'Hello Maven, Executing build'
                                            //            sh 'mvn clean package -Dv=${BUILD_NUMBER}'
                                                        
                                        //} 
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
