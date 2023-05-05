node {
    def mvnHome
    stage('install platform'){
        UiPathInstallPlatform (
            cliNupkgPath: 'C:\\Users\\Vishnu.Kothamasu\\Downloads\\UiPath.CLI.Windows.23.2.8467.25277.zip.nupkg',
            //cliVersion: 'WIN_22.10.8438.32859',
            //forceInstall: true,
            traceLevel: 'Information')
    }
stage('Pack')
{
    UiPathPack (
    outputPath: 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Jenkins\\Output',
    projectJsonPath: 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Jenkins',
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
    packagePath: 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Jenkins\\Output',
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




