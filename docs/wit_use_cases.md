# WIT Use Cases on latest light weight design.

At its fundamental level, there are five wit options been used which requires Manifest.xml.
Command           Description
Submit            Combines the Update and Deploy command; Commits the updated manifest and uploads ingredients
Sync-V2           Reads the Manifest and copies the content to the local work space
Update            Update an ingredient in the manifest
show              Print entries from the manifest to the console
ingredient        Ingredient actions

## Decision Table Schema
| Command | Description|
|-|-|
| Submit   | Combines the Update and Deploy command; Commits the updated manifest and uploads ingredients|
| Sync-V2  | Reads the Manifest and copies the content to the local work space|
| Update  | Update an ingredient in the manifest|
| show   | Print entries from the manifest to the console|
| ingredient    | Ingredient actions |

## Wit submit

### Pass scenarios:

#### wit submit ingredient without deploying:

    wit submit mva_test_apps --version 1.0.58.1 --platform LNL-M-SV2-PSS --commit-message "checking the retention period for this" --Manifest LNL-M-SV2-PSS.xml

    Working as expected as we have --Manifest flag where we can pass the manifest file path used as above.

    Here is the branch created from wit submit 
    https://github.com/sakibull/manifest/pull/2

#### wit submit ingredient with deploying:

    wit submit mva_test_apps --version 1.0.58.1-test --platform LNL-M-SV2-PSS --commit-message "checking the retention period for this" --path         C:\Users\sakibull\Music\light_manifest\manifest\Packages\mva_test_apps\MVA-Test-Apps-1.0.58.1-amd64.zip --manifest "C:\Users\sakibull\Music\light_manifest\manifest\LNL-M-SV2-PSS.xml --user sakibull --password *** 
    
    Working as expected as we have --Manifest flag where we can pass the manifest file path used as above.

    Here is the branch created from wit submit 
    https://github.com/sakibull/manifest/pull/3

### Failed scenarios:
#### wit submit ingredient to update whole platform family [Failed]:
    update all platform configs from the same Platform Family using a single command

    wit submit mva_test_apps --version 1.0.58.1-test --platform LNL-M-SV2-PSS --commit-message "checking the retention period for this" --path         C:\Users\sakibull\Music\light_manifest\manifest\Packages\mva_test_apps\MVA-Test-Apps-1.0.58.1-amd64.zip --manifest "C:\Users\sakibull\Music\light_manifest\manifest\LNL-M-SV2-PSS.xml --user sakibull --password *** 
    

## Wit sync

### Pass scenarios:

#### wit sync-v2 ingredient:

        wit sync-v2 --ing mva_test_apps --platform LNL-M-SV2-PSS --Manifest LNL-M-SV2-PSS.xml
    
    Working as expected as we have --Manifest flag where we can pass the manifest file path used as above.

#### wit sync type specific ingredients for specific platform:
    wit sync --source --type bldtool  --platform MEH-SRV-HCC-WIN19 --Use-Project-Defaults --Manifest LNL-M-SV2-PSS.xml
    Working as expected as we have --Manifest flag where we can pass the manifest file path used as above.

#### wit sync all the ingredients for specific platform:

    wit sync-v2  --platform MEH-SRV-HCC-WIN19 --Use-Project-Defaults --Manifest LNL-M-SV2-PSS.xml   
    Working as expected as we have --Manifest flag where we can pass the manifest file path used as above.

#### wit sync only the specific ingredients:

    wit sync-v2 Ingredients --only mva_test_apps --Manifest LNL-M-SV2-PSS.xml
    Working as expected.

#### wit sync only the specific ingredient for specific platform:
    wit sync-v2 Ingredients --only mva_test_apps --Manifest LNL-M-SV2-PSS.xml --platform LNL-M-SV2-PSS
    Working as expected.

## Wit update

### Pass scenarios:

#### reset to platform default using wit update on specific ingredients:

    wit update mva_test_apps  --Reset-Platform-Default --manifest LNL-M-SV2-PSS.xml --platform LNL-M-SV2-PSS
    working as expected.

#### update the type of the project:
    wit update mva_test_apps  --manifest LNL-M-SV2-PSS.xml --Type bldtool --Default
    working as expected


## Wit Show

### Pass scenarios:

#### wit show command to retrive the global artifactory path:

    wit show --artifactory-glb --manifest LNL-M-SV2-PSS.xml
    working as expected

#### wit show command to retrive the ingredient details:

    wit show --ingredients vtune --manifest LNL-M-SV2-PSS.xml
    working as expected

#### wit show details of a single ingredient
    wit show --ingredient vtune --manifest LNL-M-SV2-PSS.xml --platform LNL-M-SV2-PSS --property PACKAGEPATH
    wit show --ingredient vtune --manifest LNL-M-SV2-PSS.xml --platform LNL-M-SV2-PSS --property VERSION

    working as expected.

## Wit locate

### Pass scenarios:
#### locate the ingredient
    wit ingredient locate --ingredient mva_test_apps --version 1.0.58.1-test1 -m LNL-M-SV2-PSS
    working as expected
