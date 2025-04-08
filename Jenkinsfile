pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/iesivanhicaa/ivanJenkins.git'
            }
        }

        stage('Compile') {
            steps {
                sh '''
                    rm -rf target
                    mkdir -p target/test-classes
                    javac -d target src/app/*.java
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    echo "Compilant tests..."
                    mkdir -p test-classes
                    javac -cp "target:lib/*" -d test-classes tests/*.java

                    echo "Executant tests..."
                    java -cp "target:test-classes:lib/*" org.junit.runner.JUnitCore tests.AraleTest tests.SenbeiTest > test-output.txt 2>&1 || echo "Tests completed"

                    cat test-output.txt
                '''
            }
        }

        stage('Package') {
            steps {
                sh '''
                    cd target
                    jar cvf app.jar *
                '''
            }
        }

        stage('Upload to FTP') {
            steps {
                sh '''
                    echo "open 192.168.0.22" > ftp_commands.txt
                    echo "user ivan alumne" >> ftp_commands.txt
                    echo "binary" >> ftp_commands.txt
                    echo "cd /" >> ftp_commands.txt
                    echo "put target/app.jar" >> ftp_commands.txt
                    echo "bye" >> ftp_commands.txt
                    ftp -n < ftp_commands.txt
                '''
            }
        }
    }
}
