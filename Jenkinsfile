node {
    def appDir = '/var/www/nextjs-app'

    stage('Clean Workspace'){
        echo 'Cleaning Jenkins Workspace'
        deleteDir()
    }

    stage('Clone Repo'){
        echo 'Cloning the repo'
        git(
            branch: 'main',
            url: 'https://github.com/sabaramzan123/CICD-with-Jenkins'
        )

    }

    stage('Deploy to EC2'){
    echo 'Deploying to EC2'
    sh """
        sudo mkdir -p /var/www/nextjs-app
        sudo chown -R jenkins:jenkins /var/www/nextjs-app

        rsync -av --delete --exclude='.git' --exclude='node_modules' --exclude='.next' ./ /var/www/nextjs-app

        cd /var/www/nextjs-app
        npm install --legacy-peer-deps
        npm run build
    """
    
  }

}