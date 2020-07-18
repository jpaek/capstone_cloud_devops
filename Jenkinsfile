pipeline {

     agent any
     stages {
         stage('Install Dependency') {
             steps {
                 make setup
                 make install
                 wget -O /bin/hadolint https://github.com/hadolint/hadolint/releases/download/v1.16.3/hadolint-Linux-x86_64 &&\
                 chmod +x /bin/hadolint
             }
         }
         stage('Lint') {
             steps {
                 . venv/bin/activate
                 make lint
             }
         }
         stage('Build') {
             steps {
                 docker.build('cloud_devops_capstone')
             }
         }
         stage('Docker push') {
            steps {
                docker.withRegistry('https://937431759388.dkr.ecr.us-east-2.amazonaws.com', 'ecr:jenkins') {
                    docker.image('cloud_devops_capstone').push('latest')
                }
            }
         }
     }
}
