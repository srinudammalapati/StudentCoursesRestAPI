pipeline{
    agent {label 'TERRAFORM'}
    triggers { pollSCM('* * * * *') }
    stages{
        stage('vcs') {
            steps{
                git url: 'https://github.com/srinudammalapati/StudentCoursesRestAPI.git',
                branch: 'master'
            }
        }
        stage('docker image build') {
            steps{
                sh """
                    unix /var/run/docker.sock +x
                    docker image build -t scr:1.0 .
                    docker image tag scrdev:1.0 maheshstar/scr:1.0
                    docker image push maheshstar/scr:1.0
                  """    
            }
        }
        stage('container creation') {
            steps{
                sh """
                   docker image ls
                   docker image pull maheshstar/scr:1.0
                   docker container run -d -P --name scr2 maheshstar/scr:1.0
                   docker contanier ls
                  """  
            }
        }
    }
}