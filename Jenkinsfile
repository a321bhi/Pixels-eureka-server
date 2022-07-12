pipeline {
  agent any
  stages {
    stage('Initialize') {
      steps {
        echo 'Initializing'
        bat 'mvn clean'
      }
    }

    stage('Build') {
      steps {
        bat 'mvn package'
      }
    }

    stage('Static Analysis') {
      steps {
        bat 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
      }
    }

    stage('Deploy') {
      steps {
        bat 'docker build -t pixels-eureka-server .'
        bat 'docker tag pixels-eureka-server abhi2104/pixels-eureka-server'
        bat 'docker push abhi2104/pixels-eureka-server'
      }
    }

    stage('') {
      agent {
        node {
          label 'jenkinsagent'
        }

      }
      steps {
        sh 'docker pull abhi2104/pixels-eureka-server'
      }
    }

  }
}