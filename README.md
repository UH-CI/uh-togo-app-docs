# UH Agave ToGo Documentation

## Creating a Storage System

Click on 'Systems' in the sidebar on the left.  You should see something like this:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/ExistingSystems.jpg" alt="Systems Main View" title="Systems Main View">

On the resulting page, click "New System" and this comes up:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/SystemsNew1.jpg" alt="Systems Builder Step 1" title="Systems Builder Step 1">

This is the start of a 3 step wizard that takes you through all the fields required to create a system.  Notice at the top right corner of the wizard area, there are 3 buttons: Form, code, and split.  As you go through the wizard and provide values, it generates JSON code that gets submitted via the Agave API to set everything up.  If you have existing JSON, you can just select the code button, paste the JSON, and submit it.  For the purposes of this documentation, we're going to use the form.  Make sure the split button is selected so you can see both the form and the JSON that gets created as you progress.  

On the form, the drop down box has 2 items: Storage and Execution.  Select "Storage."  Next to each form entry there is a little question mark which you can click on to get more information about what the field is for.  Unfortunately, t the time of writing this documentation, the aid for this particular field is incorrect as it seems to think this is the ID field which comes later.

After selecting the storage option and clicking next, you get:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/SystemsNewStorage2.jpg" alt="Systems Builder Storage Step 2" title="Systems Builder Storage Step 2">

There are five fields here, but only 3 are required: id, name, and status.  The ID is a unique identifier that will be used throughout the system.  Later, when you go to create apps and have to select an existing storage system, the list to choose from will show this identifier, so make it something you can understand.

The "Name" field is a way to include a more human readable version of the ID.  It appears in the overview as illustrated in the first systems image above, but outside of that, it doesn't seem to be used.

The last required field, status, should just be set to "up" assuming the system you are connecting to is available.  The other options are "down", "maintenance", and "unknown".  It the status is not set to "up", jobs tied to that system will not be able to run.  This is a feature in that if you know a system is down for whatever reason, you can come back and change the status and any related scheduled jobs won't attempt to start.  

"Description" allows you to include a more elaborate explanation of the system. It appears in the overview as illustrated in the first systems image above, but it doesn't seem to be used outside of the main systems display page.

The "Site" field is something like "hawaii.edu/its/ci." It's primary purpose is to group together systems within the same group.  It really isn't used for anything so don't sweat it.

For this demo, I'm only filling in required field.  I've entered "a-test-storage-system" as the id, "A test storage system" as the name, and gave it a status of "up."  After clicking "Next," here's what you see:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/SystemsNewStorage3.jpg" alt="Systems Builder Storage Step 3" title="Systems Builder Storage Step 3">

All the fields on this page are required.

Protocol: the options are: FTP, SFTP, GridFTP, Irods, Local, and S3.  I selected SFTP.

Host: the hostname or ip address of the storage server.  Example: uhhpc1.its.hawaii.edu

System Auth Server Port: Your storage server's port number.  I entered '22' for my server.

Root directory: The path on the remote system to use as the root directory for all API requests.  Just put '/'.

Home directory: The help button says this "The path on the remote system, relative to rootDir to use as the virtual home directory for all API requests. This will be the base of any requested paths that do not being with a /. Defaults to /, thus being equivalent to rootDir."  For the UH HPC system, I entered '/home/jgeis'.

Storage Authentication, Type: There are Anonymous, APIKeys, Local, Pam, Password, SSHKeys, X509.  I entered password which caused the form to display username and password fields into which I entered my UH username and password.

After filling in all the fields and clicking submit, this should show up:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/SystemsNewStorageSuccess.jpg" alt="Systems Builder Storage Success" title="Systems Builder Storage Success">

If you click the systems item in the left-hand menu to bring up the main systems page, your new system will be listed.

Here is the final JSON with my password removed.

    {
      "site": null,
      "id": "a-test-storage-system",
      "default": false,
      "status": "UP",
      "description": null,
      "name": "A Test Storage System",
      "owner": "jgeis",
      "globalDefault": false,
      "available": true,
      "public": false,
      "type": "STORAGE",
      "storage": {
        "mirror": false,
        "port": 22,
        "homeDir": "/home/jgeis",
        "protocol": "SFTP",
        "host": "uhhpc1.its.hawaii.edu",
        "publicAppsDir": null,
        "proxy": null,
        "rootDir": "/",
        "auth": {
          "type": "PASSWORD",
          "password": "PASSWORD"
        },
        "proxyTunnel": "NO"
      }
    }

