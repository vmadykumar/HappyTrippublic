pipeline {
        agent {dockerfile true }
                stages {
                        stage('build') {
                                steps {
                                        sh "docker build -t happytrip:${BUILD_NUMBER} -f Dockerfile . "
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
