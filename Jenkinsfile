pipeline {
  agent any
  stages {
    stage('checkout project') {
      steps {
        checkout scm
      }
    }
    stage('Test') {
      steps {
        sh 'mvn cobertura:cobertura test'
      }
    }
    stage('report') {
      parallel {
        stage('report') {
          steps {
            junit 'rarget/surefire-reports/*.xml'
          }
        }
        stage('coverage') {
          steps {
            cobertura(coberturaReportFile: 'target/site/cobertura/coverage.xml')
          }
        }
      }
    }
    stage('package') {
      steps {
        sh 'mvn package'
        archiveArtifacts 'target/*.jar'
      }
    }
  }
  post {
    always {
      echo 'I will always say Hello again!'

    }

    success {
      echo 'success!'

    }

    failure {
      echo 'failure!'

    }

  }
}