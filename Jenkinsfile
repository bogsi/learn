#!/usr/bin/env groovy

pipeline {
 
    agent any
    
    
    stages {
         stage('Git clone') {
                 steps {
                    checkout([$class: 'GitSCM', branches: [[name: "*/$env.GIT_BRANCH"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/nvaklinov/DevOps.git']]])
          }
        }

         stage ('Build') {
		 steps {
		       sh 'cp /var/lib/jenkins/scripts/* . && bash -x script.sh'
	      
               }
              
                  post {
                      success {
			  slackSend channel: "#devops", message: "Build Successfully completed - ${env.JOB_NAME} ${env.BUILD_NUMBER}" 
                 }
                }
              }
           } 
         
           post {  
             failure {
  		  slackSend channel: "#devops", message: "Build Failed :( - ${env.JOB_NAME} ${env.BUILD_NUMBER}"

            }
        always {
             cleanWs()
             
            }
               }
           }
