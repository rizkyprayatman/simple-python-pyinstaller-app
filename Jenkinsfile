node {
    stage('Checkout') {
        git branch: 'master', url: 'https://github.com/rizkyprayatman/simple-python-pyinstaller-app.git'
    }

    stage('Setup Python') {
        sh '''
        apt-get update
        apt-get install -y python3 python3-pip python3-venv
        python3 -m venv venv
        . venv/bin/activate
        pip install pyinstaller
        pip install pytest
        '''
    }

    stage('Run Tests') {
        sh '''
        . venv/bin/activate
        pytest -q
        '''
    }

    stage('Build Executable') {
        sh '''
        . venv/bin/activate
        pyinstaller --onefile sources/add2vals.py --name add2vals
        '''
    }

    stage('Archive Artifact') {
        archiveArtifacts artifacts: 'dist/*', fingerprint: true
    }
}
