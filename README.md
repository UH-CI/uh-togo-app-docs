# UH Agave ToGo Documentation

## Logging in UH AgaveToGo

Bring up https://ikewai.its.hawaii.edu/app/ (pre-release, use https://ikewai-dev.its.hawaii.edu/app/) in your browser.  You will see a screen like this:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/Login1.jpg" alt="Login Page 1" title="Login Page 1">

Click on the drop-down field and a list of organizations may appear.  

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/Login2.jpg" alt="Login Page 1, step 2" title="Login Page 1, step 2">

For now, the list is limited to the University of Hawaii, so select the item labeled "Hawaii Development Tenant". 

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/Login3.jpg" alt="Login Page 1, step 3" title="Login Page 1, step 3">

Click the "Login" button and you will see something like:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/Login4.jpg" alt="Login Page 2" title="Login Page 2">

It's possible the logo that appear may be different as we're planning on changing it.  Click on the UH logo and that will bring you to:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/Login5.jpg" alt="Login Page 3" title="Login Page 3">

Enter your UH username and password and click the 'sign in' button.  After a successful login, you will see:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/Login6.jpg" alt="Login Page 5" title="Login Page 5">

This will show that your login is good for one hour.  Right below that, there's a link that says "Go to your Dashboard."  Click on that and it will take you to the main page of the AgaveToGo app.

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/Dashboard.jpg" alt="Dashboard" title="Dashboard">


## Creating a Storage System

Click on 'Systems' in the sidebar on the left.  You should see something like this:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/ExistingSystems.jpg" alt="Systems Main View" title="Systems Main View">

On the resulting page, click "New System" and this comes up:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/SystemsNew1.jpg" alt="Systems Builder Step 1" title="Systems Builder Step 1">

This is the start of a 3 step wizard that takes you through all the fields required to create a system.  At the top of the form, there's a drop down menu where you can select an existing system to use a template. If you have existing systems that are similar to the one you want to create, this is probably the way to go.

Also at the top right corner of the wizard area, there are 3 buttons: Form, code, and split.  As you go through the wizard and provide values, it generates JSON code that gets submitted via the Agave API to set everything up.  If you have existing JSON, you can just select the code button, paste the JSON, and submit it.  For the purposes of this documentation, we're going to use the form wizard.  Make sure the split button is selected so you can see both the form and the JSON that gets created as you progress.  

On the form, the drop down box has 2 items: Storage and Execution.  Select "Storage."  Next to each form entry there is a little question mark which you can click on to get more information about what the field is for.  Unfortunately, at the time of writing this documentation, the aid for this particular field is incorrect as it seems to think this is the ID field which comes later.

After selecting the storage option and clicking next, you get:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/SystemsNewStorage2.jpg" alt="Systems Builder Storage Step 2" title="Systems Builder Storage Step 2">

There are five fields here, but only 3 are required: id, name, and status.  For many of the fields covered in this document, I'll be including the text from the help button next to the field in the app as it seemed to be the most succinct explanation.

* ID:  a unique identifier that will be used throughout the system.  This has to be unique across all systems in the tenant, meaning if another user created a system with a given ID, you will not be able to use that ID for your system.  Even if you delete a system, the ID still cannot be reused.  After you create your system, when you go to create apps and have to select an existing storage system, the list to choose from will show this identifier, so make it something you can understand.  An example of a good ID would be jgeis.sftpstorage.uhhpc.its.hawaii.edu

* Name: a more human readable version of the ID.  It appears in the overview as illustrated in the first systems image above, but outside of that, it doesn't seem to be used.

* Status: this is the current status of the system you are connecting to.  You likely will just set this to "up" assuming the system you are connecting to is available.  The other options are "down", "maintenance", and "unknown".  It the status is not set to "up", jobs tied to that system will not be able to run.  This is a feature in that if you know a system is down for whatever reason, you can come back and change the status and any related scheduled jobs won't attempt to start.  

The non-required fields are:

* Description: a more elaborate explanation of the system. It appears in the overview as illustrated in the first systems image above, but it doesn't seem to be used outside of the main systems display page.

* Site: something like "hawaii.edu/its/ci." It's primary purpose is for grouping.  It really isn't used for anything so don't sweat it.

For this demo, I'm only filling in required fields.  I've entered "a-test-storage-system" as the id, "A test storage system" as the name, and gave it a status of "up."  After clicking "Next," here's what you see:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/SystemsNewStorage3.jpg" alt="Systems Builder Storage Step 3" title="Systems Builder Storage Step 3">

All the fields on this page are required.

* Protocol: the options are: FTP, SFTP, GridFTP, Irods, Local, and S3.  I selected SFTP.

* Host: the hostname or ip address of the storage server.  Example: uhhpc1.its.hawaii.edu

* System Auth Server Port: Your storage server's port number.  I entered '22' for my server.

