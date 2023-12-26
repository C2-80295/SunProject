// Setup the webhook to send the notification to Jenkins Machine

pipeline {
    agent any

    stages {
        stage ('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/C2-80295/SunProject.git'
            }
        }
        stage ('docker login') {
            steps {
                sh 'sudo echo dckr_pat_FxQD9x_Fec84SBAiHZuCeAkz8Rs | /usr/bin/docker login -u jakejake23 --password-stdin'
            }
        }
        stage ('docker build image') {
            steps {
                sh 'sudo /usr/bin/docker build -t jakejake23/sunproject .'
            }
        }
        stage('send notification to mail if build fails') {
            steps {
                script {
                    emailext body: 'Jenkins Pipeline Failed',
                    recipientProviders: [developers(), requester()],
                    subject: 'Jenkins Pipeline Failed',
                    to: 'manojjakcin@gmail.com'  // Specify the recipient email address
                }
            }
        }
        stage ('docker push image') {
            steps {
                sh 'sudo /usr/bin/docker push jakejake23/sunproject'
            }
        }
        stage ('docker create service') {
            steps {
                sh 'sudo /usr/local/bin/docker service create --name myservice --replicas 5 -p 9090:9000 jakejake23/sunproject'
            }
            
        }
    }
}

