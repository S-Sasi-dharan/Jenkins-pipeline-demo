pipeline {
    agent any

    environment {
        JMETER_HOME = 'C:\\Users\\ssathiyamoorthy\\Downloads\\apache-jmeter-5.6.3\\apache-jmeter-5.6.3' // <-- change this to your JMeter installation path
        RESULTS_DIR = 'jmeter-results-github'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out code from Git (main branch)..."
                git branch: 'main', url: 'https://github.com/S-Sasi-dharan/Jenkins-pipeline-demo.git'
            }
        }

        stage('Run JMeter Tests') {
            steps {
                echo "Running JMeter test plan..."
                
                // Make sure results directory exists
                bat "if not exist %RESULTS_DIR% mkdir %RESULTS_DIR%"
                
                // Run JMeter in non-GUI mode
                bat """
                %JMETER_HOME%\\bin\\jmeter.bat -n -t "C:\\Users\\ssathiyamoorthy\\Downloads\\Testing Folder\\blazedemo\\Enhancing script\\enhancingscript.jmx" -l "C:\\Users\\ssathiyamoorthy\\Downloads\\Testing Folder\\blazedemo\\Enhancing script\\blazedemo_github.jtl" -e -o "C:\\Users\\ssathiyamoorthy\\Downloads\\Testing Folder\\blazedemo\\Enhancing script\\Github_html_report"
                """
            }
        }

        stage('Archive Results') {
            steps {
                echo "Archiving JMeter reports..."
                archiveArtifacts artifacts: "${RESULTS_DIR}/**", allowEmptyArchive: true
            }
        }

        stage('Publish HTML Report') {
            steps {
                script {
                    // Check if HTML Publisher plugin is installed
                    if (fileExists("${RESULTS_DIR}/report/index.html")) {
                        publishHTML (target: [
                            allowMissing: false,
                            alwaysLinkToLastBuild: true,
                            keepAll: true,
                            reportDir: "${RESULTS_DIR}/report",
                            reportFiles: 'index.html',
                            reportName: 'JMeter Test Report'
                        ])
                    } else {
                        echo "HTML report not found, skipping HTML publish."
                    }
                }
            }
        }
    }

    post {
        always {
            echo "JMeter pipeline finished!"
        }
    }
}
