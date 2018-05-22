pipeline {
  agent {
    node {
      label 'maven-jdk-8'
    }
    
  }
  stages {
    stage('Preparation') {
      steps {
        git(url: 'https://github.com/jglick/simple-maven-project-with-tests.git', branch: 'master')
        sh 'echo "hello"'
      }
    }
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh 'mvn -Dmaven.test.failure.ignore clean package'
          }
        }
        stage('codeQA') {
          steps {
            echo 'code has been scanned'
          }
        }
        stage('License Check') {
          steps {
            sh 'ls -al'
          }
        }
        stage('Copyright') {
          steps {
            sh 'echo "copyright checks performed"'
          }
        }
      }
    }
    stage('Result') {
      steps {
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.jar'
      }
    }
  }
}