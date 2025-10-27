pipeline {
agent any
triggers { githubPush() }
stages {
stage('Checkout') {
steps { checkout scm }
}
stage('Build (fat JAR)') {
steps { sh './mvnw -B -DskipTests clean package' }
}
stage('List Artifacts') {
steps { sh 'ls -lh target/*.jar || true' }
}
stage('Archive') {
steps { archiveArtifacts artifacts: 'target/*.jar', fingerprint: true }
}
}
post {
success {echo 'Build OK' }
failure { echo 'Build failed' }
}
}
