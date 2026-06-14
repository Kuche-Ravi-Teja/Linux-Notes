# --------------- Key Based Authentication --------------- <u/>

### Key-based authentication is a highly secure method of logging into a Linux server remotely using SSH (Secure Shell).

### Instead of typing a traditional password (which can be guessed, intercepted, or brute-forced by hackers), key-based authentication uses a matching pair of cryptographic keys—like a physical lock and its matching key—to verify your identity instantly.

## <u> How It Works: The Analogy <u/>

  - Key-based authentication relies on an asymmetric cryptography pair:

  - The Private Key (Your Physical Key): This stays safely on your local computer. You must never share it with anyone.

  - The Public Key (The Lock): This is placed on the remote Linux server you want to access. Anyone can see it; it's completely safe if exposed.

  - When you try to log in, the server creates a cryptographic puzzle using your Public Key and sends it to your computer. Your local computer uses its Private Key to instantly solve the puzzle and sends the answer back. The server verifies the answer and lets you in without you ever typing a password.

## <u> Step-by-Step Implementation Guide <u/>

Here is how a professional sets up passwordless, key-based authentication between a local computer and a remote Linux server.

### Step 1: Generate the Key Pair on Your Local Machine

  - First, you need to create your public and private keys. We use the modern, highly secure ed25519 algorithm.

  - Open your local terminal and run:

        ssh-keygen -t ed25519 -C "admin@company.com"
        -t ed25519: Specifies the type of key to create (fastest and most secure standard).
        
        -C "comment": Adds a professional label (like your email) to the end of the key file so you can identify it later.

  - What happens next:

  - The terminal will ask: "Enter file in which to save the key". Press Enter to accept the default location (~/.ssh/id_ed25519).

  - It will ask for a passphrase. This is an optional password to protect your private key on your local machine. You can press Enter to skip it for pure automation, or add one for maximum security.

  - This creates two files in your ~/.ssh/ directory:

        id_ed25519 (Your Private Key 🛑 Keep Secret!)
        
        id_ed25519.pub (Your Public Key 🟢 Shareable)


### Step 2: Copy Your Public Key to the Remote Server

  - Now, you need to install the "lock" (your public key) onto the remote Linux server.

  - Run this command on your local machine:

        ssh-copy-id ubuntu@192.168.1.50
        (Replace ubuntu with your server's username and 192.168.1.50 with your server's actual IP address).

  - What happens next:

  - The system will prompt you for your remote server's password one last time.

  - It automatically takes your public key (id_ed25519.pub) and appends it safely inside a special file on the server located at /home/ubuntu/.ssh/authorized_keys.


### Step 3: Test Your Secure Login

  - Once the key is copied, test your connection. You should automatically fly straight into the server terminal without being prompted for a password:

        ssh ubuntu@192.168.1.50

    
### Step 4: Lock Down the Server (Professional Best Practice)

  - Once you confirm that your key-based authentication works perfectly, it is standard professional practice to turn off traditional password logins completely.
  - This stops hackers from trying to guess passwords on your server.

  - Log into your remote server.

  - Open the SSH configuration file with admin privileges:

        sudo nano /etc/ssh/sshd_config

  - Look for the following lines, uncomment them (remove the #), and change them to no:

        Plaintext
        PasswordAuthentication no
        PubkeyAuthentication yes
        Save and exit the file (In nano, press Ctrl+O, Enter, then Ctrl+X).

  - Restart the SSH service to apply the new security rules:

        sudo systemctl restart ssh
    
⚠️ Warning: Make sure your key login works perfectly in a separate terminal window before closing your current session, or you risk locking yourself out of the server!

## <u> Why Use It? (Key Benefits) <u/>

  - Brute-Force Immunity: Automated hacking bots try millions of common password combinations on servers daily. Key authentication makes brute-forcing mathematically impossible.

- DevOps Automation: Essential for tools like Ansible, Jenkins, or GitHub Actions to log into servers securely and deploy applications automatically without human intervention.

- Centralized Access Control: If an employee leaves a company, an administrator can simply delete their single public key from the authorized_keys file to immediately revoke their access.
