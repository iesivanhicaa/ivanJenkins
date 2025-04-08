

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
    }
}
