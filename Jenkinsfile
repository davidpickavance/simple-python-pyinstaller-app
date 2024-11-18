pipeline {
    agent any
    stages {
        stage("Build") {
            steps {
                sh "python3 -m py_compile sources/add2vals.py sources/calc.py"
                stash(name: "compiled-results", includes: "sources/*.py*")
            }
        }
        stage("Run Socket") {
            steps {
                script {
                    withCredentials([string(credentialsId: "SOCKET-API", variable: "SOCKET-SECURITY-API-KEY")]) {
                        sh "python3 -m venv .venv && PATH=.venv/bin:$PATH && pip install socketsecurity --upgrade && socketcli --target_path ."
                    }
                }

            }
        }
    }
}