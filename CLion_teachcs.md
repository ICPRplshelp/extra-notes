# How to use CLion and teach.cs

> [!Warning]
> 
> This document is outdated! Please view [Using CLion with WSL](/CLion_WSL.md); the results you would get by doing that is way better than by using this document.

> [!NOTE]
> 
> This document tells you how to automatically sync files between your computer and that of a(n) SSH server *quickly*.


If you're using MacOS or WSL (hopefully), you'll notice that CLion gives you a lot of power when it comes to code checking. You can't get that when using VSCode. When you SSH using VSCode, you can't even get proper error checking, and setting that up is too much of a pain.

Windows will still give you reasonable power with this, but beware that the C you have with Windows may not be full-featured in comparison to teach.cs' Linux.

It's really hard to use SSH with CLion, so we'll not be doing that. Instead, I will configure CLion to constantly update any folder you want in teach.cs whenever you make a change to the project.

## Setup

You'll be importing a folder in teach.cs to CLion.

Create an empty CLion project. You want to be creating a C Executable, with the language standard set to as late as possible.

Then, go to `Tools > Deployment > Configurations`

Then, in connection, set up the SSH configuration and the root path:

- SSH configuration: set one up
	- The type should be SFTP
  - The host is `teach.cs.toronto.edu`
	- The username is your UTORID
	- Your password is your teach.cs password
	- The port is 22
- Your root path is what running `pwd` on teach.cs gives you. `pwd` stands for present working directory, and it should be the "root" directory of your user folder. For example, mines looks like `/h/uX/cX/XX/UTORID/`, where `X` can be substituted with any number.

![Configuration 1](https://github.com/ICPRplshelp/extra-notes/assets/93059453/c6e3b18e-ef59-4337-8cd4-11de1283d775)


In mappings, set the deployment path to the folder you want to "work" on in teach.cs. If you want to work on an assignment, set your deployment path to your assignment folder, **not** the entire Markus repository.

![](https://github.com/ICPRplshelp/extra-notes/assets/93059453/94d77a49-422f-4ffd-a790-e4bf0d7aafb6)


Then, in Excluded Paths, click +, add local paths, and add the CMake debug folder there (it causes a mess).

After doing this, go to `Tools > Deployment > Options` and set

> Upload changed files automatically to the default server

to ALWAYS.

Then, to finally sync all files, in CLion, right click on your project folder (the outmost folder in the project), go to `deployment` and click `Download from <PROJECT>`. The files from teach.cs should now appear in your project.

![](https://github.com/ICPRplshelp/extra-notes/assets/93059453/dc4f8c89-8fee-4a00-9e0e-dc254d4e547a)


From that point onwards, any changes you make or new files you create in your project folder locally will also be reflected on the teach.cs servers. However, if you delete a file locally, the deletion will not be reflected on the teach.cs servers.

If you edit a file on the teach.cs servers, it may not be reflected on your CLion project. You should resync as possible by right clicking on your project, going to deployments, and clicking what looks like resync.

## CMake

CMake is like a Makefile. I have no idea how to make Makefile projects, so you need to edit `CMakeLists.txt` to make sure CLion knows which C files to properly lint.

In `CMakeLists.txt`, in `add_executable`, after the project name, add all `.c` files in your project that you want to link together (DO NOT ADD `.h` FILES). That's it. Reload the project. The `.c` file that contains the `main()` function will be the one that runs.
