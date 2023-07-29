pipeline {
    agent any

    triggers {
        cron('0/2 * * * *') // Schedule to run every 2 minutes
    }


stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'Github-Cred-New', url: 'https://github.com/cutenegro4u/sonarscript.git'
            }
        }

stage("Sonarqube Analysis") {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'Sonar-Jenks-Cred') {
                        sh "mvn clean compile sonar:sonar"
                    }
                }
            }

    stages {
        stage('SonarQube Pipeline') {
            steps {
                script {
                    // Load the SonarQube pipeline script from the file
                    def sonarQubePipeline = load 'sonarqube_pipeline.groovy'

                    // Execute the SonarQube pipeline
                    sonarQubePipeline.startSonarQube()
                }
            }
        }
    }
}
