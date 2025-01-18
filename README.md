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
