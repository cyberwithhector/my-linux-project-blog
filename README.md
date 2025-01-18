# My First Linux Project: Building a Mock Office for a Cybersecurity Company

Hey there! So, I’m diving into the world of **Linux administration**, and I thought, what better way to get my feet wet than to build a **mock office environment** for a cybersecurity company? Sure, I’m not sure yet if I’ll land a **sysadmin** role, but I’m taking it one step at a time. This project is my first hands-on attempt at learning Linux and gaining some real experience that’ll help me in **cybersecurity**, **DevOps**, and maybe even **cloud** someday.

---

## Why This Project?

Honestly, I wanted something practical to get started with Linux—something that would give me a feel for how things work in the real world. Setting up a mock office for a cybersecurity company gives me the perfect chance to practice creating users, managing access, and organizing files, all of which will be super useful down the line.

---

## Step 1: Creating Groups for Each Department

In an office, you’ve got different teams working on different stuff, so I figured it would make sense to organize the users into departments. I made four departments for this project: **IT**, **HR**, **Finance**, and **Cybersecurity**. Each department gets its own group.



### Linux Commands:
```bash
sudo groupadd IT
sudo groupadd HR
sudo groupadd Finance
sudo groupadd Cybersecurity
```

![Screenshot of creating groups](https://github.com/cyberwithhector/my-linux-project-blog/blob/main/Screen%20Shot%202025-01-17%20at%2011.41.19%20PM.png)





## Step 2: Create User Accounts

Next, I created user accounts for the employees. **Admins** (Goku and Vegeta) will have full access to everything, while **regular users** (Piccolo and Bulma) will only have access to their department's directories.

### Linux Commands:
```bash
# Create Admin Users (Goku and Vegeta)
sudo useradd -m -G sudo goku
sudo useradd -m -G sudo vegeta

# Create Regular Users (Piccolo and Bulma)
sudo useradd -m piccolo
sudo useradd -m bulma

# Assign Users to Their Department Groups
sudo usermod -aG IT piccolo     # Piccolo is part of IT
sudo usermod -aG HR bulma       # Bulma is part of HR
```

![Screenshot of creating groups](https://github.com/cyberwithhector/my-linux-project-blog/blob/main/Screen%20Shot%202025-01-17%20at%2011.55.37%20PM.png)

![Screenshot of creating groups](https://github.com/cyberwithhector/my-linux-project-blog/blob/main/Screen%20Shot%202025-01-18%20at%2012.51.19%20AM.png)





## Step 3: Set Up Directory Structure for Departments

Now it’s time to create the directory structure that will represent each department in the office. This will allow us to organize the data in a way that reflects real-world access control.

### Linux Commands:
```bash
# Create the main directory for the company and subdirectories for each department
sudo mkdir -p /company/IT
sudo mkdir -p /company/HR
sudo mkdir -p /company/Finance
sudo mkdir -p /company/Cybersecurity
```

![Screenshot of creating groups](https://github.com/cyberwithhector/my-linux-project-blog/blob/main/Screen%20Shot%202025-01-17%20at%2011.57.56%20PM.png)





## Step 4: Set Directory Ownership and Permissions

To ensure that the right users have access to the right directories, we need to set the correct ownership and permissions.

### Linux Commands:
```bash
# Set Group Ownership for Directories
sudo chown :IT /company/IT
sudo chown :HR /company/HR
sudo chown :Finance /company/Finance
sudo chown :Cybersecurity /company/Cybersecurity

# Set Permissions for Directories
sudo chmod 770 /company/IT         # IT group (Goku, Vegeta, Piccolo) can read, write, execute
sudo chmod 770 /company/HR         # HR group (Goku, Vegeta, Bulma) can read, write, execute
sudo chmod 770 /company/Finance    # Finance group (Goku, Vegeta) can read, write, execute
sudo chmod 770 /company/Cybersecurity # Cybersecurity group (Goku, Vegeta) can read, write, execute
```


![Screenshot of creating groups](https://github.com/cyberwithhector/my-linux-project-blog/blob/main/Screen%20Shot%202025-01-18%20at%2012.37.05%20AM.png)

![Screenshot of creating groups](https://github.com/cyberwithhector/my-linux-project-blog/blob/main/Screen%20Shot%202025-01-18%20at%203.28.29%20AM.png)







## Step 5: Test User Access

Let’s make sure everything works as expected. I’ll log in as each user and test whether they can access the right directories. Admins (Goku and Vegeta) should have full access to all directories, while regular users (Piccolo and Bulma) should only have access to their respective department’s directories.

### Linux Commands:
```bash
# Log in as Piccolo (a regular user in the IT department)
su - piccolo
ls /company/IT       # Piccolo should have access to IT
ls /company/HR       # Piccolo should not have access to HR
ls /company/Finance  # Piccolo should not have access to Finance
ls /company/Cybersecurity  # Piccolo should not have access to Cybersecurity

# Log in as Bulma (a regular user in the HR department)
su - bulma
ls /company/HR       # Bulma should have access to HR
ls /company/IT       # Bulma should not have access to IT
ls /company/Finance  # Bulma should not have access to Finance
ls /company/Cybersecurity  # Bulma should not have access to Cybersecurity
```


![Screenshot of creating groups](https://github.com/cyberwithhector/my-linux-project-blog/blob/main/Screen%20Shot%202025-01-18%20at%2012.52.43%20AM.png)

![Screenshot of creating groups](https://github.com/cyberwithhector/my-linux-project-blog/blob/main/Screen%20Shot%202025-01-18%20at%2012.55.01%20AM.png)







## Step 6: Optional Enhancements

Here are two optional enhancements to improve the setup: a **shared directory** for everyone and **logging** to track access attempts.

### 1. Create a Shared Directory
To create a directory that all users can access (read-only for regular users, but admins can modify), we can set up a shared directory.

#### Linux Commands:
```bash
# Create a Shared Directory
sudo mkdir /company/shared

# Set Permissions: Read-only for others (755)
sudo chmod 755 /company/shared
```

### 2. Enable Logging with auditd
Logging is crucial for tracking access to sensitive data. I set up logging to monitor changes to the HR directory using the auditd tool.


#### Linux Commands:
```bash
# Install auditd (if not already installed)
sudo apt install auditd

# Enable Logging for the HR Directory
sudo auditctl -w /company/HR -p rwxa -k HR_access

# Explanation of Flags:
# -w: Watch the directory (/company/HR)
# -p: Permissions to monitor (r=read, w=write, x=execute, a=attribute changes)
# -k: Custom key for identifying logs (HR_access)

# View Logs for HR Access Attempts
sudo ausearch -k HR_access
```


## Conclusion

This project was a great way to start exploring **Linux administration**. I learned a lot about managing users, groups, directories, and permissions, and setting up a mock office environment helped me see how these concepts apply in real-world IT scenarios. It also brought me one step closer to my goals of working in an interesting field like **cybersecurity**, **DevOps**, or **cloud computing**.

### Key Takeaways:
- **Groups**: A simple way to organize users and control access across departments.  
- **Permissions**: Essential for keeping data secure and ensuring everyone has the right level of access.  
- **Admins vs. Regular Users**: Admins can manage the system, while regular users have limited access to just what they need.  
- **Optional Enhancements**: Adding features like shared directories and logging can improve both collaboration and security.  

While I’m still figuring out exactly where I want to go in my career, this project has been a solid way to practice and build my skills. I’m looking forward to continuing to learn, take on new challenges, and grow my expertise.
