node {
    def app
    
    stage('Clone Repositry') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email odark@naver.com"
                    sh "git config user.name odark"
                    sh "cat deployment.yaml"
                    sh "sed -i s+odark/test.*+odark/test:${DOCKERTAG}+g deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernestesmanifest.git HEAD:main"
                }
            }
        }
    }
}