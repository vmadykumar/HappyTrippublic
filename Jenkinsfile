pipeline {
        agent {label 'docker'}
                stages {
                        stage('build') {
                                steps {
                                        sh "docker build -t happytrip:B${BUILD_NUMBER} ."
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
