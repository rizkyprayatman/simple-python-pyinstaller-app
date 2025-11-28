node {

    stage('Checkout') {
        checkout scm
    }

    stage('Setup Python') {
        sh '''
        apt-get update
        apt-get install -y python3 python3-pip
        python3 --version
        pip3 --version
        '''
    }

    stage('Install Dependencies') {
        sh 'pip3 install -r requirements.txt'
    }

    stage('Unit Test') {
        sh 'python3 -m pytest --maxfail=1 --disable-warnings -q'
    }

    stage('Build Executable') {
        sh 'pip3 install pyinstaller'
        sh 'pyinstaller --onefile app.py'
    }

    stage('Archive Artifact') {
        archiveArtifacts artifacts: 'dist/*', fingerprint: true
    }
}
