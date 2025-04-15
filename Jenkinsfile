node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    // Only runs this stage if on 'dev' branch
    if (env.BRANCH_NAME == 'dev') {
        stage('Build image') {
            app = docker.build("mariosek1/kiii-jenkins")
        }

        stage('Push image') {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
            }
        }
    } else {
        stage('Skip Docker') {
            echo "Skipping Docker build & push for branch: ${env.BRANCH_NAME}"
        }
    }
}
