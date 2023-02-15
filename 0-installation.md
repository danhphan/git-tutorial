---
layout: page
permalink: installation/
title: Installation and setup
---

To work with this tutorial, you're going to need a few things:

- **Git**, of course. Install this by going to the git homepage,
  [git-scm.com](http://git-scm.com).
  
- **A GitHub account**. Create an account by going to
  [github.com](https://github.com).
  
- **A text editor**. Try [Visual Studio Code](https://code.visualstudio.com/) (VS Code) or [Sublime Text](http://www.sublimetext.com) (both of which are multiplatform). 
  
  Configure them to be your default git editors by following the instructions on [this page](https://help.github.com/articles/associating-text-editors-with-git/).
  Note: programs like Microsoft Word or TextEdit are *not* valid text editors
  here because they don't produce plain text files, but rather more elaborate
  file formats that include text formatting information.
  
- **A graphical git client or browser**. This lets you visualize your git history more easily, and understand the concepts behind git better. For a
  full list of clients, see [here](http://git-scm.com/downloads/guis). On Mac,
  I recommend [Git Tower](https://www.git-tower.com), though it's not free. The cross-platform [SourceTree](https://www.sourcetreeapp.com/) is free and available on Windows and Mac. On Linux, try gitg or gitk.


## Git installation

  **Install Git on Windows:**

  1. Download the latest [Git for Windows installer](https://git-for-windows.github.io/).
  2. When you've successfully started the installer, you should see the Git Setup wizard screen. 
    Follow the Next and Finish prompts to complete the installation. 
  3. In your StartUp menu, search for "git bash" and open it. 
  4. Verify installation by typing `git --version` in the git bash window. You will see the installed git version like this: git version 2.33.0.

  <img src="https://jcutrer.com/wp-content/uploads/2018/01/launch_git_bash_start_menu.png" style="zoom:70%;align='center';" />

  **Install Git on Mac OS X:**

  1. Download the latest [Git for Mac installer](https://sourceforge.net/projects/git-osx-installer/files/).
  2. Follow the prompts to install Git.
  3. Open your Terminal app. 
  3. Verify installation by typing `git --version` in the terminal. You will see installed git version like this: git version 2.33.0.

  **Install Git on Linux:**

  1. Open terminal and run: `sudo apt install git-all` or `sudo yum install git`.
  2. Verify installation by typing `git --version` in the terminal. You will see the installed git version like this: git version 2.33.0.


## Create an account on Github

1. Open the [GitHub link](https://github.com) and sign-up using your email address.
   
2. Remember your email id and your unique GitHub username; we will be using them in git configuration.

## Git configuration

You also need to configure git so that it knows your full name and email address. 
Fire up a console/terminal, and type:

{% highlight console %}
$ git config --global user.name "Your Name"
$ git config --global user.email "Your.Name@email.com"
{% endhighlight %}

DO NOT copy the `$` for the command. 
Note that you need to replace "Your name" with your own information. 
Please use the same email address you used for your GitHub account.

For a more user-friendly text editor, we recommend [Visual Studio Code](https://code.visualstudio.com/) and you can associate it with Git by typing the following command in your terminal/git bash window:

{% highlight console %}
$ git config --global core.editor "code --wait"
{% endhighlight %}

The following command also lets you see a rudimentary graphic of your history
without needing a GUI git client:

{% highlight console %}
$ git config --global alias.lsd "log --graph --decorate --pretty=oneline --abbrev-commit --all"
{% endhighlight %}

Then you can get a nice history (when you have several commits later) *within your terminal* by typing:

{% highlight console %}
$ git lsd
{% endhighlight %}

## Setup SSH key

Now our git configuration is completed and we are ready to work with git. However, each time we want to push (upload) 
files to GitHub, we have to associate the local machine with our GitHub account. 

Setting up SSH key helps with authentication every time we want to push local commits to the web client GitHub. Please follow the instructions
[here](https://help.github.com/en/enterprise/2.17/user/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to create ssh-key and adding it to your GitHub account. We have briefly outlined the commands needed for this step below, and please refer to the link above for more detailed explanations. 

- Generating a new SSH key:

{% highlight console %}
$ ssh-keygen -t rsa -b 4096 -C "Your.Name@email.com"
{% endhighlight %}

Press Enter three times (if you prefer to have another passphrase, type it twice). 

- Adding your SSH key to the ssh-agent:

{% highlight console %}
$ eval "$(ssh-agent -s)"
$ ssh-add -K ~/.ssh/id_rsa
{% endhighlight %}

- [Add the SSH key to your GitHub account:](https://docs.github.com/en/enterprise/2.17/user/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)

Copy the SSH key by printing it and copy the output of the command:

{% highlight console %}
$ cat < ~/.ssh/id_rsa.pub
{% endhighlight %}

Go to your [GitHub Settings](https://github.com/settings/keys) and click `New SSH key`. Name your key and paste it in the `Key` field.

- Test the connection:

{% highlight console %}
$ ssh -T git@github.com
{% endhighlight %}

Verify that the fingerprint in the message you see matches the following message, then type `yes`:

`Hi username (Your GitHub username)! You've successfully authenticated, but GitHub does not
provide shell access.`


## Notes

When typing a passphrase, it might seem that the keyboard isn't working.
However, this is just a security feature (similar to the `*`s you might see
when typing a password on the web). Just go ahead and type the passphrase,
then repeat it as requested.


**For Windows users**: Windows does not have an ssh agent running in the
background by default. If you see the error:

{% highlight console %}
$ ssh-add ~/.ssh/id_rsa
Could not open a connection to your authentication agent.
{% endhighlight %}

you will need to use this command to start the ssh-agent:

{% highlight console %}
$ eval `ssh-agent -s`
{% endhighlight %}

(Be careful to use the proper backtick symbol, usually just above the "Tab"
key on most keyboards; NOT the single quote/apostrophe character.)

Then type:

{% highlight console %}
$ ssh-add ~/.ssh/id_rsa
{% endhighlight %}

(You might need to change the filename from `id_rsa` to whatever you used.)
See [this StackOverflow answer](http://stackoverflow.com/a/17848593) for more
info.

You need to keep the window on which you launched the ssh-agent open.


---

Whew! That's quite a lot of stuff! But I hope by the end of the tutorial you'll
find it all useful and worth getting! (Plus: free stuff!)
