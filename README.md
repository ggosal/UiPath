Changes to the Robot Enterprise Framework:

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

Changes to previous best practices:

- Changed switch to decision when try/catching an invoked workflow
- Rethrow exceptions in try/catch instead of capturing them then throwing them via a switch
- Removed 'Set Out Args' sequence from Invoked Workflow Template
- Changed "Starting Workflow - '[WorkflowName]'" to 'Starting [WorkflowName]'
- Changed "Ending Workflow - '[WorkflowName]'" to 'Ending [WorkflowName]'