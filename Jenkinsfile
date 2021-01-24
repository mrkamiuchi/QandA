pipeline {
    agent {
        docker {
            image "maven:3.6.3-jdk-8"
            args '-v $HOME/.m2:/root/.m2'
        }
    }
    stages {
        stage('checkout') {
            steps {
                git branch: 'master',
                    credentialsId: 'mygithub',
                    url: 'https://github.com/mrkamiuchi/QandA.git'
                    sh 'cat /etc/*issue'
            }
        }
        stage('Build') {
            steps {
                sh 'export MAVEN_OPTS="-Xmx4G"'
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                sh 'export MAVEN_OPTS="-Xmx4G"'
                sh 'mvn test '
               }
           }
    }
    post {
        always {
            archive "target/**/*"
            junit 'target/surefire-reports/*.xml'
        }
    }
}
