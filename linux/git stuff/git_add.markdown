

Make a new repository on GitHub

Every time you make a commit with Git, it is stored in a repository (a.k.a. "repo"). To put your project up on GitHub, you'll need to have a GitHub repository for it to live in.

More about repositories
Click New Repository.

Click "New Repository

Fill out the information on this page. When you're done, click "Create Repository."

Fill in the info

Congratulations! You have successfully created your first repository!

Create a README for your repository

While a README isn't a required part of a GitHub repository, it is a very good idea to have one. READMEs are a great place to describe your project or add some documentation such as how to install or use your project. You might want to include contact information - if your project becomes popular people will want to help you out.

More about READMEs
Step 1: Create the README file

In the prompt, type the following code:

mkdir ~/Hello-World
# Creates a directory for your project called "Hello-World" in your user directory

cd ~/Hello-World
# Changes the current working directory to your newly created directory

git init
# Sets up the necessary Git files
# Initialized empty Git repository in /Users/you/Hello-World/.git/

touch README
# Creates a file called "README" in your Hello-World directory
Open the new README file found in your Hello-World directory in a text editor and add the text "Hello World!" When you are finished, save and close the file.

Step 2: Commit your README

Now that you have your README set up, it's time to commit it. A commit is essentially a snapshot of all the files in your project at a particular point in time. In the prompt, type the following code:

More about commits
git add README
# Stages your README file, adding it to the list of files to be committed

git commit -m 'first commit'
# Commits your files, adding the message "first commit"
Step 3: Push your commit

So far everything you've done has been in your local repository, meaning you still haven't done anything on GitHub yet. To connect your local repository to your GitHub account, you will need to set a remote for your repository and push your commits to it:

More about remotes
git remote add origin https://github.com/username/Hello-World.git
# Creates a remote named "origin" pointing at your GitHub repository

git push origin master
# Sends your commits in the "master" branch to GitHub
Now if you look at your repository on GitHub, you will see your README has been added to it.

Your README has been created

Celebrate

Congratulations! You have now created a repository on GitHub, created a README, committed it, and pushed it to GitHub. What do you want to do next?