# Intro
ACME process built using new best practices.

- Scrape all work items from ACME
- Upload all work items to Orchestrator
- For each work item of type WI3 (or WI5 I can't remember):
  - Scrape client details
  - Use client details to generate an SHA code
  - Open the work item's page and copy the code to the comments box of the work item
  - Set the work item status to 'Complete' in ACME and save the update

The repo contains three folders:
- **Libraries** contains the ACME and SHA libraries built in UiPath
- **Packages** contains the *GetWorkflowDetailActivites* package used as a dependency for many invoked workflows. Either add this folder as a package source in the process, or copy the package to an existing source
- **Process** contains the main UiPath process

## Setup
Open each library in ```Libraries``` in UiPath and publish the library as a package to a package source used in the process.  
In Orchestrator, create a queue named **Acme Queue** and credential named **acme-login** (names can be changed in ```Data\Config.xlsx```)

## Contributors
Gauravdeep Gosal  
Michael Tubbs

## Changes to the Robot Enterprise Framework:

- Added workflow for loading queue at start of process during initialization
- Create case log csv file during initialization for local logging in addition to Orchestrator logging
- Moved config path and config sheets from arguments to internal variables in 'InitializeAllSettings.xaml' as these are unlikely to change
- Added 'Reinitialize' state to 'Main.xaml' to allow applications to be relaunched in case of a system error
- Added 'Process Workflows' and 'Data Workflows' folders
- Created LogToCSV.xaml to log transaction statuses to locally
- Created SendFinalEmail.xaml to send an email when the robot finishes running
- Added email templates to Data\Email Templates\ for robot to use when sending final email
- Added InvokedWorkflowTemplate.xaml to be copied when creating new workflows
- Added check to see if robot should stop after reaching a maximum number of subsequent system errors in 'Finally' stage of 'Process Transaction'
- Added GlobalHandler.xaml to log error and stop in case of unhandled error.

## Changes to previous best practices:

- Changed switch to decision when try/catching an invoked workflow
- Rethrow exceptions in try/catch instead of capturing them then throwing them via a switch
- Removed 'Set Out Args' sequence from Invoked Workflow Template
- Changed "Starting Workflow - '[WorkflowName]'" to 'Starting [WorkflowName]'
- Changed "Ending Workflow - '[WorkflowName]'" to 'Ending [WorkflowName]'
