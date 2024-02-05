pipeline {
    agent { label 'agent_237' } // Specify the label of your AWS agent
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/princekumarsh/jenkins_test.git' // Replace with your GitHub repository URL
            }
        }

        stage('Upload to AWS Agent') {
            steps {

                script {
            def privateKey = """
                                        -----BEGIN RSA PRIVATE KEY-----
                        MIIEpQIBAAKCAQEAvhEQEzG12SUCsfE/Ou0MYEa7L5biGtnIZvMD55Le9H8vJXDP
                        J/a092TFBzJiWxE9oDourTnfeBVNbxsLvpjkUCFx38XsQ88R08SBAZSIgmZAMp4y
                        j8kuCmTx0JxL0bPH2ihMQ0kRGinMucE5O/iXjWsPMvW8A4m9/zcmM3fpR6bY0ecO
                        +JRVKhRiBhTi2iPOfy6JnwkX3cpsl9N7VKHUx1JR4q2rH66O/JQG6A83A1QstVuD
                        IgGCrXGuS89u4aYLRx55LtZ6i4WOecPsHMz2c4D/54T3S58XwhUaIefDS5jWCWEo
                        /NwQm2BWaUlxHfLoYCTsrgtD4M/0S9URTYYdLwIDAQABAoIBAQCTrCAoOZxHbUkN
                        xhnRh7Hw76OqEvnz0LeyvSeQef1+S37vARoCu9zYxlOLBuuCQ//0iKAReQCWhT6X
                        j5Ttbk8drw6RxW6PNMhuF6P//U6euiEw8tbn/nAmJU34Piduc9dYOa0fLhr6j/V/
                        cZAtdzUQ7FhvyJteyFt1enzUylrWjoOFuljC49qX+/NNlpOXilYxasiqXrSipDF/
                        lXupPdiZCLK2HavmmM30npOFdNsBCbeDrdy9DejZo7yKB60T6Eq6UIuc6jTza5oW
                        pH4OavP6I/xN5/6LaN4Pi324uoXPhPR56HX8MmXe9Lh1zWBVG+/pIkvncBgEBGpp
                        jE+VajZBAoGBAPhIKAMCiQQ+E9A8TdHlfr/BXTNj2FqgmpBEwTuaejqwDpTBBKzA
                        baMycwz/Nw4NXqLcAxA5nW83zBupiEpkEce0suDm02C/JGNuGZIcNb8PvH/GCQps
                        XwSTIv1N7Pe6jKUmNpZQsWiSFd7ooShprfAi4TcXfVHlR7QM/F9FcoUhAoGBAMP5
                        oD7HYUkW9x29FBkdZhacY636HcuTcjv14ovAM0lvDhDENI89ppDvDcZujmxKdEqW
                        /97hetD4zwY+nB0EQF2FdnreGMKkUmtuxsdyzCUWvChRxIBYLACek13EsxgOYbSP
                        iuwZnEEnpkic0+mrkLcd1gHOyHgbrS52jG5kRghPAoGBALtl6x1qenTDTj0sZyh4
                        ahTeJDS3tgOhmUgvPRJ55KwLWtYYYijqDVbSq1gyAiIPIVEXcxB6DER3/w0aBw7v
                        PSRZVXK/huhNHXAXGCHaPQ77F7Hxjb1aUtWnIQ/EE4pgOewlTapjOaTOLsfTGmDg
                        czL/gLIOfr6jql1SN+LJDklBAoGAIDPXqhk3GjyE1MUqFUpoaRS/qGnuFXKgFcw8
                        srwdcVanWAf1nwgBY9V0TQQDsTW20D7pwqUIemg4FI2bN4VoUjXJFz2BkhJQXMjy
                        LvnlI78Nog51nKVgbaWhD4pv52cNlQ71RACdVXN/dnUWuVHw0LY9YUSqWlop5fWi
                        88zUWS8CgYEAyB1oaN2IEMkN5beQ+SwoRnEmFiUjZCvAj9sIf14JhHINcWbufBZ3
                        K9cSKCTPW2B3am7L+kygHmM2Qt3ZzWZLohvDxGzcdTLBLMl6h0RWdMtRj6nuXUcj
                        yJiNmoBkq62q2BAHhFpTeMnpbMqCCOmLbDRGgaoR+kdRERNmOERp1kQ=
                        -----END RSA PRIVATE KEY-----
            """
            
            sh "echo '${privateKey}' > temp-key.pem"
            sh 'scp -i temp-key.pem -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -r * ubuntu@13.201.47.237:/usr/share/nginx/html'
        }

                
                //sh 'scp -i /home/princekumar/Downloads/test-key-pair.pem -r * ubuntu@13.201.47.237:/usr/share/nginx/html' // Replace with your AWS agent IP and destination path
                // sh 'scp -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -i /home/princekumar/Downloads/test-key-pair.pem -r * ubuntu@13.201.47.237:/usr/share/nginx/html'
            }
        }

        stage('Deploy with Nginx') {
            steps {
                sh 'ssh -i /home/princekumar/Downloads/test-key-pair.pem ubuntu@13.201.47.237 "sudo systemctl restart nginx"' // Restart Nginx or perform any other deployment tasks
            }
        }
    }
}
