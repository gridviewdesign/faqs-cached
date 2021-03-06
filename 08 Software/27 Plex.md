<h1>Plex</h1>

        
<strong>Important note:</strong>&nbsp; You can open a support ticket for help setting up Plex.<br>
<strong>Currently available Plex version: </strong> 1.1.3<br>
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: <a href="https://www.feralhosting.com/faq/view?question=12">SSH Guide - The Basics</a><br>
<br>
Your FTP &#x2F; SFTP &#x2F; SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:<br>
<br>
<img src="https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png"><br>
<br>
You login information for the relevant slot will be shown here:<br>
<br>
<img src="https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png"><br>
<br>
<h2>Plex.tv account:</h2><br>
If you have not already created an account with <a href="https://plex.tv/">plex.tv</a> please do so now.<br>
<br>
<a href="https://plex.tv/users/sign_in">https:&#x2F;&#x2F;plex.tv&#x2F;users&#x2F;sign_in</a><br>
<br>
<br>
<h2>Automated Installation script:</h2><br>
We are current testing a new automated installation script for Plex. It no longer requires you port forward over SSH to get Plex working. You will still need to SSH into your slot in order to run the script, but it&#x27;s just a copy and paste after that.&nbsp; <br>
To use the script just use this command:<pre><code>wget -qO ~&#x2F;install.plex.sh <a href="https://git.io/vKbgP">https:&#x2F;&#x2F;git.io&#x2F;vKbgP</a> &amp;&amp; bash ~&#x2F;install.plex.sh</code></pre><br>
<strong>Important note:</strong> Once you have run this script, log into the Plex instance at the URL given. Be sure to go to Setting &gt; Remote Access &gt; Advanced and recheck the manual port mapping button.<br>
<h2>Manual Plex Installation and Set Up Outlined</h2><br>
To install Plex this is the procedure you will need follow. All these steps are described in this guide.<br>
<br>
<strong>1:</strong> Create a directory named <code>plex</code> inside your <code>private</code> directory that is located in your slot&#x27;s root directory.<br>
<strong>2:</strong> Activate the the port forward using the commands described below.<br>
<strong>3:</strong> Create an SSH tunnel on the relevant slot to connect to the Local Plex URL.<br>
<strong>4:</strong> Once connected to Plex you must then connect the server to your plex.tv account.<br>
<strong>5:</strong> Then active remote connection by manually specifying the port that was used for the port forward.<br>
<strong>6:</strong> Disable the SSH proxy in your web browser and then connect to the remote Plex URL.<br>
<br>
Once done Plex should be fully functional. To achieve this please continue reading the guide.<br>
<br>
<h2>Manual Plex Installation</h2><br>
 <strong>Important note:</strong> After the <code>~&#x2F;private&#x2F;plex</code> directory is created Plex will then be installed and set up automatically within the next 5 minutes.<br>
