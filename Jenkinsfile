pipeline {
   agent any

   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
            powershell 'write-host "Hello world! Howdy!" `
                        write-host "Hello world again!"'
         }
      }
   }
}