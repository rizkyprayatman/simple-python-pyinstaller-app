node {
    stage('Checkout') {
        git branch: 'master', url: 'https://github.com/rizkyprayatman/simple-python-pyinstaller-app.git'
    }

    stage('Setup Python') {
        sh '''
        apt-get update
        apt-get install -y python3 python3-pip
        pip3 install --upgrade pip
        pip3 install pyinstaller
        '''
    }

    stage('Install Dependencies') {
        sh '''
        if [ -f "requirements.txt" ]; then pip3 install -r requirements.txt; fi
        '''
    }

    stage('Build Binary') {
        sh '''
        pyinstaller --onefile app.py
        '''
    }

    stage('Archive Artifact') {
        archiveArtifacts artifacts: 'dist/**', fingerprint: true
    }
}
