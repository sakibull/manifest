# Roadmap to see the impact of light wieght manifest:
  **Step1:**
  Inspect all the jobs and stages of PlatCI , see the impact on the PlatCI E2E flow.

  **Step 2:**
  Going through all the PlatCI libs and Services and find out the impact based on module.

  Plan is to go with Step1 first followed by Step2.

**Approval from Anil:**_______________

# Impact on orchestrator with latest light weight design.

## CLI: pOWR pyWit check:
this will check if the provided manifest is good or not [able to parse or not]
Dependency on Manifest.xml , in our case we cannot verify because we will have platform.xml


## CLI: automerge target:
No dependency on Manifest.xml 


## CLI: {jobManager} jenkins create --schema splunk-server:
No dependency on Manifest.xml 

## CLI: {jobManager} jenkins create --schema job-config:
No dependency on Manifest.xml 


## CLI: {jobManager} jenkins create --schema pull-request:
No dependency on Manifest.xml 

## CLI: jobManager scm get-context-property:
No dependency on Manifest.xml 

## CLI: abi pyabi sourcecontrol create_status:
No dependency on Manifest.xml 

## CLI: {jobManager} kafka-producer produce:
No dependency on Manifest.xml 

## CLI: {jobManager} orchestrator generate-platform-artifacts:

powr/checker.py::verify_data # We have a verify data function call in generate-platform-artifacts , it requires Manifest.xml --> currently its a keyword argument but we do have a platform list which we can utilize when we move to light wight manifest <br/>

powr/diffcheck.py::manifest_diff_output # this method used to check the changed platforms in Manifest.xml , in our we will have multiple manifest so we should update the logic


## CLI: {automerge} latest:
No dependency on Manifest.xml 

## CLI: ${jobManager} orchestrator create-new-submission-message:
job_manager/orchestrator/utils.py::get_changed_platforms_data  # have dependency on Manifest.xml, we do have platform list which we can iterate to support light wieght


**Open**:
Check where we are pulling ingredient owner ids which requires Manifest to pull the data.



