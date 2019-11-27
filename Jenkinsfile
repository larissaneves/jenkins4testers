pipeline {
    agent {
        docker {
            image "ruby:alpine"
            args "--network=skynet"
        }
    }
    stages {
        stage("Build") {
            steps {
                sh "gem install bundler"
                sh "chmod +x build/alpine.sh"
                sh "./build/alpine.sh"
                sh "bundle install"
            }
        }
        stage("Tests") {
            steps {
                sh "bundle exec cucumber -p ci"
            }
            post {
                always {
                    cucumber failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: '**/*.json', jsonReportDirectory: 'log', pendingStepsNumber: -1, skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1                
                }
            }
        }
    }
}