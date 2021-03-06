# logcat-colorize

A simple program that colorizes Android Debug Bridge (adb)'s logcat output on a terminal window.

*Notes*:

  - supports output formats: brief, tag, process, time or threadtime (see more about this in the official [docs][1]);
  - works on Linux (haven't tested on other platforms);

![image][2]

I would also recommend: [Android Bash Completion][4]


# Installation

## PPA (for Ubuntu-ers)

I created a DEB package and placed in my personal launchpad repository, for Ubuntu (and alike) convenience:

        $ sudo add-apt-repository -y ppa:bruno-braga/logcat-colorize
        $ sudo apt-get update
        $ sudo apt-get install -y logcat-colorize

*Note*: from quantal (12.10) and newer versions only (older versions might require some tackle in the C++ code).


## DIY (from sources)

This depends on:

  * libboost-regex
  * libboost-program-options

If you are on Debian/Ubuntu:
    
        $ sudo apt-get install -y build-essential libboost-regex-dev libboost-program-options-dev

If you are on Mac OS X (using macports with libs installed in /opt/local):

        $ sudo port install boost

Compile and install:

        # download (or clone) the source
        $ make
        $ sudo make install

# Usage

        # Help and version info:
        $ logcat-colorize
        
        # Simplest usage:
        $ adb logcat | logcat-colorize
        
        # Using specific device, with time details, and filtering:
        $ adb -s emulator-5556 logcat -v time System.err:V *:S | logcat-colorize
        
        # Piping to grep for regex filtering (much better than adb filter):
        $ adb logcat -v time | egrep -i '(sensor|wifi)' | logcat-colorize


That's it!


**Note**: I had written this as a quick approach in bash, but turns out it is pretty slow, specially pulling logcat from new devices (really a lot). So I decided to go a bit lower level and re-wrote this in C++. For reference, if you want to see the bash version, check out the [tag 0.2][3].


[1]: http://developer.android.com/tools/debugging/debugging-log.html#outputFormat
[2]: https://bitbucket.org/brunobraga/logcat-colorize/downloads/example.jpg
[3]: https://bitbucket.org/brunobraga/logcat-colorize/src/8a17155d0d7c29c19130695d7a699e83830456ce?at=0.2
[4]: https://github.com/mbrubeck/android-completion
