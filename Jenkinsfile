node {
    stage 'Checkout'
    git url: 'https://github.com/jpaek/capstone_cloud_devops.git'
    
    stage('Install Dependency')
    make setup
    make install
    
    stage('Lint') {
    . venv/bin/activate
    make lint
    
    stage('Build') {
        docker.build('cloud_devops_capstone')
    }
    stage('Docker push') {
        docker.withRegistry('https://937431759388.dkr.ecr.us-east-2.amazonaws.com', 'ecr:jenkins') {
            docker.image('cloud_devops_capstone').push('latest')
        } 
    }
}
