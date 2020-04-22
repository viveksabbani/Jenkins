pipeline {
   agent any

   stages {
      stage('build') {
         steps {
            powershell("""
                    new-item buildText.txt
                    Add-Content buildText.txt \$(cat myTextFile.txt)
            """) 
         }
      }
      stage('versioning'){
          steps{
              powershell("""
                    if(Test-Path ./version.txt  -PathType leaf){
                        Rename-Item -Path buildText.txt -NewName "buildText_v\$(cat version.txt).txt"
                        \$version= \$(cat version.txt)
                        Set-Content -Path version.txt -Value "\$($version+1)"
                    }else{
                        New-Item version.txt
                        Add-Content version.txt "1"
                    }
              """)
          }
      }
      stage('Deploy'){
          steps{
              powershell("""
                    jfrog rt c TestServer --url=http://localhost:8081/artifactory --user=admin --password=artifactory@01
                    jfrog rt u "buildText*.txt" generic-local/buildOutput/
              """)
          }
      }
   }
}