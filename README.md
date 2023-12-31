<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1 align = "center">osTicket - Prerequisites and Installation</h1>
osTicket is an open source support ticketing system. This tutorial will outline the prerequisites and the installation steps needed for installation!<br />

<h2>Environments and Technologies Used</h2>

<ul>
  <li>Microsoft Azure (Virtual Machines/Networks)</li>
  <li>Remote Desktop Connections</li>
  <li>Internet Information Services (IIS)</li>
</ul>

</br>

<h2>Operating Systems Used </h2>
<ul>
  <li>Windows 10 (21H2)</li>
</ul>

</br>

<h2>List of Prerequisites</h2>
<ol>
  <li>Set up an Azure Virtual Machine (Windows 10 4 vCPUs Recommended, guide <a href ="https://github.com/joshuafinchCC/VM-VN-RDC">here</a>)</li>
  <li><a href = "https://drive.google.com/drive/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6">osTicket Installation Files</a> (Download these files on your Azure Virtual Machine) </li>
  <li>Enable IIS in I.S.S.</li>
  <li>Install Web Platform Installer</li>
  <li>Install MySQL and set up username and password</li>
    <ul>
    <li>For this tutorial, we will set up our username and password as:</li>
      <ul>
      <li>username: root</li>
      <li>password: Password1</li>
      </ul>
    </ul>
  <li>Install C++ Redistributable</li>
  <li>Configure permissions and install osTicket</li>
  <li>(OPTIONAL) Notepad for login information</li>
</ol>

<h2>Installation Steps</h2>

<h3>Install / Enable IIS in Windows WITH CGI and Common HTTP Features</h3>

<p>
  <ul>
    <li>In your VM, go to the start menu and search <b>Control Panel</b>. Select <b>Programs</b> -> <b>Programs and Features</b>. </li>
    <li>Under <b>Program and Features</b> click on <b>Turn Windows features on or off</b></li>
    <li>Scroll down the list and check the box for <b>Internet Information Services</b></li>
    <li>Expand the list for <b>Internet Information Services</b>, navigate to <b>World Wide Web Services</b> then expand that to find <b>Application Development Features</b>, and check the box for <b>CGI</b>.</li>
    <li>Before selecting OK, make sure the boxes under <b>Common HTTP Features</b> in World Wide Web Services are checked.</li>
     
   <p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/179de16a-ff86-413e-b38c-b9aed3bd4024" height="80%" width="80%"/>
   </p>
    
  <ul>
    <li>To confirm all your settings are correct, go to your browser in your VM and type in <b>127.0.0.1</b>, it should load the page to Internet Information Services. This is basically a loopback address, running a page off of yourself</li>
      <ul>
<p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/2e08c27f-449c-432a-8c82-b9286fbcba08" height="80%" width="60%" />
   </p>

<br />

<h3>Installing Files for osTicket</h3>

<p>
  <ul>
    <li><b>NOTE:</b> <i> Your download speeds will vary depending on the VM's CPU and Google Drive's virus scanning speed </i></li>
    <li>From the Installation Files, download <b>PHP Manager</b> (PHPManagerForIIS_V1.5.0.msi) and <b>Rewrite Module</b> (rewrite_amd64_en-US.msi). Install both </li>

<p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/e587309d-cddd-488c-89ab-8daf8a03e88d" height="80%" width="80%" />
   </p>
    
   <li>Create a Folder in your VM's C Drive and name it <b>PHP</b></li>
      <ul>

<p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/192612f8-01fd-4e1a-8939-cb1abfba3755" height="80%" width="60%" />
   </p>
       
  </ul>
    <li>From the Installation Files, download the zip file <b>PHP 7.3.8</b> (php-7.3.8-nts-Win32-VC15-x86.zip) and extract the contents into the newly created PHP folder (C:\ PHP)</li>
      <ul>

<p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/f0ee0ae6-9b99-4810-a9d5-297ebc8f4a11" height="80%" width="80%" />
   </p>
     
  </ul>
    <li>From the Installation Files, download and install <b>VC_redist.x86.exe</b></li>
    <li>From the Installation Files, download and install <b>MySQL 5.5.62</b> (mysql-5.5.62-win32.msi)</li>
      <ul>
       <li>After installing, launch the <b>Configuration Wizard</b></li>
        <li>Check <b>Install As Window Service</b>, for this tutorial our Service Name will stay as <b>MySQL</b></li>
        <li>Check <b>Modify Security Settings</b> and for this tutorial we'll set the password as <b>Password1</b> and then execute to finish installation</li>

<p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/6f736192-60e8-4ca8-aacd-7df848b89c55" height="60%" width="40%" />
   </p>
     
  </ul>
</p>

<br />

<h3>Setting up IIS and PHP</h3>

<p>
  <ul>
    <li> In your start menu search <b>Internet Information Services (IIS) Manager</b> and run it as Administrator</li>
    <ul>
      <li> You should see <b>PHP Manager</b> and <b>URL Rewrite</b> in your IIS Manager due to the PHP Manager and Rewrite Modules files we just downloaded </li>
<p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/dce39db3-ddba-4b58-a340-a0d9700130e8" height="80%" width="80%" />
   </p>
      </ul>
    <li>Go to <b>PHP Manager</b> and click on <b>Register new PHP Version</b>, set the directory to the <b>php-cgi</b> file found in the PHP folder we've set in C Drive (C:\PHP)</li>
    <ul>

