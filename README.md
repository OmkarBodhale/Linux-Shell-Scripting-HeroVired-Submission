# Linux-Shell-Scripting-HeroVired-Submission

Question 1: Set Up Your DevOps Project Structure

**Solution :**

● Create the directory /home/ec2-user/webapp/ with three subdirectories inside it: scripts/, logs/, and config/ using a single mkdir -p command.

<img width="1257" height="225" alt="image" src="https://github.com/user-attachments/assets/5a54d429-7e90-4fb4-92f0-c457f89e5226" />

● Use cat > to create config/app.conf with two lines of content: APP_NAME=WebApp and PORT=8080. Save using Ctrl+D.

<img width="1322" height="215" alt="image" src="https://github.com/user-attachments/assets/a22b8bc8-a3fe-4bef-b0d0-b27cac470f59" />

● Use touch to create an empty file at logs/app.log. Confirm it is 0 bytes using ls -l.
<img width="750" height="315" alt="image" src="https://github.com/user-attachments/assets/f0881910-da76-4250-bd2b-8f67720911af" />

● Set permissions: chmod 755 scripts/ and chmod 644 config/app.conf. Explain in your own words what 755 and 644 mean for owner, group, and others.

<img width="651" height="243" alt="image" src="https://github.com/user-attachments/assets/6af2b195-dd01-4291-8535-c10dec1c7c67" />

● What it means:

    ● chmod stands for Change Mode. It alters who can read, write, or execute a file/folder.
    ● Linux permissions use three numbers representing three groups: Owner, Group, and Others.
    ● The numbers are calculated using binary weights: Read (r)=4, Write (w)=2, Execute (x)=1.
  
● 755 (rwxr-xr-x): The Owner gets 7 ($4+2+1$), meaning full Read, Write, and Execute rights. The Group and Others get 5 ($4+1$), meaning they can view and run scripts inside the folder, but cannot change or delete them.
● 644 (rw-r--r--): The Owner gets 6 ($4+2$), meaning they can Read and Write to the config file. The Group and Others get 4, meaning they can read the configuration but cannot modify it.

● Recursively change ownership of the entire webapp/ directory to root:root using chown -R. Then run ls -lR /home/ec2-user/webapp/ and share the output to confirm every file and folder shows root root as owner.

Expected final structure:

webapp/

├── scripts/          (drwxr-xr-x  root root)

├── logs/             (drwxr-xr-x  root root)

└── config/           (drwxr-xr-x  root root)

    ├── app.conf          (-rw-r--r--  root root)

    └── app.log           (-rw-r--r--  root root)
    
<img width="1897" height="51" alt="image" src="https://github.com/user-attachments/assets/0ab0a589-4766-4ec2-8014-6eb9d1eab95b" />

<img width="1913" height="437" alt="image" src="https://github.com/user-attachments/assets/cc560be3-09a1-4f78-89ce-54624a41330a" />

--------------------------------------------------------------------------------------------------------------------------

Question 2: Write an Interactive Log Script

**Solution :**

● Create a new script file at /home/ec2-user/webapp/scripts/log_user.sh using vim. Start with the correct shebang line.

<img width="1912" height="48" alt="image" src="https://github.com/user-attachments/assets/0dd34fab-42a3-438e-ac8c-392aaaab255b" />


● Use read -p to prompt the user to enter their name and store it in a variable called username.

● Use cat with the absolute path to display the contents of config/app.conf to the screen.

● Append a log entry to logs/app.log using echo >> in this exact format: Login: $username Date: $(date). Then display the full log file contents.

<img width="1918" height="196" alt="image" src="https://github.com/user-attachments/assets/e2ac3de7-f36c-42ad-8fcd-93f288bb8ae0" />

<img width="1905" height="153" alt="image" src="https://github.com/user-attachments/assets/b27449de-2f95-4ad9-80c2-c2d01aa83a49" />


● Give the script execute permission with chmod +x and run it at least 3 times using different names

<img width="1912" height="31" alt="image" src="https://github.com/user-attachments/assets/544e973d-be86-48ae-a9d6-433f45a8d45a" />

<img width="1918" height="462" alt="image" src="https://github.com/user-attachments/assets/47247199-b083-4fb0-9375-42990c487453" />

Question 3: User Management and File Permission Control

**Solution :**

● Create a group called writers

<img width="1917" height="58" alt="image" src="https://github.com/user-attachments/assets/0742957e-84be-4dfc-ba0d-b3192cb79ae0" />

● Create 4 users with home directories:

<img width="1918" height="120" alt="image" src="https://github.com/user-attachments/assets/bd5d4189-a337-498e-9380-ca0620ee2ff7" />

● Add the two write-access users to the writers group:

<img width="1912" height="111" alt="image" src="https://github.com/user-attachments/assets/b017faae-a0ec-4772-a17d-de4e18af9754" />

● Change the group ownership of log_user.sh to writers: sudo chown root:writers /home/ec2-user/webapp/scripts/log_user.sh

<img width="1918" height="50" alt="image" src="https://github.com/user-attachments/assets/c47c0802-1abc-416e-bdf5-ae40a410d5b5" />

● Set permissions to 664 so writers group gets rw and others get r only: sudo chmod 664 /home/ec2-user/webapp/scripts/log_user.sh

<img width="1917" height="51" alt="image" src="https://github.com/user-attachments/assets/cb8dd891-90b8-4e1d-9d38-4baf25a72d7b" />

● Verify the permission output shows: -rw-rw-r--  root  writers  log_user.sh


<img width="1917" height="71" alt="image" src="https://github.com/user-attachments/assets/eb6a376a-a0c9-46db-b3b9-4dd9448194d7" />


● Switch to each user and test access to confirm it is working correctly:

<img width="1902" height="292" alt="image" src="https://github.com/user-attachments/assets/9f36414c-3bc2-44a8-8643-ad52054a9264" />

<img width="1911" height="773" alt="image" src="https://github.com/user-attachments/assets/9718fb58-2c24-4c54-a6db-a503146d2bfa" />

<img width="1916" height="553" alt="image" src="https://github.com/user-attachments/assets/db25296e-4ff4-4f98-ac0e-a3da9fa71d8a" />

<img width="1908" height="247" alt="image" src="https://github.com/user-attachments/assets/426674cc-444a-40fb-9c75-5b0ac8fe7b50" />

<img width="1917" height="756" alt="image" src="https://github.com/user-attachments/assets/9adf515c-0410-45bb-a641-8d6a73698307" />