* Root directory: The path on the remote system to use as the root directory for all API requests.  Just put '/'.

* Home directory: The help button says this "The path on the remote system, relative to rootDir to use as the virtual home directory for all API requests. This will be the base of any requested paths that do not being with a /. Defaults to /, thus being equivalent to rootDir."  For the UH HPC system, I entered '/home/jgeis'.

* Storage Authentication, Type: There are Anonymous, APIKeys, Local, Pam, Password, SSHKeys, X509.  I entered password which caused the form to display username and password fields into which I entered my UH username and password.

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


## Creating an Execution System

Click on 'Systems' in the sidebar on the left.  You should see something like this:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/ExistingSystems.jpg" alt="Systems Main View" title="Systems Main View">

On the resulting page, click "New System" and this comes up:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/SystemsNew1.jpg" alt="Systems Builder Step 1" title="Systems Builder Step 1">

This is the start of a 3 step wizard that takes you through all the fields required to create a system.  At the top of the form, there's a drop down menu where you can select an existing system to use a template. If you have existing systems that are similar to the one you want to create, this is probably the way to go.

In the top right corner of the wizard area, there are 3 buttons: form, code, and split.  As you go through the wizard and provide values, it generates JSON code that gets submitted via the Agave API to set everything up.  If you have existing JSON, you can just select the code button, paste the JSON, and submit it.  For the purposes of this documentation, we're going to use the form wizard.  Make sure the split button is selected so you can see both the form and the JSON that gets created as you progress.  

On the form, the drop down box has 2 items: Storage and Execution.  Select "Execution."  Next to each form entry there is a little question mark which you can click on to get more information about what the field is for.  Unfortunately, at the time of writing this documentation, the aid for this particular field is incorrect as it seems to think this is the ID field which comes later.

After selecting the execution option and clicking next, you get:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/SystemsNewExecution2.jpg" alt="Systems Builder Execution Step 2" title="Systems Builder Execution Step 2">

At this point, you'll see a form with a lot of fields, only ID, Name, Execution Type, and Scheduler require responses.  There are other required fields, but they are pre-populated with likely default values.  For many of the fields covered in this document, I'll be including the text from the help button next to the field in the app as it seemed to be the most succinct explanation.

* ID (required): a unique identifier that will be used throughout the system.  This has to be unique across all systems in the tenant, meaning if another user created a system with a given ID, you will not be able to use that ID for your system.  Even if you delete a system, the ID still cannot be reused.  After you create your system, when you go to create apps and have to select an existing storage system, the list to choose from will show this identifier, so make it something you can understand.  An example of a good ID would be jgeis.execute.uhhpc.its.hawaii.edu

* Name (required): more human readable version of the ID.  It appears in the overview as illustrated in the first systems image above, but outside of that, it doesn't seem to be used.

* Status: this is the current status of the system you are connecting to.  You likely will just set this to "up" assuming the system you are connecting to is available.  The other options are "down", "maintenance", and "unknown".  It the status is not set to "up", jobs tied to that system will not be able to run.  This is a feature in that if you know a system is down for whatever reason, you can come back and change the status and any related scheduled jobs won't attempt to start. 

* Description: a more elaborate explanation of the system. It appears in the overview as illustrated in the first systems image above, but it doesn't seem to be used outside of the main systems display page.

* Site: something like "hawaii.edu/its/ci." It's primary purpose is for grouping.  It really isn't used for anything so don't sweat it.

* Execution Type (required):  The help button gives you this "Specifies how jobs should go into the system. HPC and Condor will leverage a batch scheduler. CLI will fork processes."  For this demo, I entered HPC.  After selecting an execution type, a drop-down box labeled "Scheduler" appears right below this field.  It appears regardless of which option you select, but it is populated differently depending on your selection.

* Scheduler (required):  The type of batch scheduler for the given execution type. This field doesn't appear until you select and execution type and its values differ depending on which execution type you selected. For CLI and Condor, there is only one option for each, but for HPC your options are LSF, Loadleveler, psb, sge, cobalt, torque, moab, and slurm.  For this demo, I chose slurm.

* Maximum System Jobs: The help button displays "Maximum number of jobs that can be queued or running on a system across all queues at a given time. Defaults to unlimited." While it says the default is unlimited, the field is actually pre-populated with 50.

* Maximum Jobs Per User: the help button displays "Maximum number of jobs that can be queued or running on a system for an individual user across all queues at a given time. Defaults to unlimited".  While it says the default is unlimited, the field is actually pre-populated with 5.

* Scratch Directory: Path to use for a working scratch directory, if you are using the UH HPC system, enter /lus/scratch/your-username/  Note that help button has the wrong information for this item and doesn't apply here.

* Work Directory: The help button shows "Path to use for a job working directory. This value will be used if no scratchDir is given. The path will be resolved relative to the rootDir value in the storage config if it begins with a /, and relative to the system homeDir otherwise." For the UH HPC system, enter /home/your-username

