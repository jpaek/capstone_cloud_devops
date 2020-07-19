node {
    stage 'Checkout'
    git url: 'https://github.com/jpaek/capstone_cloud_devops.git'

    stage('Lint')
        sh 'whoami'
        sh 'ls ~/'
        docker.image('python:3.7.3').inside {
            sh '''
            pip install -r requirements.txt
            wget -O /bin/hadolint https://github.com/hadolint/hadolint/releases/download/v1.16.3/hadolint-Linux-x86_64 &&\
            chmod +x /bin/hadolint
            hadolint Dockerfile
            pylint --disable=R,C,W1203 web.py
            '''
        }

    stage('Build') {
        docker.build('cloud_devops_capstone')
    }
    stage('Docker push') {
        docker.withRegistry('https://937431759388.dkr.ecr.us-east-2.amazonaws.com', 'ecr:jenkins') {
            docker.image('cloud_devops_capstone').push('latest')
        } 
    }
}
