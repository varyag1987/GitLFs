pipeline {
    agent {label 'node01'}
    
    stages {
        stage('Verify non LFS files') {
            steps {
                script {
                    def expected = [
                        'NonGitLFs.txt': 'NonGitLFs',
                        'folder/NonFolderGitLFs.txt': 'NonFolderGitLFs'
                    ]
                    expected.each { fileName, expectedValue ->
                        def actual = readFile(file: fileName, encoding: 'UTF-8').trim()
                        if (actual != expectedValue) {
                            error("Non LFS content missing or incorrect: ${fileName}. Enable Git LFS pull after checkout in Branch Sources.")
                        }
                    }                    
                }
            }
        }

        stage('Verify LFS files') {
            steps {
                script {
                    def expected = [
                        'GitLFs.txt': 'GitLFs',
                        'folder/folderGitLFs.txt': 'folderGitLFs'
                    ]
                    expected.each { fileName, expectedValue ->
                        def actual = readFile(file: fileName, encoding: 'UTF-8').trim()
                        if (actual != expectedValue) {
                            error("LFS content missing or incorrect: ${fileName}. Enable Git LFS pull after checkout in Branch Sources.")
                        }
                    }                    
                }
            }
        }
    }

    post {
        always {           
            echo "Bye 1"
            deleteDir()
        }
    }
}
