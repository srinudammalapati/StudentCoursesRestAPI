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
                    docker image build -t scrdev:1.0 .
                    docker image tag scrdev:1.0 maheshstar/scrdev:1.0
                    docker image push maheshstar/scrdev:1.0

                  """    
            }
        }
        stage('k8s deploy') {
            steps{
                sh """
                   kubectl apply -f depolyment/sqlpvc.yaml
                   kubectl apply -f depolyment/sqldb.yaml
                   kubectl apply -f depolyment/scrapp.yaml

                  """   
            }
        }
    }
}