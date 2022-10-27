node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
       app = docker.build("192.168.56.120:9091/image-argocd-dev/devopsodia:${env.BUILD_NUMBER}")
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        sh 'docker login -u admin -p admin http://192.168.56.120:9091/repository/image-argocd-dev/'
        sh 'docker push 192.168.56.120:9091/image-argocd-dev/devopsodia:${env.BUILD_NUMBER}'
        
        // docker.withRegistry('https://registry.hub.docker.com', 'DockerHub') {
        //     app.push("${env.BUILD_NUMBER}")
        // }
    }
    
    // stage('Trigger ManifestUpdate') {
    //             echo "triggering Updatemanifest Job"
    //             build job: 'update-k8s-manifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
    //     }
}
