pipeline {
    agent {
        docker {
            image 'maven:3.8-jdk-8-openj9' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                def username = 'jenkins'
                echo 'hello Mr. ${username}'
                echo "I said, Hello Mr. ${username}"
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Test') {
            steps {
                echo 'start testing'
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                echo "env path: ${env.WORKSPACE}"
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
    
}