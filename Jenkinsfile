pipeline {
    agent any
    stages {
        stage('Prepare for AWS Codebuild') {
            steps {
                // Clean workspace
                cleanWs disableDeferredWipeout: true, deleteDirs: true
                // We need to explicitly checkout from SCM here
                checkout scm
            }
        }

        stage ("AWS Codebuild") {
            steps {
                awsCodeBuild credentialsType: 'keys', downloadArtifacts: 'false', projectName: 'iris-devops-codebuild', region: 'eu-central-1', sourceControlType: 'jenkins'
            }
        }
    }
    post {
        // Clean after build
        always {
            cleanWs(cleanWhenNotBuilt: false,
                    deleteDirs: true,
                    disableDeferredWipeout: true,
                    notFailBuild: true)
        }
    }
}
