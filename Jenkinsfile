node {
    stage('Checkout') {
        git branch: 'master', url: 'https://github.com/rizkyprayatman/simple-python-pyinstaller-app.git'
    }

    stage('Setup Python & Dependencies') {
        sh '''
        apt-get update
        apt-get install -y python3 python3-pip python3-venv

        python3 -m venv venv
        . venv/bin/activate

        pip install --upgrade pip
        pip install -r requirements.txt
        '''
    }

    stage('Build Executable') {
        sh '''
        . venv/bin/activate
        pyinstaller --onefile app.py
        '''
    }

    stage('Archive Artifact') {
        archiveArtifacts artifacts: 'dist/*', fingerprint: true
    }
}
