> Now we are going to take our first step into the world of programming, for this we'll start from learning the `C` programming language.
> It was one of the first few high-level programming language built that has stood the test of time and is used worldwide in more ways than you can probably imagine.
> Most of think that `C` is a language of the past but without it, you won't be having or enjoying a lot of electronics/gadgets you own now. A vast majority of them run on the `UNIX` or `linux` based systems which we're built in this language, a lot of modern day programming languages like `java`, `python` won't be existing without it, a lot of other languages have taken inspiration from the `C` language for their own syntax whether directly visible or not and a lot more things that I won't be able to fit here.
> 
> Henceforth, I want to conclude by saying that please take the `C` programming language seriously, as it is very essential for people interested and enthusiastic about the field of computer science.

And after this lengthy introduction, I won't deny if you are feeling bored, but without further ado, let's dive into it.

---
## Prerequisites

First I'll present you with some prerequisites you'll need to fulfill:
- You need to have a code editor installed on your system, like for example: [Visual Studio Code](http://code.visualstudio.com) along with extensions support and your config as you need it to function.
- We'll be following the **==GNU/GCC==** standard of `C-language` so the compilers like **==Turbo-C==**, **==DevC/DevC++==**, **==MinGW==** etc might give different results, so have that installed along with some other useful tools **==(make sure of an internet connection)==**.
	- Linux users: you probably don't need me to tell you but anyway, just run the command below in the terminal
		1. `sudo apt install gcc g++ make gdb git libboost-all-dev`
	- Mac users: just run the following commands, and yes they are safe to run, and yes you need to open the terminal (_not everything is clickity-clackity_)
		1. `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
		2. `sudo brew install gcc --force-bottle`
		3. `sudo brew install gdb make git`
		4. Finally check which version of `gcc` is installed on your system by running `which gcc-vv` where `vv` denoted the version number like `10, 11, 12, 13`. You'll get the result for the version installed on your system.
		5. We simply want the `gcc` command not some version number attached to it right, so now we are going to create an alternate name for it by running these commands(order does not matter and don't forget to replace the `vv` with the version of `gcc`):
			- `echo alias gcc='gcc-vv' >> ~/.bashrc`
			- `echo alias g++='g++-vv' >> ~/.bashrc`
			- `echo alias gcc='gcc-vv' >> ~/.zshrc`
			- `echo alias g++='g++-vv' >> ~/.zshrc`
	- Windows Users: You are the most troublesome bunch, cause Microsoft had to go and do it's own thing which is blatant blasphemy. But here you go:
		1. Download and install (just keep the default settings and click next) `git` command line tool from [here](https://git-scm.com/download/win) according to the config your system. (Setup not Portable)
		2. Now we're going for the most messed process for installing the `GNU's` `gcc` compiler, so please bear with it.
		3. Go to [cygwin](http://cygwin.com) homepage and download the installer based on your system config.
		4. Now run the installer and follow this guide:
			1. Select `Install from Internet` option and click `Next` 4 times.
			2. Now after waiting for some time you'll be presented with a list of some `URLs` (these are the locations all over the internet where the tools we need are stored), you can select any one of them but in my personal opinion the `URL`: `https://cygwin.mirror.constant.com` works good. And after selection click next.
			3. Now the installer will fetch the list of tools on that server, and after this you'll see a weird window.
			4. Now select the `Full` view next to the category drop-down.
			5. Finally we need to select the packages we need which are (use the search box above and match exact names, to select the package if skipped, just double click on `Skip` next to the package name):
				`class:multi-col-list`
				
				- `gcc-core`
				- `gcc-g++`
				- `gcc-fortran`
				- `gcc-objc`
				- `gcc-objc++`
				- `gdb`
				- `automake`
				- `cmake`
				- `imake`
				- `make`
				- `nano`
				- `curl`
				- `libcurl-devel`
				- `libboost-devel`
				- `bash-completion`
			6. Now just click on next and install buttons u
		- Finally add the location `C:\cygwin64\bin` or `C:\cygwin\bin` (as per your install) to the system `PATH` variable. (Search the internet for editing the `PATH` variable in windows)
- Now just restart your system for it to digest all the new things we've setup on it. (Not necessary but helpful in some cases)
- With all the necessary tools installed, now we'll start writing our first `c-program` which will just be a `hello` program.
---

## The Hello Program

Now follow these steps:
1. Open your code editor which we installed earlier
2. Create a new file and name it `hello.c`
3. Write the code below into it and save it.
	```c
	#include<stdio.h>
	
	int main()
	{
		printf("Hello\n");
		return 0;
	}
	```
	> [!tldr] There will be a lot of things here you won't understand at first but the journey is worth the wait 	

4. Time to compile the code and run it. For this step we need the command line and we need to do this:
	1. In the command line navigate to the folder where you've saved the `hello.c` file using. (refer internet)
	2. Now that you are in that folder run `gcc hello.c` and this'll generate an executable for you to run usually with the name of `a.out` or `a.exe` based on the operating system.
	3. To run it, use the below command:
		- Mac/Linux: `./a.out`
		- Windows: `.\a.exe`
	4. Then you'll see the word `Hello` written on the terminal.

---

 > [!info] And this will be the standard procedure we'll follow through.

Now let's see what's going on in the code we just wrote above:

1. Line 1: `#include<stdio.h>`, this picks up the `stdio.h` file (containing the functions for input output) and copy it's content in our code (well the compiler does).
2. Line 3: `int main()`, this is the declaration of the `main()` function which is by standards the entry point for code in most languages, i.e. for where the execution of out program starts. Note that we have written `int` before `main()` denoting that when executed we'll receive an integer value from it. (the reason is that this helps us identify how the program executed, like any error or such thing)
3. Line 4: `{`, an opening curly bracket, denoting that the scope or let's say bound of the main function starts from here, can also be written in `Line 3`.
4. Line 5: `printf("Hello\n");`, we are calling the `printf` function which is defined in the `stdio.h` file responsible for output and telling it to print `Hello\n` by enclosing it in double quotes (`"`) and the `\n` is a special way of telling to get to a new line while writing something, just like how we press the `Enter`/`Return` key on our keyboards while typing.
5. Line 6: `return 0;`, as we mentioned earlier that main returns an integer value and `0` is something we all can agree on is the most basic number, hence returning it denotes that the code executed successfully without any errors, as all errors have their own specific error codes with a meaning attached to them.
6. Line 7: `}`, the closing curly bracket, denoting the we are ending the scope of the main function here.

> In this short snippet of code we saw many different things happening, like copying of a whole file without doing it, we wrote a basic function for entry and called another function inside it to print something and finally returned something from that function.
>
> There is a lot more yet to come and we'll see how all these things work and more.