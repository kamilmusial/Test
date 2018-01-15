#!/usr/bin/groovy
def fetch(){
    def cf= [
        server: 'http://127.0.0.1:8000',
        app: 'example',
        hash: '663ae89b23e65fbc2bd8f1541e65f2b090fb2a2f',
        output: 'conf.php',
        source: 'conf.yml',
        format: 'php',
        environment: 'development',
        stage: 'development'
    ]

    sh "wget ${cf.server} -O configfetcher.phar"
    sh "echo '${cf.hash}  configfetcher.phar' | shasum -c"
    sh "php configfetcher.phar ${cf.app} --output=${cf.output} --format=${cf.format} --source=${cf.source} --environment=${cf.environment} --stage=${cf.stage}"
    sh 'rm -rf configfetcher.phar'
}

pipeline {
    agent {
        label "cf-test"
    }
    stages {
        stage('Config Fetcher') {
            steps{
                dir('/Users/kamil.musial/projects/test/pull/test/') {
                    fetch()
                }
            }
        }
    }
}