* Environment: The help button shows "List of key-value pairs that will be added to the environment prior to execution of any command."

* Startup Script: The help button shows "Path to a script that will be run prior to execution of any command on this system. The path will be resolved relative to the rootDir value in the storage config if it begins with a "/", and relative to the system homeDir otherwise. Any environment variables defined in the system description will be set before this script is called. If this script fails, the job will fail."  Actually, it doesn't show all of that, it's getting truncated.  We'll get around to fixing it, but for now, the above is the full text.  You likely want to point this to something like ./bashrc

* Queues: The help button shows "An array of batch queue definitions providing descriptive and quota information about the queues you want to expose on your system. If not specified, no other system queues will be available to jobs submitted using this system." Paraphrasing from <http://slurm.schedmd.com/quickstart.html>, A queue can be thought of as a group of nodes/resources which has an assortment of constraints such as job size limit, job time limit, users permitted to use it, etc. Priority-ordered jobs are allocated nodes until the resources (nodes, processors, memory, etc.) within that queue are exhausted.  The UH HPC has seven different queues: community.q, exclusive.q, lm.q, gpu.q, sb.q, kill.q, and htc.q.  Jobs submitted to kill.q and htc.q can be preempted by jobs in other partitions.  You can see the details/restrictions on these queues by going to [the Cyberinfrastructure site](http://www.hawaii.edu/its/ci/hpc-resources/slurm-partitions/).  Use the values you find there to fill out the following fields.  If you are using resources from elsewhere and don't have the necessary information, try to use the defaults provided.
  * Name: Arbitrary name for the queue. This will be used in the job submission process, so it should line up with the name of an actual queue on the execution system.  This has no default value, for this example using the UH HPC, enter "community.q"
  * Maximum Jobs: Maximum number of jobs that can be queued or running within this queue at a given time. Defaults to 10. -1 for no limit.
  * Maximum Nodes: Maximum number of nodes that can be requested for any job in this queue. -1 for no limit.  Default is 128.
  * Maximum Memory Per Node: Maximum memory per node for jobs submitted to this queue in ###.#[E|P|T|G]B format.  Default is 1024GB.
  * Maximum Processors Per Node: Maximum number of processors per node that can be requested for any job in this queue. -1 for no limit.  Default is -1.
  * Maximum Requested Time: Maximum run time for any job in this queue given in hh:mm:ss format.  Default is 24:00:00.
  * Custom Directives: Arbitrary text that will be appended to the end of the scheduler directives in a batch submit script. This could include a project number, system-specific directives, etc. 
  * Default: True if this is the default queue for the system, false otherwise.
  
After entering all this, click next and see a screen similar to this:

<img src="https://github.com/UH-CI/uh-togo-app-docs/blob/master/images/SystemsNewExecution3.jpg" alt="Systems Builder Execution Step 3" title="Systems Builder Execution Step 3">

There are five required fields (login host, protocol, storage host and port, and authentication type) and 10 fields total:

* Login Host (required): The hostname or ip address of the server where the job will be submitted.  For the UH HPC, use uhhpc1.its.hawaii.edu
* System Auth Server Port: The port number of the server where the job will be submitted. Defaults to the default port of the protocol used.  
* Protocol (required):  The protocol used to submit jobs for execution: SSH, GSISSH, and Local.  For this example, using the UH HPC, enter SSH.  This has 2 side affects 1.) auto-fill in the port number to 22 and 2.) causes another field 'proxyTunnel' to appear.  For this, leave it to the default of 'NO.'
* Storage Protocol: The protocol used to authenticate to the storage server.  The options are FTP, SFTP, GridFTP, IRods, Local, and S3.  For the UH HPC example, use SFTP.
* Storage Host (required): The hostname or ip address of the storage server.  This is where you have your data.  For the UH HPC, enter uhhpc1.its.hawaii.edu
* Storage System Auth Server Port (required):  The port number of the storage server.  For the UH HPC example, enter 22.
* Storage Root Directory:  The path on the remote system to use as the virtual root directory for all API requests. Defaults to '/'.  For this example, leave it as the default.
* Storage Home Directory: The path on the remote system, relative to rootDir to use as the virtual home directory for all API requests. This will be the base of any requested paths that do not being with a /. Defaults to /, thus being equivalent to rootDir.  For the UH HPC example. enter /home/your-username
* Proxy Tunnel: configuration attributes give information about how to connect to a remote system through a proxy server. This often happens when the target system is behind a firewall or resides on a NAT. Currently proxy servers can only reuse the authentication configuration provided by the target system.  For this example, leave it at the default of "No."
* Storage Authentication Type: In this case, the help button is showing the wrong information.  The options are Anonymous, APIKeys, Local, Pam, Password, SSHKeys, X509.  I entered password and filled in the username and password fields with my UH username and password.



