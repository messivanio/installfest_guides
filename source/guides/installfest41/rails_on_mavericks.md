# Getting starts on Mavericks

Unfortunately OS X Mavericks isn't supported by Rails Installer. This means we
need to do a slightly more "professional" installation of Ruby and of Rails.
Here's the basic outline:

1. Setup a compiler
2. Install [homebrew](http://brew.sh)
3. Use homebrew to install [ruby-install](https://github.com/postmodern/ruby-install) and [chruby](https://github.com/postmodern/chruby)
4. Use ruby-install to install a new version of the Ruby programming language
5. Use Ruby to install Rails

## Setting up a compiler

In Mavericks this process has been streamlined by Apple fairly significantly.

1. Open the Terminal application. You can do this by pressing Command+Space (to open Spotlight) then typing "terminal" in the search window which appears.
2. In the Terminal type: `xcode-select --install` or alternatively `gcc` and press enter. A popup will appear which will install the command-line compilation tools.
3. You may receive a warning like: "_You have not agreed to the Xcode license agreements, please run 'xcodebuild -license'_". If so, simply run: `sudo xcodebuild -license` and enter your account password then follow the steps.
4. Once that has finished try typing `gcc -v` into your terminal window. You should see a message like:

```sh
Configured with: --prefix=/Applications/Xcode.app/Contents/Developer/usr
Apple LLVM version 5.0 (clang-500.2.79) (based on LLVM 3.3svn)
Target: x86_64-apple-darwin13.0.0
Thread model: posix
```

If so, congratulations you've installed the compilation tools. You can move
onto the next section!

## Installing homebrew

[Homebrew](http://brew.sh) is a tool which developers use to install other bits
of software. Using homebrew we can easily install things like the Postgres
database tool, or even tools which lets us install other tools.

Installing homebrew is easy. In your terminal window run:

```
ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go/install)"
```

Once that is complete you can run `brew -v` on the terminal to check that it
has installed properly.

## Installing ruby-install and chruby

ruby-install is a tool which can install multiple versions of the Ruby
programming language.  Professional Ruby developers will use ruby-install (or
    similar tools) so they can test their applications with many different
versions of Ruby.

chruby is a tool which can be used to manage and switch between different
installed versions of Ruby.

Run all the the following step by step:

1. First install openssl: `brew install openssl`
2. Next install ruby-install: `brew install ruby-install`
3. Now use ruby-install to install Ruby: `ruby-install ruby 2.0.0`

Installing Ruby may take a little while. Next we'll install and configure
chruby:

```
brew install chruby
echo "source '/usr/local/share/chruby/chruby.sh'" >> ~/.bash_profile
source '/usr/local/share/chruby/chruby.sh'
echo "chruby `chruby | grep 2.0.0 | sed 's/\* //'`" >> ~/.bash_profile
chruby `chruby | grep 2.0.0 | sed 's/\* //'`
```

This set of commands may seem overwhelming, but all we're doing is:

1. Installing chruby with homebrew
2. Configuring chruby to start when you open your terminal.
3. Starting chruby in your current terminal.
4. Telling chruby to use the latest version of ruby when your start your terminal.
5. Telling chruby to use the latest version of ruby in your current terminal.

Assuming that all worked properly you can run:

```sh
ruby -v
```

and you should see something like:

```sh
ruby 2.0.0p247 (2013-06-27 revision 41674) [x86_64-darwin13.0.0]
```

Importantly you should NOT see:

```sh
ruby 2.0.0p247 (2013-06-27 revision 41674) [universal.x86_64-darwin13]
```

The word __universal__ means that it's the version of Ruby which comes with OS
X.  We don't want to use this.

If your Ruby is installed properly you can move onto the next section.

## Installing Rails

Installing Rails is easy just run:

```sh
gem install rails -v 4.1.1
```

If you want to install the latest version of Rails (4.1.1 at time of writing)
  just type

```sh
gem install rails
```

If you install multiple versions of Rails onto your computer you can choose
which one to create an app with as follows:

```sh
rails _3.2.13_ new quick_blog
rails _4.0.1_ new quick_blog_4
```

If you just type

```sh
rails new quick_blog_again
```

it will automatically use the latest version of Rails you have installed.

Congratulations on installing Rails. You should probably [get cracking with the
rest of the guide now!](/guides/installfest41/getting_started)


