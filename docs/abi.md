# Impact on abi with latest light weight design.

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
powr/checker.py

Check where we take ingredient owner ids which requires Manifest to pull the data.

{automerge} latest:
No dependency on Manifest.xml 

${jobManager} orchestrator create-new-submission-message:
It does have dependency on Manifest,
https://github.com/intel-innersource/frameworks.devops.platform-integration-framework.job-manager/blob/main/job_manager/scripts/orchestrator.py#L519

job_manager/orchestrator/utils.py::get_changed_platforms_data have dependency on Manifest.xml, we do have pplatform list which we can iterate to support light wieght





