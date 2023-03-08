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



