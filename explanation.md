PART 1:
--------------------------------------TIMESTAMP & RENAMING IMPLEMENTATION---------------------------------

In order to implement this section, we will first capture the timestamp then rename the file and concatenate the timestamp

1. Create a new workflow called Capture-Timestamp
2. Use the assign activity and create a variable Timestamp under the Capture_Timestamp scope and assign it the value DateTime.Now.ToString("xxxx")
3. For the value of xxxx define the date and time format you want - refer to https://support.microsoft.com/en-us/office/format-a-date-and-time-field-47fbbdc1-52fa-416a-b8d5-ba24d881b698
4. Create a message box with the variable timestamp to log the timestamp captured.


-------------------------------------RENAMING IMPLEMENTATION------------------------------------------
Next we create the renaming function.
1. Inside the Capture_Timestamp Sequence, create another sequence called Renaming
2. Here we will use the Invoke method to Rename our file
3. Define 2 variable:
        - OldFile as a String under the Renaming Scope with the filepath of your Request file (as a string)
        - NewFile as a String under the Renaming Scope with the new name of your Request file as "Newname" + Timestamp variable
3. Define the below parameters in the invoke method
        - Target Type: Microsoft.VisualBasic.FileIO.FileSystem (This is a name sphere that allows us to move files, rename files etc)
        - MethodName: RenameFile
        - Target Object: Define 2 parameters as OldFile and NewFile

The steps above are all we need to capture the Timestamp and Rename the file with the timestamp concatenated. To have time is separated by - due to naming conventions that do not allow use of ":" and date is defined in long form due to same naming conventions that do not allow use of "/"

Lastly we need to intergrate this workflow with Main.xaml
1. Just before moving the Request file to the processed folder. Create a Invoke Workflow activity and locate the and import Capture-TimeStamp.xaml file
2. Modify the Move file activity to capture all documents in the folder as the name of our excel file has changed from what was initially defined as Request.xlsx using "*"


PART 2: 
Capturing additional fields:
In this section we will capture the Description, AccountName and Phone Details.
First add these field in the request.xlsx file
1. Under the SaaSAutomation Workflow Use the record function to capture the additional 3 feilds and add them under the Web Sequence.
2. Add 3 additional arguments to cover the 3 additional field in the In direction.
3. Replace the type fields with the newly defined arguments.
To integrate the newly defined scope, follow the steps below
4. On the main workflow, create 3 additional variables under the sequence as strings
5. On the main workflow, under the SaaSAutomation Invoke workflow import the arguments and map them to the defined variables

PART 3:
Use Hotkeys to terminate the automation
1. In the main workfflow create a new variable called Trigger and set it to False
2. Introduce an if activity and define the trigger variable.
3. In the the activity define the already defined activities in the workflow.
4. In the else activity define a new trigger scope and define a hotkey of your choice.
        - under the actions activity, define a terminate workflow activity and add a relevant message.
        - To track this action add a log message with a message of your choice.
5. Edit the first message to incorporate the newly added task. E.g Agent is ready, please use ALT + s to start the automation. To stop the automation use ALT + h


