pipeline {
        agent {dockerfile true}
        parameters {
                booleanParam(name: 'Run_SonarAnalysis', defaultValue: false, description: 'Will Run Sonar Code Analysis')
                booleanParam(name: 'Release', defaultValue: false, description: 'Will Push code to the Server')             
        }
        tools {
                   jdk 'JAVA_HOME'
                   maven 'maven'      
               }
        stages {
                stage('checkout'){
                        
                        steps {
                                echo 'starting checkout'
                               checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '11bd51bc-7ca4-45ce-a238-d472f2ab4101', url: 'https://github.com/vmadykumar/HappyTrippublic.git']]]) 
                               echo 'checkout completed'
                        }
                }
                stage('build') {
                        steps {
                                script {
                                        echo 'Executing build process'
                                        docker.build
                                }
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
