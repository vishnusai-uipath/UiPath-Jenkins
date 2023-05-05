node {
    def mvnHome
     stage('Check Out')  {
        steps {
            git url: 'https://github.com/vishnusai-uipath/UiPath-Jenkins.git', branch: 'main'
        }
    }
    stage('install platform'){
        UiPathInstallPlatform (
            cliNupkgPath: 'C:\\Users\\Vishnu.Kothamasu\\Downloads\\UiPath.CLI.Windows.22.10.8438.32859.nupkg',
            //cliVersion: 'WIN_22.10.8438.32859',
            //forceInstall: true,
            traceLevel: 'Information')
    }
stage('Pack')
{
    UiPathPack (
    outputPath: 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Multibranch\\Output',
    projectJsonPath: 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Multibranch',
    traceLevel: 'Information',
    version: AutoVersion())
}
stage('Deploy'){
    UiPathDeploy (
    createProcess: true,
    credentials: UserPass('Orchestrator'),
    entryPointPaths: 'Main.xaml', environments: '',
    folderName: 'Shared',
    orchestratorAddress: 'https://uipathorchvk.azurewebsites.net/',
    orchestratorTenant: 'default',
    packagePath: 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Multibranch\\Output',
    traceLevel: 'Information')
}
stage('Execute TestSets'){
    UiPathTest (
    credentials: UserPass('Orchestrator'),
    folderName: 'Shared',
    orchestratorAddress: 'https://uipathorchvk.azurewebsites.net/',
    orchestratorTenant: 'default',
    parametersFilePath: '',
    testResultsOutputPath: '',
    testTarget: TestProject(environments: '', testProjectPath: 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Jenkins'),
    traceLevel: 'Information')
}
}