<p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/37b33164-dd38-4e35-a489-25198a448d1b" height="80%" width="80%" />
   </p>
      </ul>
    <li>Optional but Recommened: Refresh the IIS Manager Server by going to <b>Actions</b> and under <b>Manage Server</b> click on <b>Restart</b></li>
  </ul>
</p>

<br />

<h3>Installing osTicket</h3>

<p>
  <ul>
    <li>From the Installation Files, download and install <b>osTicket v1.15.8.zip</b></li>
    <li>Extract the <b>upload</b> folder from the zip file and copy the folder into the directory <b>C:\inetpub\wwwroot</b> in your VM. Afterwards, rename it to <b>osTicket</b> and refresh the IIS manager</li>
      <ul>
      <p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/c331e4aa-7997-4697-b8bc-54cba0d39a64" height="80%" width="80%" />
   </p>
      </ul>
    <li>In IIS Manager, click the <b>Sites</b> dropdown, then expand <b>Default Web Site</b> and select the <b>osTicket</b> folder. Then, on the right, navigate to <b>Browse Folder</b> and click on <b>Browser*.80 (http)</b></li>

  <p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/e38fee10-0636-4d82-8b9a-2156f52d9850" height="80%" width="80%" />
   </p>
    
  <li>The page for osTicket Installer should now pop up. If not, check your directories of your files and folders</li>
      <ul>
        <p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/71b6538e-f921-4e51-8b1d-9076d6627184" height="80%" width="80%" />
   </p>
      </ul>
    
    
  <li>In IIS Manager, go to <b>osTicket</b> and click on <b>PHP Manager</b> -> <b>Enable or disable extensions</b> and enable the following extensions</li>
      <ul>
        <li>php_imap.dll</li>
        <li>php_intl.dll</li>
        <li>php_opcache.dll</li>
      </ul>
<p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/b21a5b81-651d-4f9a-b318-d04b17a06837" height="80%" width="80%" />
   </p>
      
   <li>Refresh osTicket Installer on your browser to see <b>PHP IMAP Extension</b> and <b>Intl Extensions</b> are checked signifying the extensions are installed</li>
   
  <p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/89675ac1-00b4-45df-859e-d00ed1524fae" height="60%" width="40%" />
   </p>
    
   <li>Locate the php file <b>ost-sampleconfig.php</b> inside the directory <b>C:\inetpub\wwwroot\osTicket\include\</b> and rename it to <b>ost-config.php</b> because osTicket Installer needs to interact with this file</li>
    <li>Now go to the <b>Properties</b> of the ost-config file and go to the <b>Advanced</b> settings in <b>Security</b> and <b>Disable Inheritance</b> to remove all inheritance permissions from the file (essentially making a "clean" object)</li>

  <p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/310c6a82-27c5-4605-a941-597c060036cb" height="60%" width="40%" />
   </p>
   
  <li>Now add a new Permission, then click on <b>Select a principal</b> and for a new object type "everyone" the click on <b>Check Names</b> to set the Group and click OK. Then check all the boxes on Basic Permissions and then click OK. Now everyone using osTicket should have full permission to use it</li>

<p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/afec45b5-c976-4053-8a5c-d8167e3c8d2f" height="60%" width="40%" />
   </p>
  
   <li>Head to osTicket on your browser and click on <b>Continue</b> then set your <b>System Settings</b> and <b>Admin User</b> until you get to <b>Database Settings</b></li>
      <ul>
        <li>Your email and usernames can be whatever you want (i.e "yourname@helper.com"), it is recommended to have a notepad to keep your usernames and passwords ready</li>
      </ul>
    <li>From the Installation Files, download and install <b>HeidiSQL</b></li>

  <ul>
        <li>Go through basic setup then launch HeidiSQL and create a New Session using the username "root" and password "Password1"</li>
       <p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/49f01967-4f35-41ea-9559-211ea2bdcf4e" height="60%" width="40%" />
   </p>
        <li>You should see this once connected</li>
        <p align="center">
        <img src="https://github.com/joshuafinchCC/osticket-prereqs/assets/155266044/a9280c2f-4ae4-4189-9907-13b58abf50fa" height="80%" width="80%" />
   </p>
        <li>Create a Database and name it <b>osTicket</b></li>
      </ul>
    <li>Once connected, go back to osTicket Installer type in our username and password into the respected fields in Database Settings</li>
      <ul>
        <li>MySQL Database: osTicket</li>
        <li>MySQL Username: root</li> 
        <li>MySQL Password: Password1</li>
      </ul>
    <li>Click <b>Install Now</b>, osTicket should now be fully installed on your VM!</li>
    <ul>
      <li><img src="https://github.com/ColtonTrauCC/osticket-prereqs/assets/147654000/f48259ba-ba8a-4bce-9cbe-a300903de8b2" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
      <li><a href = "http://localhost/osTicket/scp/login.php">Link to Help Desk Page</a></li>
      <li><a href = "http://localhost/osTicket/">Link to End Users Page</a></li>
    </ul>
  </ul>
</p>

<br />

<h3>Clean Up</h3>

<p>
  <ul>
    <li>Delete the <b>setup</b> folder inside your osTicket folder inside wwwroot (C:\inetpub\wwwroot\osTicket\setup)</li>
    <li>Set the permissions of <b>ost-config.php</b> to "read only" (have only the Read and Read and Execute boxes checked)</li>
  </ul>
</p>



  <p align="center">
        <img src="" height="80%" width="80%" />
   </p>

<br />

<h3 align = "right">Next Tutorial - <a href="https://github.com/ColtonTrauCC/post-install-config">osTicket - Post-Install Configuration</a></h3>
