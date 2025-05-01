# Creating a Standard User Account on Your Ubuntu VPS

Hello! For better security, we'll create a standard user account on your VPS instead of always using the root account. Here are step-by-step instructions:

## Step 1: Connect to Your VPS as Root
1. Open Terminal on your Mac
2. Connect to your VPS with:
   ```
   ssh root@5.78.69.191
   ```
3. Enter your root password when prompted

## Step 2: Create a New User
1. Once connected as root, create a new user (replace "username" with the name you want):
   ```
   adduser username
   ```

2. You'll be asked to:
   - Enter a password (twice)
   - Fill in some optional information (you can press Enter to skip these)

## Step 3: Give Your New User Administrative Privileges
1. Add your new user to the sudo group so you can perform administrative tasks:
   ```
   usermod -aG sudo username
   ```

## Step 4: Set Up SSH Keys for Your New User
1. While still logged in as root, create the SSH directory for your new user:
   ```
   mkdir -p /home/username/.ssh
   ```

2. Copy your public key to the authorized_keys file for your new user:
   ```
   cp /root/.ssh/authorized_keys /home/username/.ssh/
   ```

3. Set the correct ownership and permissions:
   ```
   chown -R username:username /home/username/.ssh
   chmod 700 /home/username/.ssh
   chmod 600 /home/username/.ssh/authorized_keys
   ```

## Step 5: Test Your New User Account
1. Open a new Terminal window on your Mac
2. Connect using your new username:
   ```
   ssh username@5.78.69.191
   ```
3. You should connect without needing to enter a password (if you set up SSH keys)

## Step 6: Confirm You Can Use Sudo
1. Try running a command with sudo:
   ```
   sudo apt update
   ```
2. Enter your user password when prompted
3. If this works, your new user account is set up correctly with administrative privileges

After confirming everything works properly, you can let your administrator know so they can secure the root account.
