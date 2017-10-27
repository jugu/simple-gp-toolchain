# Creating a devops toolchain that integrates with Globalization Pipeline to provide automated application translations

### Step 1 - Create toolchain

- Create a simple toolchain by clicking on the `Create a Toolchain` button in the README document
- Configure parameters for the following services:
  - **Globalization Pipline** (make sure you have credentials for an existing Globalization Pipeline instance, other fields can be modified as per requirement)
  - **Sacuelabs** (provide username, and access key)
  - **Slack** (provide hook url, channel name, and team name)
  - **Delivery Pipeline** (preconfigured for this tutorial)
  - **Github Repos** (preconfigured using clone of public git repo)

### Step 2 - Modify a source (english) resource file 
  - In the cloned git repo, modify the `resources_en.json` file which contains source language key value pairs
  - git add, commit, and push the file into the repository
  
### Step 3 - Wait for Pull Request and merge after review
  - As soon as the resource file is pushed to the repository, then as part of the preconfigured delivery pipeline following things occur automatically:
    - The globalization pipline which was preconfigured to look for changes in source translation json file will trigger Machine translation of all the source language resource files.
    - After the Machine translation has been completed a slack notification will be sent to the slack channel configured as part of this toolchain.
    - The user can then see a Pull Request being created in the git repo which contains translated resource files which can be merged into the git repository
    - The user can then review the pull request and merge the Pull Request changes once satisfied.

### Step 4 - Trigger the build stage of delivery pipeline
   - The user should now trigger the build stage of the preconfigured pipeline
   - BUILD - In the build stage of the pipeline the node application undergoes a npm build
   - DEPLOY-STAGING - After the success of the build stage, in the deploy-staging part of the pipeline, the node app is deployed to staging enviroment
   - SAUCE-TEST - After the successful deployment in staging, using the saucelabs configuration, end to end tests are performed where using the node test cases translations/appearance can be validated in different browsers
   - DEPLOY-PRODUCTION - After the success of the saucelabs test, the app is deployed to production with the updated translations   
    
   
