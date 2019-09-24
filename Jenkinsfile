pipeline {
        agent {
               label "docker"
              }
        stages {
                stage('checkout'){
                        
                        steps {
                               echo 'starting checkout'
                               checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '11bd51bc-7ca4-45ce-a238-d472f2ab4101', url: 'https://github.com/vmadykumar/HappyTrippublic.git']]]) 
                               echo 'checkout completed'
                        }
                }
        }
}
