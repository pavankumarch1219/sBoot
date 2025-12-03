pipeline {
  agent any

  environment {
    // fallback values; will be set properly when we call 'tool'
    MVN_OPTS = '-B -V'
  }

  stages {
    stage('Prepare Tools') {
      steps {
        script {
          // use the JDK tool configured in Manage Jenkins -> Global Tool Configuration
          def javaHome = tool name: 'jdk17', type: 'jdk'          // name must match Jenkins config
          env.JAVA_HOME = "${javaHome}"
          env.PATH = "${javaHome}/bin:${env.PATH}"

          // optional: use configured Maven
          def mvnHome = tool name: 'maven3', type: 'maven'       // name must match Jenkins config
          env.M2_HOME = "${mvnHome}"
          env.PATH = "${mvnHome}/bin:${env.PATH}"
        }
      }
    }

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Compile') {
      steps {
        sh 'mvn ${MVN_OPTS} compile'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn ${MVN_OPTS} test'
      }
      post {
        always { junit '**/target/surefire-reports/*.xml' }
      }
    }

    stage('Package') {
      steps {
        sh 'mvn ${MVN_OPTS} clean package'
      }
    }
  }
}
