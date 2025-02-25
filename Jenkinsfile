pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // This checks out the code from the repository.
                bat 'git clone "https://github.com/YuriKha/class7-ci.git"'
            }
        }
        stage('Run Script') {
            steps {
                script {
                    // Jenkins sets BRANCH_NAME for multibranch pipelines.
                    if (env.BRANCH_NAME == 'main') {
                        // For the master branch, simply run the script.
                        echo "Running myapp.py on master branch..."
                        sh 'python myapp.py'
                    } else if (env.BRANCH_NAME?.startsWith("feature")) {
                        // For any branch starting with "feature", run the script and then fail intentionally.
                        echo "Running myapp.py on a feature branch..."
                        sh 'python myapp.py'
                        error("Intentional failure for feature branch")
                    } else {
                        echo "Branch ${env.BRANCH_NAME} does not trigger any specific action."
                    }
                }
            }
        }
    }
}