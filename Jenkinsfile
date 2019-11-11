pipeline {
        agent {label 'docker'}
        parameters  {
                booleanParam(name: 'Run_SonarAnalysis', defaultValue: false, description: 'Will Run Sonar Code Analysis')
                booleanParam(name: 'Release', defaultValue: false, description: 'Will Push code to the Server') 
        }
        environment {
                happytripImage = ''
                registry = "vmady/happy_trip"
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
                        stage('sonar analysis') {
                                        when {
                                                expression { params.Run_SonarAnalysis == true}
                                        }
                                        steps { 
                                                dir('Code') {
                                                        echo 'Executing sonar Analysis'        
                                                        withSonarQubeEnv('sonar server') {
                                                                sh 'mvn sonar:sonar'  
                                                        }
                                                }
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
                        stage('Release'){
                                        agent any
                                        when {
                                                expression { params.Release == true }
                                        }
                                steps {
                                        echo 'Starting Release'
                                        //deploy adapters: [tomcat7(credentialsId: '51d79b50-5fd8-4444-91eb-c6ead7dc4151', path: '', url: 'http://172.30.13.143:8081')], contextPath: '/HappyTrip', war: 'Code/target/*.war'
                                        echo 'Release Completed'
                                }
                        }
                }
        
}
