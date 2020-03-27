node('chris') {
   withEnv([
      'DEVICE=cheeseburger', 
      'BRANCH=lineage-17.1',
      'VERSION=17.1',
      'ROMTYPE=UNOFFICIAL',
      'OTA_ROMTYPE=unofficial',
      'SYSTEM_PATH=/home/exodusnick/LineageOS/17.1_LineageOS',
      'OUTPUT_PATH=/home/exodusnick/LineageOS/17.1_LineageOS/out/target/product',
      'FILENAME=lineage-17.1-$TARGET_DATE-UNOFFICIAL_microG_ready-$env.DEVICE.zip',
      'SEARCH_FILENAME=lineage-17.1-$TARGET_DATE-UNOFFICIAL-$env.DEVICE.zip',
      'URL=https://los-legacy.de',
      'SSH_URL=los-legacy.de',
      'LOCAL_MANIFESTS_URL=https://raw.githubusercontent.com/los-legacy/local_manifests/lineage-17.1/cheeseburger.xml',
      'LOCAL_MANIFESTS_PATH=.repo/local_manifests', 
   ]) {
   stage('Preparation') { // for display purposes
            
                checkout([$class: 'GitSCM', 
                branches: [[name: "$BRANCH"]], 
                doGenerateSubmoduleConfigurations: false, 
                extensions: [[$class: 'CleanBeforeCheckout', 
                deleteUntrackedNestedRepositories: true], 
                [$class: 'RelativeTargetDirectory', relativeTargetDir: '/home/exodusnick/LineageOS/17.1_LineageOS/build_script']], 
                submoduleCfg: [], 
                userRemoteConfigs: [[credentialsId: 'e1791597-2cce-40b2-8357-fcbc77a559d5', 
                url: "https://github.com/los-legacy/${DEVICE}.git"]]
                ])
                sh label: 'Preparation', script: 'source $SYSTEM_PATH/build_script/preparation.sh'
            }
            stage('RepoSync') { // for display purposes
                sh label: 'RepoSync', script: 'source $SYSTEM_PATH/build_script/reposync.sh'
            }
            stage('Build') { // for display purposes
                sh label: 'Build', script: 'source $SYSTEM_PATH/build_script/build.sh'
            }
            stage('OTA Upload') { // for display purposes
                sh label: 'OTA Upload', script: 'source $SYSTEM_PATH/build_script/upload.sh'
            }
        }
    }
         """
      }
   }
}
