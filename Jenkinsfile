pipeline {
    agent any

    tools {
        gradle 'Gradle 8.14-rc-2' // Use the name set in Global Tool Config
    }

    environment {
        ARTIFACTORY_USER = credentials('jfrog-user')
        ARTIFACTORY_PASSWORD = credentials('jfrog-trial3lah5w')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'develop', url: 'https://github.com/SRI-2004/jenkins.git'
            }
        }

        stage('Build Services') {
            steps {
                sh './user-service/gradlew -p user-service clean build'
                sh './order-service/gradlew -p order-service clean build'
            }
        }

        stage('Publish to Artifactory') {
            steps {
                sh './user-service/gradlew -p user-service publish -Partifactory_user=$ARTIFACTORY_USER -Partifactory_password=$ARTIFACTORY_PASSWORD'
                sh './order-service/gradlew -p order-service publish -Partifactory_user=$ARTIFACTORY_USER -Partifactory_password=$ARTIFACTORY_PASSWORD'
            }
        }
    }
}
