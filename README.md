# Jenkins


There are two different type of authtication are in the github
1. SSH authentication
2. Personal access Token (PAT) authentication
    a. Fine-grained personal access tokens
    b. Classic Token


1. SSH key Setup for Git pull Push  

✅ Steps to Fix
1. Check if SSH key exists:
Run the following in your terminal:

ls ~/.ssh/id_ed25519.pub
or

ls ~/.ssh/id_rsa.pub
If neither file exists, you need to create an SSH key.

2. Generate a new SSH key (if needed):

ssh-keygen -t ed25519 -C "your_email@example.com"
(Use RSA if you're on an older system: ssh-keygen -t rsa -b 4096 -C "your_email@example.com")

Just press Enter to accept default file locations. Then start the SSH agent:
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
3. Add the public key to GitHub:
Copy the public key:

cat ~/.ssh/id_ed25519.pub
Go to GitHub > Settings > SSH and GPG keys > New SSH key. Paste the key there.

4. Test SSH connection:

ssh -T git@github.com
You should see a success message like:

Hi username! You've successfully authenticated...

5. Try the push again:

git push -u origin main
Let me know if you want help automating this or checking your SSH key setup.

=======================================================================
2. PAT Setup


🔧 Step-by-Step: Use Token with HTTPS
1. Generate a GitHub Token
Go to GitHub Token Settings.

Click "Generate new token (classic)" or use "Fine-grained tokens" (recommended for tighter security).

Choose scopes:

For pushing code, check:

repo (for full control of private repos)

workflow (if needed for CI)

Copy the token immediately — GitHub won't show it again.

2. Update the Git Remote URL to HTTPS
Check current remote:


git remote -v
If it's SSH (git@github.com:user/repo.git), switch it to HTTPS:

git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
Replace USERNAME and REPOSITORY with your actual GitHub details.

3. Push Using the Token
When you push:

git push -u origin main
You'll be prompted for a username and password:

Username: your GitHub username

Password: paste your token instead of your real GitHub password

💡 You can also use a credential manager to avoid entering it every time.

============================================================================

If you want to Switch from SSH to HTTPS with Token Authentication


🔁 1. Change the Remote URL from SSH to HTTPS
Check current remote:


git remote -v
If it shows something like:

origin  git@github.com:your-username/your-repo.git
Change it to HTTPS:

git remote set-url origin https://github.com/your-username/your-repo.git
Verify the change:

git remote -v
Now it should show:

origin  https://github.com/your-username/your-repo.git
🔐 2. Set Up Credential Helper to Store Your Token
Use Git’s credential helper to store your token securely:

git config --global credential.helper store
This will store credentials in plain text in ~/.git-credentials. If you prefer security, skip this and use a credential manager instead.

🔓 3. Push to Trigger Login Prompt
Now push:

git push -u origin main
Git will prompt you:

Username: your GitHub username

Password: your personal access token (paste it)

If you used credential.helper store, Git will save this token for future use.
===============================================================
