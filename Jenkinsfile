pipeline {
        agent {label 'docker'}
                stages {
                        stage('build') {
                                steps {
                                        //sh "docker build ."
                                         def happytripapp = sh "docker build -t vmady/myrepo:happytrip:${BUILD_NUMBER} ."
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
