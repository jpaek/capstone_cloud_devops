node {
    stage 'Checkout'
    git url: 'https://github.com/jpaek/capstone_cloud_devops.git'

    stage('Lint') {
        sh 'tidy -q -e *.html'
    }

    stage('Build') {
        docker.build('cloud_devops_capstone')
    }
    stage('Docker push') {
        docker.withRegistry('https://937431759388.dkr.ecr.us-east-2.amazonaws.com', 'ecr:us-east-2:Jenkins-docker') {
            docker.image('cloud_devops_capstone').push('latest')
        } 
    }
}
