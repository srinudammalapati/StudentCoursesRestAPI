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
                    docker image build -t scr:1.0 .
                    docker image tag scr:1.0 qtdev.azurecr.io/scrdev:1.0
                    docker image push qtdev.azurecr.io/scrdev:1.0
                  """    
            }
        }
        stage('container creation') {
            steps{
                sh """
                   docker image ls
                   docker image pull qtdev.azurecr.io/scrdev:1.0
                   docker container run -d -P --name scr2 qtdev.azurecr.io/scrdev:1.0
                   docker contanier ls
                  """  
            }
        }
    }
}