pipeline
{
    agent any
    stages
    {
        stage ('continuous Download')
        {
            steps
            {
                 git 'https://github.com/rajupoloj/hello-world.git'
            }
        }
        stage ('continuous build')
        {
            steps
            {
                 sh '/opt/maven/bin/mvn package'
            }
        }
        stage ('continuous Deploy')
        {
            steps
            {
                 sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''ansible-playbook /opt/docker/regapp.yml;
sleep 10;
ansible-playbook /opt/docker/deployregapp.yml''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//docker', remoteDirectorySDF: false, removePrefix: 'webapp/target/', sourceFiles: 'webapp/target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}
