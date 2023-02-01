pipeline {
    agent any
    environment {
        registryURI = "registry.hub.docker.com/"
        registry = "prakuldip/jenkinsfile_kul_app_trialtwo"
        registryCredential = "dockerhub_cred"
    }
stages {
        stage('docker image build,push to remote and delete locally') {
            steps{
                script {
                    docker.withRegistry("https://${env.registryURI}",registryCredential){
                    docker.build("${env.registryURI}${env.registry}:$GIT_COMMIT").push()
                    }
                    sh "docker image rm '${registryURI}${registry}:$GIT_COMMIT'"
                }
            }
        }
    }
    post { 
        always { 
            echo 'Deleting Workspace'
            deleteDir() /* clean up our workspace */
        }
    }
}
