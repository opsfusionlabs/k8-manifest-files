pipeline {
    agent any
    parameters {
    string(name: 'docker_image_name')
    string(name: 'release_version_tag_id' )
  }
    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }
        stage("Checkout from SCM") {
               steps {
                   git changelog: false, poll: false, url: 'https://github.com/opsfusionlabs/k8-manifest-files.git'
               }
        }

        stage("Update the Deployment Tags") {
            steps {
                sh """
                   cat deployment.yaml
                   sed -i 's/${params.docker_image_name}.*/${params.docker_image_name}:${params.release_version_tag_id}/g' deployment.yaml
                """
            }
        }

         stage("New Deploymnet File") {
            steps {
                sh " cat deployment.yaml " 
            }
        }
    }
}