node{
    def appDir = '/var/www/nextjs-app'

    stage("Clean Workspace"){
        echo 'Cleaning jenkins workspace'
        deleteDir()
    }

    stage("Clone Repo"){
        echo 'Cloning git repo'
        git{
            branch: 'main',
            url: 'https://github.com/sabaramzan123/CICD-with-Jenkins'
            }
    }

    stage("Deploying to EC2"){
        echo 'Deploying app to EC2'
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}
            rsync -av --delete 
            --exclude='.git'
            --exclude='node_modules' ./ ${appDir}

            cd ${appDir}
            sudo npm install
            sudo npm run build
            sudo fuser -k 3000/tcp || true
            npm run start
        """

        
    }
    
}