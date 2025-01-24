# Honeypot Lab (in progress.)

## Objective

Setting up a honeypot on Ubuntu is a great way to learn about cyberattacks by creating a fake system that looks vulnerable. This fake system attracts attackers, which security teams can watch the attackers actions, what tools they use, and why they're attacking. The information gathered helps improve cyber defense, protect real systems, and stay ahead of potential threats, all while keeping the actual network safe. 

### Skills Learned


- Skill 1
- Skill 2

### Tools Used

- List the tools and what you did with it.

## Steps

These are the steps to create a vulnerable system to trick attackers.

### 1.Updating the Operating System
<p>
    We need to update our OS by doing this command. 
</p>
<div>
<a href="https://postimg.cc/v4Qh8FYx">
    <p>
    "sudo apt-get update".
    </p>
<div>
    <p>
    We will also install the python dependencies.
        <li>apt install python3.11-venv</li>
</p>
      <p>
        I showed the proof I already installed it but when you first do it you will get something else and it'll be much longer.
    </p>
<a href="https://postimg.cc/tZVwdQVC">
    <p>
    "sudo apt-get install git python3-venv libssl-dev libffi-dev build-essential libpython3-dev python3-minimal authbind".
    </p>
</a>
</div>
<p>
        Keeping your system updated with the latest patches is essential to prevent attackers from exploiting vulnerabilities during the setup process. Regular updates enhance the security and stability of your honeypot environment.
    </p>
</div>

### 2.Making a User.
 <p>
    We need to make our own user for security purposes. This is the user we will be when installing Cowrie.
 </p>
<div>
<a href="https://postimg.cc/2qcPvvtR"> 
    <p>
    "sudo adduser --disabled-password cowrie".
    </p>
    <p>
    "sudo su - cowrie"
    </p>
</a>
    <p>
        Creating a dedicated Cowrie user enhances security by limiting its permissions and isolating it from critical system processes. This follows the principle of least privilege, ensuring that even if Cowrie is compromised, the impact is contained to the cowrie user environment. Running Cowrie as a non-root user reduces security risks and aligns with best practices for safeguarding the system.
    </p>
</div>
    
### 3.Installing our Honeypot Tool
<p>
   Now installing the Honeypot tool is easy! The tool we will use is Cowrie and we need to first pull it from GitHub.
</p>
<div>
<a href="https://postimg.cc/ftmWKD0v">
    <p>
    "git clone http://github.com/cowrie/cowrie".
    </p>
</a>
<p>
        We will also set up the virtual environment for our Honeypot.
    </p>
</div>
<div>
<a href="https://postimg.cc/8JMZsrzj">
    <p>
    "git clone https://github.com/cowrie/cowrie.git".
    </p>
</a>
    <ol>
  <li>
    Install dependencies:
    <pre><code>sudo apt update
sudo apt install python3-pip git python3-venv -y</code></pre>
  </li>
  <li>
    Navigate into the Cowrie directory:
    <pre><code>cd cowrie</code></pre>
  </li>
  <li>
    Set up a Python virtual environment:
    <pre><code>python3 -m venv cowrie-env</code></pre>
  </li>
  <li>
    Clone the Cowrie repository:
    <pre><code>git clone https://github.com/cowrie/cowrie.git</code></pre>
  </li>
  <li>
      Actuvate the Cowrie source code:
      <pre><code>source cowrie-env/bin/activate</code></pre>
  </li>
  <li>
    Upgrade pip and install required dependencies:
    <pre><code>pip install --upgrade pip
pip install -r requirements.txt</code></pre>
  </li>
</ol>
</div>

### 2.Configure Cowrie Rules
<p>
   We will now configure the Cowrie rules. This will be configured on the .cfg file
</p>
<ol>
 <li>
    Where the cfg file is located.
    <pre><code>nano cowrie.cfg.distt</code></pre>
 </li>
</ol>
<div>
<a href="https://postimg.cc/fkrbFfbH">
    <p>
    "[telnet] 
     enabled = true".
    </p>
</a>
<p>
        We enabled Telnet through the cfg file.
    </p>
</div>

### 3.Adding a Password
<p>
   We will now configure the Cowrie rules. This will be configured on the .cfg file
</p>
    <div>
<a href="https://postimg.cc/2qPjDnqv">
    <p>
    "user:x:password".
    </p>
</a>
<p>
    That's how the username and password is set up. X is not used as anything.
