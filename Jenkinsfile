#!/usr/bin/env groovy Jenkinsfile
pipeline {
    agent {
        node {
            label 'slave-1'
        }
    }
    if(env.BRANCH_NAME == 'master'){
     stage("Upload"){
        echo 'Building..'
        }
     stage("Deploy"){
        echo 'Testing..'
       }
     }
}
