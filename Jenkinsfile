pipeline {
    agent {label 'node01'}
    
    stages {
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

        stage('deleteDir') {
            steps {
                deleteDir()
            }
        }
    }
}
