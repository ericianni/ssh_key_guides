## Motivation
Two-factor authentication is becoming more and more of standard operating proceedure for large orginizations. Oregon State University is no different and two-factor authentication will soon be manditory. Many of you are accustomed to using Duo to authenticate when logging into your email or Canvas. 

What some of you may not have realized is that two-factor authentication is now required for logging into Flip. This can cause problems with people who are not using a terminal to access the school servers as there is an additional prompt that requires a response. This is of particular inconvience to those using FTP programs. 

Below are guides to help streamline logging onto Flip without the need of involving Duo.
## Windows Guide
For this you will need:

* PuTTY Key Generator - a program to generate ssh private and public keys (download [here](http://the.earth.li/~sgtatham/putty/latest/x86/puttygen.exe))
* Some way to log onto Flip such as PuTTY (available [here](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html))
* A FTP Client such as Filezilla (available [here](https://filezilla-project.org/))

#### Steps
1. Open up PuTTY Key Generator, click "Generate," and follow the on-screen instructions
2. Once the key is generated, you will need to save the public key

   ![Save public key](./images/windows/win_save_public_key.png)

   Save it to a location you will be able to easily find it and name it `id_rsa.pub`
   
3. Now you need to save the private key

   ![Save public key](./images/windows/win_save_private_key.png)
   
   Ignore the warning about the passcode. Save it to the same location as before and name it `id_rsa.ppk`
   
4. Using PuTTY, log onto Flip and enter your password when prompted
5. You will be presented with a Duo two-factor prompt. Enter `1` and press enter. This will send a request to your Duo Mobile app which you will need to accept
   
   ![Duo prompt](./images/windows/win_flip_duo_prompt.png)
   
6. You are now logged onto Flip
7. Use your favorite command text editor (mine is emacs) to open up `~/.ssh/authorized_keys` which should be an empty file. If it does not exist, create it
8. Now, locate the public key file you saved and open it with notepad and copy the key as shown in the image below

   ![Copy public key](./images/windows/win_notepad_pub_key.png)

9. Back in the editor on Flip, type `ssh-rsa` followed by a space and the paste the copied public key and save the changes

   ![Update authorized keys](./images/windows/win_flip_save_auth_key.png)

10. Back in PuTTY, you want to create a Saved Session you have not done so already

  1. In Host Name entere `your_username@access.engr.oregonstate.edu`
     
	 ![Enter host name](./images/windows/win_session_url.png)
	 
  2. Below in the Saved Sessions field enter `flip` and click Save
  
     ![Save session anme](./images/windows/win_save_session.png)
	 
  3. Click Connect->SSH->Auth on the sidebar
  
     ![Open Connection->SSH->Auth](./images/windows/win_ssh_auth_panel.png)
	 
  4. On this screen, Browse to the location of your private key file: id_rsa.ppk. Now click the Open Button at the bottom
  
     ![Load private key](./images/windows/win_load_private_key.png)
	 
  5. You should not be logged onto Flip without needing to provide a password OR two-factor authorization
  
     ![SSH Key success](./images/windows/win_putty_key_auth.png)
 
11. Now we need to set up FileZilla
  1. Open Filzilla and go to File->Site Manager
     
	 ![Open Site Manager](./images/windows/win_filezilla_site_manager.png)
	 
  2. Create a New Site and name it `flip`
   
     ![Create new site](./images/windows/win_filezilla_new_site.png)
	 
  3. To the right in the General Tab, Select `SFTP` for the Protocol and enter the Host as `access.engr.oregonstate.edu`
  
     ![Enter Host](./images/windows/win_filezilla_enter_host.png)
	 
  4. For Logon Type select `Key file`, enter your username for User, and then browse to the location of your `id_rsa.ppk' file.
 
     ![Set User and load key](./images/windows/win_filezilla_load_key.png)
	 
  5. Click Connect at the bottom and you should now be connected to Flip without the need of two-factor authentication!
  
## Mac Guide

## Linux Guide
