# Connecting to Your Cloud VPS from Your Mac

Hello! I'm going to guide you through connecting to your cloud VPS using your Mac. These instructions are designed to be beginner-friendly, as I understand you haven't used Terminal before.

## What You'll Need
- Your Mac computer
- The VPS IP address: 5.78.69.191
- The root password (provided separately by your administrator)

## Basic Connection Instructions

1. **Open Terminal**
   - Click on the Spotlight search icon (magnifying glass) in the top-right corner of your screen
   - Type "Terminal" and press Enter when it appears in the results

2. **Connect to Your VPS**
   - In the Terminal window, type this command exactly as shown:
   ```
   ssh root@5.78.69.191
   ```
   - Press Enter after typing the command

3. **First-Time Connection**
   - You'll see a message asking if you're sure you want to connect
   - Type `yes` and press Enter

4. **Enter Password**
   - Type the root password that was provided to you
   - Note: When typing passwords in Terminal, you won't see any characters appear—this is normal
   - Press Enter after typing the password

5. **Success!**
   - If everything worked, you'll now be connected to your VPS

## Setting Up SSH Keys (More Secure Option)

For more security and convenience (so you don't need to type your password each time):

1. **Create an SSH Key**
   - In Terminal on your Mac, type:
   ```
   ssh-keygen -t ed25519
   ```
   - Press Enter

2. **Save the Key**
   - When asked where to save the key, just press Enter to use the default location

3. **Create a Passphrase**
   - You'll be asked to enter a passphrase - this is like a password for your key
   - Type a passphrase and press Enter (or press Enter twice for no passphrase)

4. **Copy Your Key to the VPS**
   - Type this command:
   ```
   ssh-copy-id -i ~/.ssh/id_ed25519.pub root@5.78.69.191
   ```
   - Enter your root password when prompted

5. **Connect Without Password**
   - Now you can connect by simply typing:
   ```
   ssh root@5.78.69.191
   ```
   - If you set a passphrase, you'll be asked for that instead of the server password

If you have any questions or run into any issues, please let your administrator know!
