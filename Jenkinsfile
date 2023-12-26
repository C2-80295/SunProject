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
        //         mail bcc: '', body: 'Build Failed', cc: '', from: 'manojjakcin.2001@gmail.com', replyTo: '', subject: 'Build Failed', to: 'manojjakcin@gmail.com'
        //     }
        // }
        stage ('docker push image') {
            steps {
                sh '/usr/bin/docker image push jakejake23/sunproject'
            }
        }
        stage ('docker remove container') {
            steps {
                sh '/usr/bin/docker container rm -f sunproject'
            }   
        }
        stage ('docker create container') {
            steps {
                sh '/usr/bin/docker container run -d -p 9090:80 --name sunproject jakejake23/sunproject'
            }
    }
}
}

