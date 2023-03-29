# OWR PlatformCI Build Migration During Planned Power shutdown or Maintainance Activity.

### Goal
 ###### To provide robust PlatformCI build Infra which is available round the clock\zero-downtime.<br>
 ###### To provide a uninterrupted production environrment to support continuous PlatformCI BKC build support.<br>
 ###### To eliminate any chance of inavailability of the Production environement.<br>

### prerequisites
###### Check with BKC Team for Release plans and sync those kits.....

### Proposed Flow
###### During shutdown activity all builds should be redirected to the agent geo which does not have any impact during the shutdown activity. In a nutshell, switch the Jenkins agent location in case the mentioned Agent label geo is having planned shutdown
    * we need to update the default agent label defined in Jenkins file based on the downtime,
      current default agent label contains a combination of both BA and US Agents ,during downtime
      we will update the default agent label based on the downtime geo location.
      
    * we do provide an option to the user to run the image build on specific geo location, geo location label defined in props file.
    
    * Make a JSON file in Manifest repo example: {downtime_labels:"dcgba"} , if agent label defined in props matches with downtime_label
      then will run the build on default lable itself [Requires changes in Jenkins file].

### All latest ingredient versions may not be available in the Artifactory geo location where the targetted builds should move during the shutdown activity.
    one or two day prior to the downtime activity, run the wit sync commands for all active platforms which created to run on the impacted geo location.
    This excercise will ensure that the all the ingredient versions are cached to Artifactory geo where builds will run during downtime.
    Repeat the process couple of hours prior to the shutdown activity so that recent Ingredient versions are also get cached.

### Post downtime activity Task

    * Remove the label from downtime_labels defined in JSON file.
    * revert the default label changes from jenkins files.

**Note** - **'owr2_platform-1.0.0'** - default label
   *consist of BA & OR agents. So need to update default pool to 'platformci_win_us' or dcgba during downtime. Very few builds run on SH agents and there are very    few nodes, so we will not update it to DCGSH for BA or OR shutdown activity.
