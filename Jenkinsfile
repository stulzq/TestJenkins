#!/usr/bin/env groovy Jenkinsfile

def cusversion="Jenkinsfile"
def testStage(String ppp) {
         echo 'functions '+ppp
         sh 'echo '+ppp
}


library 'JenkinsSharedLibraries'
pipeline {
    agent {
        node {
            label 'slave-1'
        }
    }
    environment {
        NUGET_KEY     = credentials('CanalSharp_Nuget_key')
    }
    triggers {
      githubPush()
    }
     stages {
         stage('Testaaa') {
             steps {     
                  testStage 'aaa'
                  sleep(time:3,unit:"SECONDS")
                  script {
                           currentBuild.result = 'SUCCESS'
                           timeout(time: 20, unit: 'MINUTES') {
                           echo "FAILURE stage"
                           def aaa='aaa'
                           }
                           echo 'aaa: ${aaa}'+aaa
                  }
             }
         }
          stage('build') {
            steps {
                echo "branch: ${env.BRANCH_NAME}"
                echo "current SHA: ${env.GIT_COMMIT}"
                echo "previous SHA: ${env.GIT_PREVIOUS_SUCCESSFUL_COMMIT}"
                echo "WORKSPACE: ${env.WORKSPACE}"
                script {
                    res1 = sh (script: "git diff --name-only $GIT_PREVIOUS_SUCCESSFUL_COMMIT|grep '$cusversion'", returnStatus: true) 
                    echo "res1: ${res1}"
                    echo "cusversion: ${cusversion}"
                    res2=releaseSelector 'Jenkinsfile2'
                    echo "res2: ${res2}"
                
                }
                script {
                    result = sh (script: "git log -1 | grep '\\[ci skip\\]'", returnStatus: true) 
                    if (result != 0) {
                        echo "performing build..."
                    } else {
                        echo "not running..."
                    }
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                echo "${env.NUGET_KEY}"
            }
        }
        stage('Deploy') {
            when {
                branch "test"
            }
            steps {
                echo 'testaaaa'
            }
        }
    }
    post { always { 
        script { currentBuild.result = 'NOT_BUILT' } 
    } }
}
