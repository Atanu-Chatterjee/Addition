node('master') 
{ 
	def MSBUILD = "C:/Windows/Microsoft.NET/Framework/v4.0.30319"
	def nuspecFilePath = "${env.WORKSPACE}/Addition.nuspec"
	def JobError = ""
	try 
	{
		echo "Job Started..."
		stage('Build Solution') 
		{
				BuildOut = bat(script: "${MSBUILD}/msbuild.exe /p:Configuration=Release  /p:SolutionDir=${env.WORKSPACE}")
				echo "${BuildOut} "
		}
		
		stage("Generate Publish Version")
		{		
				def nuspecFileVersion = "1.0.0.0"
				script {
				   
					nuspecFileVersion = powershell(returnStdout: true, script: 
					 '[xml] $nuspecFile = Get-Content '+nuspecFilePath+'; $nuspecFile.package.metadata.version')
					 echo 'Nuspec Version: ' + nuspecFileVersion
				}
					   
				
				def tempVersion = (nuspecFileVersion.split("\\r?\\n"))[0]
				finalVersion = "${tempVersion}.${BUILD_NUMBER}"
				echo "package final version is: ${finalVersion}"    

		}
	}
	catch(error)
	{
				JobError = error
				JobStatus = "Failed"
				echo "Error:" + ${JobError}
	}
}