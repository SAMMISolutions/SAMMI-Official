=================================
Building SAMMI Extensions
=================================
---------------------------------
- 1. Overview and Prerequisites -
---------------------------------

This document will provide an introduction to creating custom SAMMI (SEF) extensions.  Creating new extension files requires knowledge of JavaScript programming, and a strong understanding of SAMMI variable types and commands.  Manual receiver protocol usage and executing hooks from receiver requests are outside of the scope of this introductory documentation.

All SAMMI extensions are Microsoft Windows format text files saved with an .sef file extension.  It is highly recommended to review other extensions to get a better idea on the different sections of the extension file and how they work.  You can also copy and modify the basic extension example or use the empty template content from section 2 below into a new .sef file to get started.

For questions or issues creating SEF extensions, visit the official SAMMI Discord server (https://discord.gg/dXez8Zh) and post in the Extension section #development channel.  Please remember that there are a limited number of users on the Discord server that can assist with extension development and that they are all volunteers.

------------------------------
- 2. Extension Template File -
------------------------------

See the \bridge\template.sef file under the main SAMMI folder for an empty extension template.

(To-do: Create a basic extension example here)

------------------------------
- 3. Extension File Sections -
------------------------------

[extension_name]

This section contains the name of the extension and is what will be displayed to users as the extension name in the transmitter and receiver.  Alphanumeric characters and spaces are supported.

[extension_info]

You can add any text content here or leave it empty, it is not used by the transmitter or receiver.  Version and author name information is good information to include in this section.

[extension_version]

Add your current extension version here. Should only contain numbers and dots. For example 2.01. This will be later used in an automatic version checker where you will be able to submit your PRs to our public repo whenever you release a new version of your extension.

[insert_external]

The content in this section supports HTML format text content and will display on the extension's tab in the transmitter.  This section may be left empty if desired.

[insert_command]

Defines the command or set of commands for the button editor in the SAMMI Core application.  Use the SAMMI.extCommand helper function outlined in the transmitter documentation to create a new command:

https://github.com/SAMMISolutions/SAMMI-Bridge#helper-functions

An extension can add more than one SAMMI.extCommand block to create multiple button commands in the receiver.  Each SAMMI.extCommand block sets the name of a new extension command in the receiver, the command's color, height, and a JavaScript object defining the set of fields/boxes to show in the receiver UI for the command.

[insert_hook]

This section bridges the command name(s) and data from the receiver and the JavaScript function(s) and parameters to execute.  This section must include a JavaScript case statement, or hook, for each SAMMI.extCommand block defined in the [insert_command] section.

Case matching values (aka hook names) must match the button command names from the [insert_command] section exactly, including case sensitivity and spaces.  The case statement code block should contain the JavaScript function to call defined in the [insert_script] section of the extension.  All function parameters used must include the object prefix of "SAMMIJSON." (Without the quotes) and parameter names that align with boxVariable values in the order defined within the SAMMI.extCommand blocks of the [insert_command] section.

[insert_script]

The main extension behavior code goes into this section via standard JavaScript function definitions.  Function and property names must comply with JavaScript naming conventions.  The parameter order must match the order defined in the matching [insert_hook] case statement.  It is not required, although strognly recommended, that the function parameter names align with the names used in the [insert_hook] and [insert_command] sections for clarity.  

Extension code can use the SAMMI websocket library to send and receive data to the receiver.  It is highly recommended to use the helper functions from the transmitter documentation to perform these actions:

https://github.com/SAMMISolutions/SAMMI-Bridge#helper-functions

[insert_over]

This section allows the extension to install a new deck into the SAMMI Core.  Developers can create and save the deck content in the receiver UI, right click the deck, select "Export JSON", and paste the JSON text content into this section. SAMMI users installing the extension will receive a prompt to install the deck content as defined in this section.

The installed decks can use commands created in the same extension, or any other extension.  However, if the user uninstalls an extension used by the deck defined in this section, the related commands will not work in the receiver.  This may cause unexpected behavior or cause the receiver to crash.

Add these keys to your exported deck json if you want SAMMI to perform additional checks when user tries to install the extension: 

"sammi_version":"2.00.0"	Check if SAMMI version is working fine
"bridge":true		Check if the Bridge is connected
"obswebsocket":"4.9.1"		Check if OBS Main is connect and correct version
"donot_include_deck":false	Check if the deck should be create, if the deck does not exists it doesnt matter, this is if you want an optionnal deck or hidden deck
"extension_triggers":["TRG1","TRG",...]		These are all the Extension triggers that should happen, trigger pull data will include "path" for the path of where the extension was.
"required_extension":["Extension name","Another extension name",...] Check if all required extensions are installed before installing the extension

---------------------------------
- 4. Troubleshooting Extensions -
---------------------------------

Extension files install into the main transmitter HTML document.  It is important to note that syntax errors or JavaScript code issues will not prevent an extension from installing, although they may cause the transmitter or receiver to act strangely or not work at all.  During extension development and testing, it is highly recommended to close out any transmitter docks in OBS Studio and open the transmitter HTML file directly in a local browser window outisde of OBS until testing is complete.

From the browser window, errors from extensions will output to the browser developer console, usually accessed by pushing F12 in the browser window and selecting the "Console" tab of the developer tools.  Extensions support output to console.log within the [insert_script] and [insert_hook] code for testing or troubleshooting purposes and also display in the same browser console.

If code changes to the installed extension are required, you can re-upload corrected extension file as long as the extension name does not change; the receiver will prompt to replace the existing extension content.  Normally the transmitter will automatically restart after installing an extension via the receiver.  However, errors may prevent the automatic transmitter restart.  If this is the case, manually reload the transmitter by either refreshing the browser window or closing and reopening the OBS Studio transmitter dock for the new extension code to take effect.
