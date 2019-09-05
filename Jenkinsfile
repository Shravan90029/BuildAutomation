pipeline {
    agent any 
    environment { 
        CC = 'Production Environment'
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Paramesh', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    options { timestamps() 
        
    }
    stages {
        stage('Build') { 
            
                input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
               echo 'hello world' 
            }
        }
        stage('Test') { 
            steps {
                echo 'hello world1' 
        script {
                    def browsers = ['chrome', 'firefox']
                    for (int i = 0; i < browsers.size(); ++i) {
                        echo "Testing the ${browsers[i]} browser"
                    }
                    
                    def post = new URL("https://ngpsservice--tst1.custhelp.com/AgentWeb/api/elementmanager/authentication/authToken").openConnection();
                    def message = '{"message":"this is a message"}'
                    post.setRequestMethod("POST")
                    post.setDoOutput(true)
                    post.setRequestProperty("Content-Type", "application/json")
                    post.setRequestProperty("Authorization","Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IlBhcmFtZXNoMSIsInBhc3N3b3JkIjoiUGFyYW1lc2gwIn0.uhD812oOfleLLN8EpwxQoSpZdtieU1cR9huys59tvEk")
                    post.setRequestProperty("interfaceUrl", "https://ngpsservice--tst1.custhelp.com/cgi-bin/ngpsservice.cfg")
                    post.getOutputStream().write(message.getBytes("UTF-8"));
                    def postRC = post.getResponseCode();
                    println(postRC);
                    if(postRC.equals(200)) {
                        println(post.getInputStream().getText());
                    }
                }
            }
        }
        stage('Deploy') { 
            steps {
                  echo 'hello world2' 
            script {
                    println('Hello World');
                      def get = new URL("https://virtserver.swaggerhub.com/ShravanHome/Sampleapi01/1.0.0/pet/findByStatus?status=available").openConnection();
        def getRC = get.getResponseCode();
        println(getRC);
        if(getRC.equals(200)) {
            println(get.getInputStream().getText());
    }
                }
            }
        }
        stage('golive'){
            when {
                branch 'production'
            }
            steps {
                echo 'golive deplyment'
            }
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
            build 'Maven1'
        }
         success {
            echo 'I succeeeded!'
            mail to: 'team@example.com',
             subject: "Build Sccuess",
             body: "Hi paramesh , build is successful"
        }
}
}
