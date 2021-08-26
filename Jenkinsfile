pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh 'pip3 install -r requirement.txt'
            }
        }
        stage('Test') { 
            steps {
                sh 'python manage.py test'
            }
        }
        stage('Deploy To Staging') { 
            steps {
                sh 'source venv/bin/activate; \
                cd polling; \
                git pull origin master; \
                pip  install -r requirement.txt --no warn-script-location; \
                python manage.py migrate; \
                deactivate; \
                sudo systemctl restart nginx; \
                sudo systemctl restartgunicorn '
            }
        }
        stage('Deploy TO production') { 
            input{
                meaasge "shall we deploy to production"
                ok "yes"
            }
            steps {
                sh 'source venv/bin/activate; \
                cd polling; \
                git pull origin master; \
                pip  install -r requirement.txt --no warn-script-location; \
                python manage.py migrate; \
                deactivate; \
                sudo systemctl restart nginx; \
                sudo systemctl restartgunicorn '
            }
        }
    }
}