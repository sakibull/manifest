# Impact on orchestrator with latest light weight design.

Orchestrator:


pOWR pyWit check:
this will check if the provided manifest is good or not [able to parse or not]
Dependency on Manifest.xml , in our case we cannot verify because we will have platform.xml


automerge target:
No dependency on Manifest.xml 


{jobManager} jenkins create --schema splunk-server:
No dependency on Manifest.xml 

{jobManager} jenkins create --schema job-config:
No dependency on Manifest.xml 


{jobManager} jenkins create --schema pull-request:
No dependency on Manifest.xml 

jobManager scm get-context-property:
No dependency on Manifest.xml 

abi pyabi sourcecontrol create_status:
No dependency on Manifest.xml 

{jobManager} kafka-producer produce:
No dependency on Manifest.xml 

{jobManager} orchestrator generate-platform-artifacts:

We have a verify data function call in generate-platform-artifacts , it requires Manifest.xml --> currently its a keyword argument but we do have a platform list which we can utilize when we move to light wight manifest.
https://github.com/intel-innersource/frameworks.devops.platform-integration-framework.job-manager/blob/main/job_manager/scripts/orchestrator.py#L371

defined in pOWR which should also be updated:
powr/checker.py::verify_data
powr/diffcheck.py::manifest_diff_output # this method used to check the changed platforms in Manifest.xml , in our we will have multiple manifest so we should update the logic


{automerge} latest:
No dependency on Manifest.xml 

${jobManager} orchestrator create-new-submission-message:
It does have dependency on Manifest,
https://github.com/intel-innersource/frameworks.devops.platform-integration-framework.job-manager/blob/main/job_manager/scripts/orchestrator.py#L519

job_manager/orchestrator/utils.py::get_changed_platforms_data have dependency on Manifest.xml, we do have platform list which we can iterate to support light wieght


Open:
Check where we are pulling ingredient owner ids which requires Manifest to pull the data.



