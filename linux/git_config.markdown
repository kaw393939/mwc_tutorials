Signing up for a new GitHub account
GitHub offers free accounts for users and organizations working on open source projects and paid accounts for users and organizations who need private repositories.

Tip: You do not need a paid user account to access and work on repositories from your organization. You only need a free user account to work on your organization's private repositories.
Signing up for service


Signup and Pricing buttonSelect Signup and Pricing from the top of the GitHub homepage.

Select the appropriate account type and level that you want to create. If you want more information about account types, you can read about the difference between a user and an organization account.

For a free user account, select Create a free account.

For a paid user account, select Create an account.

For a paid organization plan, select Create an organization.

Enter the requested information

Username
Email Address
Password
Confirm Password

Credit Card Number
Expiration
Postal Code
Select Create an Account
Tip: Your password must contain one lowercase letter, one number, and be at least 7 characters long.
Username

First you need to tell git your name, so that it can properly label the commits you make.

git config --global user.name "Your Name Here"
# Sets the default name for git to use when you commit
Email


Git saves your email address into the commits you make. We use the email address to associate your commits with your GitHub account.

    git config --global user.email "your_email@example.com"
# Sets the default email for git to use when you commit
Your email address for Git should be the same one associated with your GitHub account. If it is not, see this guide for help adding additional emails to your GitHub account. If you want to keep your email address hidden, this guide may be useful to you.

Overriding settings in individual repos
Password caching

The last option we need to set will tell git that you don't want to type your username and password every time you talk to a remote server.

Tip: You need git 1.7.10 or newer to use the credential helper
To use this option, you need install a credential helper.

GitHub for Windows includes this helper, and provides a git shell so you don't need to install and configure git manually.

If you don't want to use GitHub for Windows, you can download the helper for your OS here:

Windows Vista, 7, & 8 (.NET 4.0 required)
Source
Unzip the file and run the git-credential-winstore.exe program inside. This will start up the helper and update your git config to use it.

Tip: The credential helper only works when you clone an HTTPS repository URL. If you use the SSH repository URL instead, SSH keys are used for authentication. This guide offers help generating and using an SSH key pair.
Celebrate

Congratulations, you now have Git and GitHub all set up! What do you want to do next?
