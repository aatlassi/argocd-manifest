node {
    def app

    stage('Clone repository') {
      
        checkout scm
    }

    stage('Update GITHUB') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    //withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
   
                    withCredentials([usernamePassword(credentialsId: 'aatlassi-github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email aatlassi@gmail.com"   //please change this adresse email 
                        sh "git config user.name aatlassi"              //please change this name
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+stategyhq/myapp.*+stategyhq/myapp:${env.BUILD_NUMBER}+g' deployment.yml"  //change image
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job update manifest: ${env.BUILD_ID}'"
                        sh "git push --force https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argocd-manifest.git HEAD:main"               
      }
    }
  }
}
}