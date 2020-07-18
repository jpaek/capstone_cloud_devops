pipeline {

     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "It is Green"'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
             }
         }
     }
}
