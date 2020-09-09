node('master') 
{ 
	def MSBUILD = "C:/Windows/Microsoft.NET/Framework/v4.0.30319"
	try 
	{

		stage('Build Solution') 
		{
					BuildOut = bat(script: "${MSBUILD}/msbuild.exe /p:Configuration=Release  /p:SolutionDir=${WORKSPACE}")
					echo "${BuildOut} "
		}
	}
}