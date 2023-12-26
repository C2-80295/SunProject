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
                sh 'echo dckr_pat_FxQD9x_Fec84SBAiHZuCeAkz8Rs | /usr/bin/docker login -u jakejake23 --password-stdin'
            }
        }
        stage ('docker build image') {
            steps {
                sh '/usr/bin/docker image build -t jakejake23/sunproject .'
            }
        }
        // stage('send notification to mail if build fails') {
        //     steps {
        //         script {
        //             emailext body: 'Jenkins Pipeline Failed',
        //             recipientProviders: [developers(), requester()],
        //             subject: 'Jenkins Pipeline Failed',
        //             to: 'manojjakcin@gmail.com'  // Specify the recipient email address
        //         }
        //     }
        // }
        stage ('docker push image') {
            steps {
                sh '/usr/bin/docker image push jakejake23/sunproject'
            }
        }
        stage ('docker create container') {
            steps {
                sh '/usr/bin/docker container run -d -p 9090:9000 jakejake23/sunproject'
            }
    }
}

