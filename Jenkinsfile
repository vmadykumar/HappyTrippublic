pipeline {
        agent {label 'docker'}
                stages {
                         stage('checkout'){
                        
                                steps {
                                        echo 'starting checkout'
                                        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'ef1c4a29-cfdc-4b61-a8ca-93f13b747a8f', url: 'https://github.com/vmadykumar/HappyTrippublic.git']]])
                                        echo 'checkout completed'
                                }
                        }
                        stage('build') {
                                steps {
                                        script {readFileFromWorkspace('Dockerfile')}
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
