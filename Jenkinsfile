pipeline {
  agent any

   stages {
      stage('Install Dev Dependencies') {
        steps {
          echo "npm install"
        }
      }
      stage('Test') {
        steps {
          parallel (
            ClientTest: {
              echo "Client Test"
            },
            ClientJest: {
              echo "Client Jest"
            },
            ServerTest: {
              echo "Server Test"
            },
            Lint: {
              echo "Lint"
            },
            LightHouse: {
              echo "LightHouse"
            }
          )
        }
      }
    stage('Deploy - QA') {
        steps {
           echo "sh './deploy qa'"
        }
    }

    stage('Install QA Dependencies') {
      steps {
        echo "gem install bundler"
        echo "bundle install"
      }
    }
    stage('Browser Testing') {
      steps {
        parallel (
          firefox: {
            echo "Firefox Testing"
          },
          Chrome: {
            echo "Chrome Testing"
          },
          IE: {
            echo "IE Testing"
          },
          MicrosoftEdge: {
            echo "Microsoft Edge Testing"
          }
        )
      }
    }
    stage('Merge into Master') {
                steps {
                    input "Is the PR approved?"
                }
            }
      stage('Deploy - Acceptance') {
          steps {
             echo "sh './deploy acceptance'"
          }
      }
    stage('Install QA Master Dependencies') {
        steps {
          echo "gem install bundler"
          echo "bundle install"
        }
      }
      stage('Final Browser Testing') {
        steps {
          parallel (
            firefox: {
              echo "Firefox Testing"
            }
          )
        }
      }
     stage('Happy to go Live') {
                      steps {
                          input "Are you happy to sign off?"
                      }
                  }
     stage('Deploy - Production') {
                steps {
                    echo "sh './deploy production'"
                }
            }
      stage('Post Live Automation') {
              steps {
                parallel (
                  firefox: {
                    echo "Firefox Testing"
                  }
                )
              }
            }
       }
}
