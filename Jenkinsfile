pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage ('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    app = docker.build('00314253/tran-shcedule')
                    app.inside {
                        sh 'echo $(curl localhost:8080)'
                    }    
                }    
            }
        }
    }
}
