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
    Clone the Cowrie repository:
    <pre><code>git clone https://github.com/cowrie/cowrie.git</code></pre>
  </li>
  <li>
    Navigate into the Cowrie directory:
    <pre><code>cd cowrie</code></pre>
  </li>
  <li>
    Set up a Python virtual environment:
    <pre><code>python3 -m venv cowrie-env
source cowrie-env/bin/activate</code></pre>
  </li>
  <li>
    Upgrade pip and install required dependencies:
    <pre><code>pip install --upgrade pip
pip install -r requirements.txt</code></pre>
  </li>
  <li>
    Copy the default configuration file:
    <pre><code>cp etc/cowrie.cfg.dist etc/cowrie.cfg</code></pre>
  </li>
  <li>
    Start Cowrie:
    <pre><code>./bin/cowrie start</code></pre>
  </li>
</ol>
</div>

### 3.How can we Monitor the Logs?
<p>
    We need to now monitor the logs that are generated by our honeypot to understand the attackers actions and analyze the attacks they are performing.
</p>
<div>
<a href="https://postimg.cc/LhMcLjZ9">
    <p>
    "tail var/log/cowrie/cowrie.log"
    </p>
</a>
<p>
       Likely you'll run into some problems. You'll most likely discover that the log file wasn't found. You will most likely need to create the output in the configuration file and try to do it again.
    </p>
<ol>
  <li>
    List Cowrie’s log directory:
    <pre><code>ls var/log/cowrie</code></pre>
    <ul>
      <li>
        If you get a “No such file or directory” error, it means the directory doesn’t exist yet. You can create it:
        <pre><code>mkdir -p var/log/cowrie</code></pre>
      </li>
      <li>
        Alternatively, confirm that Cowrie was installed or configured correctly before proceeding.
      </li>
    </ul>
  </li>
  <li>
    Open the Cowrie configuration file to edit it:
    <pre><code>nano etc/cowrie.cfg</code></pre>
  </li>
  <li>
    Specify the location of the Cowrie log file in the config:
    <pre><code>log.output = var/log/cowrie/cowrie.log</code></pre>
  </li>
  <li>
    Continuously monitor the Cowrie log file in real-time: 
    <pre><code>tail -f var/log/cowrie/cowrie.log</code></pre>
      We will use this for when we attack the honeypot.
  </li>
</ol>
</div>

### 4.Adding our own Files
<p>
    Before we start our attack, we must put some files to really understand how to trick the attacker.
</p>
<div>
<a href="https://postimg.cc/kRDCzb3Y">
    <p>
    "Fake confidential information"
    </p>
</a>

### 5.Attacking the Honeypot
<p>
    Let's now attack our honeypot by using Kali Linux! 
</p>
<ol>
    <li>
        Before we do we must figure out the honeypots IP address on the Ubuntu system. I won't show you the IP for obvious reasons but this is the command
        <pre><code>ip addr</code></pre>
    </li>
    <li>
        We will also use the command we did to monitor our log files in real time
        <pre><code>tail -f var/log/cowrie/cowrie.log</code></pre>
    </li>
    <li>
        We will now hop onto our Kali Linux system to perform an SSH login. 
        <pre><code>ssh root@(honeypot_ip) -p 2222</code></pre>
        You can find the password by doing <pre><code>cat userdb.example</code></pre>
    </li>
    
</ol>
