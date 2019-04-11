pipeline {
  agent any
  tools { 
        maven 'Maven'
        jdk 'JAVA_HOME'
  }
  stages {
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace... */
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
        sh 'echo $USER'
        sh 'echo whoami'
      }
    }
    stage('Docker Build') {
      steps {
        sh '/usr/bin/docker build -t address-service:latest .'
      }
    }
   
    stage('Push ECRImage') {
      steps {
        withDockerRegistry([credentialsId: 'AKIAJ2TAT4FMKSHX3BTA', url: "https://990456062402.dkr.ecr.us-east-1.amazonaws.com"]) {
          sh '/usr/bin/docker push satheeshch/employee-service:latest'
        }
      }
    }
  }
}
