node {
    stage('git checkout') {
        git 'file:///D:/WorkArea/Demo_CI/SsdtDevOpsDemo'
    }
    
    stage('Build Dacpac from SQLProj') {  
        bat "\"${tool name: 'Default', type: 'msbuild'}\" /p:Configuration=Release"
        stash includes: 'SsdtDevOpsDemo\\bin\\Release\\SsdtDevOpsDemo.dacpac', name: 'theDacpac'
    }
 
    stage('Deploy Dacpac to SQL Server') {
        unstash 'theDacpac'
        bat "\"C:\Program Files\Microsoft SQL Server\140\DAC\bin\sqlpackage.exe\" /Action:Publish /SourceFile:\"SsdtDevOpsDemo\\bin\\Release\\SsdtDevOpsDemo.dacpac\" /TargetServerName:(local) /TargetDatabaseName:Chinook"
    }
}
