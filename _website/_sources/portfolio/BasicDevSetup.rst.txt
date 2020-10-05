.. meta::
    :title:

###########################################################################################################################################
Set up Basic *REDACTED* Developer Environment                                                                                                   
###########################################################################################################################################


In this document, learn how to clone from and prepare to push code to *REDACTED* code repositories. Install Arcanist, Bazel, Git to contribute to the *REDACTED* development process.Be sure to join the **REDACTED** Google group as well.
Find instructions on how to:

-  Install required software
-  Add SSH Public key to Phabricator
-  Clone *REDACTED* code repositories
-  Prepare to push to *REDACTED* code repositories

To complete the setup properly, follow the instructions in each section.Ensure that you complete each section before moving on to the next one:

-   Install required software
-   Install Arcanist
-   Generate an SSH key pair
-   Setup Phabricator
-   Update Git user information
-   Clone the *REDACTED* mono repo
-   Prepare to push to *REDACTED* code repositories

.. note:: 

   If you are not on-site and connected to the *REDACTED* intranet, you will need to 
   `connect to the VPN <>`__ in order to access some systems, such as staging servers or the code repository.

Install Required Software
=============================


1. Open a terminal window and install Homebrew.

   .. code:: bash

       /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

   Click through any prompts that may appear.

2. Change Homebrew directory ownership.

   .. code:: bash

       sudo chown -h -R $(whoami) /usr/local/


3. Use Homebrew to install additional dependencies.

   .. code:: bash
    
        brew install coreutils git git-lfs python@3.7 awscli terraform gawk gnu-sed wget curl bazel jq

   .. note:: For development in any language at *REDACTED*, please refer to the language specific guide for installing the toolchain that will work with our codebase. 
             There may be additional steps required.

   Now you are ready to install Arcanist.

Install Arcanist
================

Arcanist provides:

-  Command line tools to allow access to many Phabricator tools like Differential, Files, and Paste.
-  Integrates with static analysis ("lint") and unit tests.
-  Manages common workflows like getting changes into Differential for review.

For more information see https://secure.phabricator.com/book/phabricator/article/arcanist/

1. Create a directory named *tools* to for Arcanist.

   .. code:: bash

       mkdir ~/tools

       cd ~/tools

       git clone https://github.com/phacility/arcanist.git

  These tools are required to push code to *REDACTED* code repositories.

2. Update your path to include Arcanist

   .. code:: bash

       echo 'export PATH="$PATH:$HOME/tools/arcanist/bin/"' >> ~/.bashrc

       echo 'export PATH="$PATH:$HOME/tools/arcanist/bin/"' >> ~/.zshrc

   .. note:: 
   
       A previous version of these instructions used .bash_profile and .zprofile instead of the current files.

Generate a SSH Key Pair
=========================


If you already have an SSH key pair,
continue on to `Phabricator Setup`__ section.
If you do not have an existing SSH key pair, follow the instructions below:

1. Run ``ssh-keygen`` in terminal to generate a key pair.

   Respond to each question by pressing **Enter**.
   You will be prompted to create a password, this is optional.
   Creating a password means you will need to enter it for each connection.
   You are not required to enter a password.

   **Example**: The following is an example of the output from ssh-keygen.

   .. code:: bash
   
       $ ssh-keygen

       Generating public/private rsa key pair.
       Enter file in which to save the key (/Users/fdetal/.ssh/id_rsa):
       Enter passphrase (empty for no passphrase):

       Enter same passphrase again:

       Your identification has been saved in id_rsa
       Your public key has been saved in id_rsa.pub

       The key fingerprint is:
       SHA256:0000000000000000000 fdetal@GB0000000

       The key's randomart image is:

       +---[RSA 3072]----+

       **REDACTED**  

       +----[SHA256]-----+

2. A key pair appears in the ~/.ssh folder.

   * The private key in *~/.ssh/id_rsa*.file
   * The public key in *~/.ssh/id_rsa.pub* file

   The same public key may be used on multiple hosts and services;
   you can re-use the same public key for other SSH connections.
   Set up Phabricator in the next section.

   .. important::

      Never share a private key.

Set up Phabricator
=====================

Once you have an SSH key pair,
you are now ready to upload your public key to Phabricator.

1. Go to https://phabricator.*REDACTED*.com/settings/.
   Click **SSH Public Keys** item on the left (**AUTHENTICATION** →  **SSH Public Keys** ).

2. Copy public key to your clipboard.
   Open a terminal and run:

   .. code:: bash

       pbcopy < ~/.ssh/id_rsa.pub

3. Go back to Phabricator and click **SSH Key Actions**  →  **Upload Public Key**.
   A window appears with fields for you to name the key paste the contents your clipboard.

4. Create a name for the key; the example key will use the name *id_rsa.pub*.

5. Paste the contents of ~/.ssh/id_rsa.pub into the Public Key field: Select the field and press **⌘** + **V** 
   to paste and click **Upload Public Key**.

Update Git user information
===========================

Configure Git settings to allow you clone and push changes to *REDACTED* code repositories.Git was installed earlier in this document using Homebrew.
Edit and use the following commands according to the comments on each line:

.. code:: bash
    git config --global user.email "USERNAME@*REDACTED*.com" # Replace USERNAME with the first part of your *REDACTED* email address.
    git config --global user.name "FULLNAME" # Replace FULLNAME with your full name.
    git config --global pull.rebase true # Configures git to use rebase instead of merge strategy by default when pulling.

**Example:** If your name is Fulano De Tal and email is fdetal@*REDACTED*.com,
  update your config like this:

  .. code:: bash

      $ git config --global user.email "fdetal@*REDACTED*.com"
      $ git config --global user.name "Fulano De Tal"
      $ git config --global pull.rebase true

Clone the *REDACTED* mono repo
================================


.. note:: 

   You will not be able to pull the repo if you're not `connected to the VPN <https://*REDACTED*.service-now.com/kb_view.do?sysparm_article=>`__.

From your home directory, Run the following commands:

.. code:: bash

    cd ~
    GIT_LFS_SKIP_SMUDGE=1 git clone --depth=1 --single-branch \\
    cd *REDACTED*
    git lfs install --skip-smudge --local

Prepare to Push Changes to *REDACTED* Code Repositories
=========================================================

Ensure that your ~/.zshrc is updated to include Arcanist in your path. 
Run ``echo 'export PATH="$PATH:$HOME/tools/arcanist/bin/"' >> ~/.zshrc``.

Set Default Editor for Arc and Git
==================================

Arc uses the editor ed by default.
This can be changed to your preferred editor.
Run the following commands but replace *PathToEditor* with the path to your preferred editor.

.. code:: bash

    arc set-config editor *PathToEditor*
    git config --global core.editor *PathToEditor*

**Example:** If your editor of choice is Vim installed via Homebrew, you would run the following:

.. code:: bash

    $ arc set-config editor /usr/local/Cellar/vim/8.2.0250_1/bin/vim
    $ git config --global core.editor /usr/local/Cellar/vim/8.2.0250_1/bin/vim

Install Arc Certificate
=========================

The first time you run ``arc diff`` or ``arc patch`` to push changes to *REDACTED* code repositories, 
arc may complain about verifying the centralized Phabricator server. 
If this occurs, Run ``arc install-certificate`` and follow the onscreen instructions; then run the command again.

Next Steps
==========


Now that you have completed this guide, 
you are now ready to submit code to *REDACTED* repositories with Arcanist. 
In addition, you are now ready to use many of the basic engineering resources. 
After completing this guide, find team-specific on-boarding information for further instruction:

**REACTED**