</p>
    </div>
    <p>We will now make our own text file with a username and password.</p>
    <ol>
        <li>
            <pre><code>touch /home/cowrie/cowrie/etc/userdb.txt</code></pre>
        </li>
        <li>
            We create the .txt file.
            <pre><code>touch userdb.txt</code></pre>
        </li>
        <li>
            Lets now add some content to the .txt file.
            <pre><code>nano userdb.txt</code></pre>
            Once you get into the file.
            <pre><code>root:x:pass</code></pre>
        </li>
    </ol>
    
### 4.Start Your Engines!!!
<p>
   We will now start Cowrie!
</p>
<div>
    <a href="https://postimg.cc/B8qvqR00">
    <p>
    "bin/cowrie start".
    </p>
    </a>
    <p>For proof if it's running it'll say another twistd server is running, PID ####</p>
    <p>To stop the process "bin/cowrie stop"</p>
</div>
<p>
   We can examine what occurs in the log file.
</p>
<div>
    <a href="https://postimg.cc/qggKPPkm">
    <p>
    "bin/cowrie start".
    </p>
    </a>
    <p>Honeypot log files, like those from Cowrie, capture and analyze attacker behavior, including login attempts, commands executed, and files uploaded. They help researchers and security teams understand emerging threats, identify attack patterns, and improve defenses by providing insights into attacker tactics and vulnerabilities targeted. Logs also aid in forensics, malware analysis, and strengthening intrusion detection systems.</p>
</div>

### 5.Installing and configuring the Splunk universal forwarder
<p>Installing the Splunk Universal Forwarder on your Cowrie server enables use to make the honeypot logs actionable and meaningful within Splunk. This enhances the ability to detect threats, understand attacker behavior, and improve overall security posture.</p>
<p>
    But before we start we must open necessary ports on our cowrie box.
</p>
<ol>
    <li>Port 22: For SSH access (important for Cowrie honeypot functionality).</li>
    <li>Port 80: For HTTP traffic (if Splunk Web or other tools require this).</li>
    <li>Port 443: For HTTPS traffic (encrypted communication with Splunk or other tools).</li>
    <li>Port 9997: Used by Splunk Universal Forwarder to send logs to the Splunk indexer.</li>
    <li>Port 8088: For Splunk HTTP Event Collector (HEC), if you plan to use it.</li>
    <li>Port 8090: For Splunk management or other specific services.</li>
</ol>
<p>This is how we put the commands.</p>
<ol>
    <pre><code>iptables -A INPUT -p tcp --dport 22 -j ACCEPT 
iptables -A INPUT -p tcp --dport 80 -j ACCEPT  
iptables -A INPUT -p tcp --dport 443 -j ACCEPT  
iptables -A INPUT -p tcp --dport 9997 -j ACCEPT 
iptables -A INPUT -p tcp --dport 8088 -j ACCEPT  
iptables -A INPUT -p tcp --dport 8090 -j ACCEPT</code></pre>
</ol>
<div>
    <a href="https://postimg.cc/Ffts1hHD">
    <p>
    "sudo iptables-save | sudo tee /etc/network/iptables.rules".
    </p>
    </a>
    <p>This shows that the inputs on those ports are now accepted.</p>
</div>
<p>
    We will now add Splunk and its packages into the cowrie server.
</p>
<ol>
    <li><pre><code>sudo useradd -m splunk</code></pre></li>
    <li><pre><code>sudo mkdir /opt/splunkforwarder/</code></pre></li>
    <li><pre><code>chown -R splunk:splunk /opt/splunkforwarder</code></pre></li>
    <li><pre><code>su - splunk</code></pre></li>
    <li><pre><code>chown -R splunk:splunk /opt/splunkforwarder</code></pre></li>
    <li><pre><code>wget -O splunkforwarder-9.2.0.1-d8ae995bf219-linux-2.6-amd64.deb "https://download.splunk.com/products/universalforwarder/releases/9.2.0.1/linux/splunkforwarder-9.2.0.1-d8ae995bf219-linux-2.6-amd64.deb"</code></pre></li>
    <li><pre><code>wget -O splunkforwarder-9.2.0.1-d8ae995bf219-linux-2.6-amd64.deb "https://download.splunk.com/products/universalforwarder/releases/9.2.0.1/linux/splunkforwarder-9.2.0.1-d8ae995bf219-linux-2.6-amd64.deb"</code></pre></li>
   <li><pre><code>sudo /opt/splunkforwarder/bin/splunk start --accept-license</code></pre></li>
   <li><pre><code>cd /opt/splunkforwarder/bin</code></pre></li>
</ol>