<br>
Run these SSH commands using an SSH client:<br>
<br>
<pre><code>mkdir -p ~&#x2F;private&#x2F;plex
mkdir -p ~&#x2F;.config&#x2F;feral&#x2F;ns&#x2F;forwarding&#x2F;tcp &amp;&amp; rm -f ~&#x2F;.config&#x2F;feral&#x2F;ns&#x2F;forwarding&#x2F;tcp&#x2F;*
echo 32400 &gt; ~&#x2F;.config&#x2F;feral&#x2F;ns&#x2F;forwarding&#x2F;tcp&#x2F;&quot;$(shuf -i 10001-32001 -n 1)&quot;</code></pre><br>
Then run this command to automatically load the <code>README</code> when it is created by the installation. It can take up to five minutes:<br>
<br>
<pre><code>while [ ! -f ~&#x2F;private&#x2F;plex&#x2F;README ]; do printf &#x27;\rWaiting...&#x27;; sleep 2; done &amp;&amp; cat ~&#x2F;private&#x2F;plex&#x2F;README</code></pre><br>
 <strong>Important note:</strong> If you have port issues later in the guide you can just run these two commands again. The system will sweep every five minutes and create the port forwarding, so please wait till it does this. Please note that it will also remove any incorrect files from the tcp directory <em>including files trying to forward a port which is already in use. If 5 minutes later your file is missing this is likely to be why.</em><br>
<br>
<pre><code>mkdir -p ~&#x2F;.config&#x2F;feral&#x2F;ns&#x2F;forwarding&#x2F;tcp &amp;&amp; rm -f ~&#x2F;.config&#x2F;feral&#x2F;ns&#x2F;forwarding&#x2F;tcp&#x2F;*
echo 32400 &gt; ~&#x2F;.config&#x2F;feral&#x2F;ns&#x2F;forwarding&#x2F;tcp&#x2F;&quot;$(shuf -i 10001-32001 -n 1)&quot;</code></pre><br>
<h2>Plex Post installation check-list:</h2><br>
 <strong>Important note:</strong> Once Plex has been installed and running it will be limited to local connections only. In order to successfully connect to the local Plex URL you must have done these things:<br>
<br>
<strong>1:</strong> Plex was installed and the <code>README</code> was successfully loaded.<br>
<br>
<strong>2:</strong> You activated the port forward using the commands listed in the previous section.<br>
<br>
 <strong>Important note:</strong> You will need to create an SSH tunnel connect and then configure your web browser to use it in order to connect to the Plex server. <strong>OpenVPN will not work.</strong> Please follow these steps below to create the SSH tunnel and complete the plex setup:<br>
<br>
<strong>3:</strong> You have created the SSH tunnel: <a href="https://www.feralhosting.com/faq/view?question=37">SSH Tunnels Guide - The Basics</a><br>
<br>
<strong>4:</strong> You configured your Web Browser to use it: <a href="https://www.feralhosting.com/faq/view?question=242">SSH Tunnels - How to use them with your applications.</a><br>
<br>
<h2>Connecting to Plex locally</h2><br>
The Local IP can be found again in the file <code>~&#x2F;private&#x2F;plex&#x2F;README</code>. Use this command to view the URL only.<br>
<br>
 <strong>Important note:</strong>&nbsp; If the result of the command below is an error about the file not existing make sure Plex was actually installed before you continue.<br>
<br>
<pre><code>cat ~&#x2F;private&#x2F;plex&#x2F;README | sed -rn &#x27;s&#x2F;URL: (.*)&#x2F;\1&#x2F;p&#x27;</code></pre><br>
Once connected via the tunnel, using your configured web browser, navigate to:<br>
<br>
<pre><code><a href="http://IP:32400/web">http:&#x2F;&#x2F;IP:32400&#x2F;web</a></code></pre><br>
Where IP is the IP we got from the <code>README</code>. For example:<br>
<br>
<pre><code><a href="http://10.0.3.2:32400/web">http:&#x2F;&#x2F;10.0.3.2:32400&#x2F;web</a></code></pre><br>
<h2>Plex activating remote connections</h2><br>
To avoid having to use the SSH tunnel to talk to Plex we need to make it available for remote connections. To do this, please click the settings icon in the top-right, then server, then &quot;show advanced&quot;. In the general section you may need to sign in. Then select the &quot;remote access&quot; option. You&#x27;ll see an IP address and port provided in this format:<br>
<br>
<strong>1:</strong> Click on the settings icon.<br>
<br>
<img src="https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Plex/0.png"><br>
<br>
<strong>1:</strong> Click in the <code>Server</code> tab<br>
<strong>2:</strong> Click on the <code>General</code> section (if not already selected).<br>
<strong>3:</strong> Enter your plex.tv account email address<br>
<strong>4:</strong> Enter your plex.tv account password<br>
<strong>5:</strong> Click on <code>Sign In</code><br>
<br>
<img src="https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Plex/1.png"><br>
<br>
<strong>1:</strong> You will be logged in and see an avatar of your account.<br>
<strong>2:</strong> Click on the <code>Remote Access</code> section. <br>
<br>
<img src="https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Plex/2.png"><br>
<br>
 <strong>Important note:</strong> Even if the<code>Remote Access</code> if shown as fully active at this point you must still follow this guide to manually specify the port.<br>
<br>
<strong>1:</strong> Make sure you are on the <code>Remote Access</code> section<br>
<strong>2:</strong> Click on the <code>Show Advanced</code> button<br>
<br>
<img src="https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Plex/3.png"><br>
<br>
 <strong>Important note:</strong> You will need to tick the box to manually specify the port, then select the port you chose when setting up static port forwarding. To get your port required for this step you can run this command in SSH:<br>
<br>
<pre><code>ls ~&#x2F;.config&#x2F;feral&#x2F;ns&#x2F;forwarding&#x2F;tcp&#x2F;</code></pre><br>
<strong>1:</strong> Make sure you are in the Remote Access section<br>
<strong>2:</strong> Make sure you have shown the advanced settings<br>
<strong>3:</strong> Check the box to specify the remote port manually.<br>
<strong>4:</strong> Enter the the port shown from by <code>ls</code> command above. The example port used is <code>12345</code><br>
<strong>5:</strong> Click on <code>Retry</code> to active the configuration.<br>
<br>
<img src="https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Plex/4.png"><br>
<br>
Once you have done this you will see something like this:<br>
<br>
<strong>1:</strong> You specified the port using the port forward port.<br>
<strong>2:</strong> You will see your slot&#x27;s <code>IP</code> and the remote port.<br>
<strong>3:</strong> You will see that Remote Access has been fully activated and enabled.<br>
<br>
<img src="https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Plex/5.png"><br>
<br>
<h2>Plex Remote Access via remote URL</h2><br>
 <strong>Important note:</strong> Once the remote connection is activated you will need to disable the SSH tunnel in the browser to connect to the remote URL.<br>
<br>
In a web browser connect to the remote access URL shown in previous steps. It will need to be in the URL format:<br>
<br>
 <strong>Important note:</strong> The port used in the URL will need to be the port used in the port forward we manually specified in Plex.<br>
<br>
<pre><code>123.123.123.123:12345&#x2F;web</code></pre><br>
Using the information shown in the example image we can know the URL for this example is:<br>
<br>
<pre><code>185.21.216.184:12345&#x2F;web</code></pre><br>
Optionally you can replace this IP with the server hostname. Where <code>server</code> is the name of the server that hosts the relevant slot:<br>
<br>
<pre><code>server.feralhosting.com:12345&#x2F;web</code></pre><br>
 <strong>Important note:</strong>&nbsp; When visiting the remote Plex URL it may ask you to login with your plex.tv account<br>
<br>
<img src="https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Plex/login.png"><br>
<br>
<h2>Restarting Plex:</h2><br>
 <strong>Important note:</strong> Plex will be automatically restarted if it is not running. It can take up to ten minutes to reload.<br>
<br>
Run this command to kill the plex processes. Then wait up to 10 minutes for it to restart.<br>
<br>
<pre><code>pkill -9 -fu &quot;$(whoami)&quot; &#x27;plexmediaserver&#x27;</code></pre><br>
<h2>Updating Plex</h2><br>
Run this command to update Plex to the latest version Feral is hosting and then wait up to ten minutes for it to reload.<br>
<br>
<strong>WARNING:</strong> This command will remove and then recreate a blank Plex directory. Any media kept in <code>~&#x2F;private&#x2F;plex</code> will therefore be removed. You should move media out first before running this (and consider putting your media library in a different directory entirely since it does <strong>not</strong> need to be in <code>~&#x2F;private&#x2F;plex</code>.<br>
<br>
<pre><code>pkill -9 -fu &quot;$(whoami)&quot; &#x27;plexmediaserver&#x27; &amp;&amp; rm -rf ~&#x2F;private&#x2F;plex &amp;&amp; mkdir -p ~&#x2F;private&#x2F;plex</code></pre><br>
<h2>Tips for Plex</h2><br>
<strong>Plex is a popular piece of software.</strong> Within the bounds of common sense, if you come across any problems, oddities or tips - please share them! You can do this with a ticket or reviewing this page.<br>
<br>
Plex does not write metadata to video files, instead it creates bundles. If you&#x27;re backing up the Library section please archive them first as it&#x27;ll not only reduce the size but also the time taken to transfer the thousands of files (and confirmation packets) involved in transferring via SFTP.<br>
The channels section is based on the UK locale.<br>
<br>
In <code>web</code> -&gt; <code>player settings</code>, select <code>only image formats</code> for burn subtitles for better performance.<br>
<br>
In <code>web</code> -&gt; <code>general</code>, un check <code>Play Theme Music</code><br>
<br>
If you&#x27;re experiencing issues with buffering with the playstation app streaming plex over remote, the problem is the playstation app, not your &#x2F; ferals connection.<br>
<br>
Add your own tips here!<br>
<br>
User Tip:<br>
If you are getting the error &quot;there was a problem playing this item&quot; There is a simple fix. First log into Plex via the SSH tunnel. Then go to Settings -&gt; Server -&gt; General, and sign out of your account. Then refresh your page and you will get a popup asking if you want to &quot;claim your local server&quot;. Click the link and re enter your username and password. Once that is complete you will need to restart your Plex server via command line. Once your server is back up you should be good to go!<br>
<br>
