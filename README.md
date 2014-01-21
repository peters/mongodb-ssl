# Mongodb with openssl support

Building mongodb with openssl support on Windows is not for the faint hearted. 
This short tutorial teaches you how to do it.

# Prebuilt binaries

You can download my prebuilt binaries from [Sourceforge](https://sourceforge.net/projects/mongodbssl/) if you want to get started quickly. Binaries for both x86 and x64 are available starting from mongo 2.4.9.

In order to run mongodb with ssl support on Windows Server 2008 R2 or newer the following prerequisites are required:

* Visual C++ 2008 Redistributables ([32bit](http://www.microsoft.com/downloads/details.aspx?familyid=9B2DA534-3E03-4391-8A4D-074B9F2BC1BF) / [64bit](http://www.microsoft.com/downloads/details.aspx?familyid=bd2a6171-e2d6-4230-b809-9a8d7548c1b6))
* Visual C++ 2010 Redistributables ([32bit](http://www.microsoft.com/en-us/download/details.aspx?id=8328) / [64bit](http://www.microsoft.com/en-us/download/details.aspx?id=13523))
* Openssl 1.0.1f ([32bit](http://slproweb.com/download/Win32OpenSSL-1_0_1f.exe) / [64bit](http://slproweb.com/download/Win64OpenSSL-1_0_1f.exe))

# Grabbing mongo sources

1. Create a new folder on your disk called `mongodb-ssl`
2. Download and extract [Winpcap 4.1.2 Developers pack](http://www.winpcap.org/devel.htm) into `mongodb-ssl\winpcap`
3. `git clone https://github.com/mongodb/mongo.git mongodb-ssl\mongo`
4. `cd mongodb-ssl\mongo` 
5. `git checkout r2.4.9`

# Downloading thirdparty dependencies

NB! You do not need a working Visual Studio 2010 CD-KEY after your trial expires because we are only interested in the compilers.

* [Visual Studio 2010 Professional (web installer)](http://stackoverflow.com/questions/8894654/vs-2010-trial-version-link)
* Visual C++ 2008 Redistributables ([32bit](http://www.microsoft.com/downloads/details.aspx?familyid=9B2DA534-3E03-4391-8A4D-074B9F2BC1BF) / [64bit](http://www.microsoft.com/downloads/details.aspx?familyid=bd2a6171-e2d6-4230-b809-9a8d7548c1b6))
* [Python 2.7](http://www.python.org/ftp/python/2.7.6/python-2.7.6.msi)
* [Python for Windows extensions](http://sourceforge.net/projects/pywin32/files/pywin32/Build%20218/pywin32-218.win32-py2.7.exe/download)
* [Scons 2.3.0](http://prdownloads.sourceforge.net/scons/scons-2.3.0-setup.exe)
* Openssl 1.0.1f ([32bit](http://slproweb.com/download/Win32OpenSSL-1_0_1f.exe) / [64bit](http://slproweb.com/download/Win64OpenSSL-1_0_1f.exe))

# 32-bit build

1. Modify `mongodb-ssl\mongo\SConstruct` at line 287 and add the following entry to `env = Environment(`:

    $ `MSVC_USE_SCRIPT = "C:\\Program Files (x86)\\Microsoft Visual Studio 10.0\\VC\\vcvarsall.bat",`

2. Run the following line in a Visual Studio 2010 command prompt

    $ `scons all -j 8 --release --32 --ssl --win2008plus --extrapath="C:\OpenSSL-Win32"`

3. You shall see unicorns in `mongodb-ssl\mongo\build\win32\32\extrapath_C__OpenSSL-Win32\release\ssl\mongo` folder.

# 64-bit build

1. Modify `mongodb-ssl\mongo\SConstruct` at line 287 and add the following entry to `env = Environment(`:

    $ `MSVC_USE_SCRIPT = "C:\\Program Files (x86)\\Microsoft Visual Studio 10.0\\VC\\bin\\amd64\\vcvars64.bat",`

2. Run the following line in a Visual Studio 2010 command prompt

    $ `scons all -j 8 --release --64 --ssl --win2008plus --extrapath="C:\OpenSSL-Win64"`
    
3. You shall see unicorns in `mongodb-ssl\mongo\build\win32\64\extrapath_C__OpenSSL-Win64\release\ssl\mongo` folder.
