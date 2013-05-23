openssh
=======
Pimp your ssh with all the awesome madpimpery included with OpenSSH 6.2 that can't be had with the older version included with OS X (even 10.8), without getting your nice OS X keychain/ssh-agent integration pimp slapped into pimplivion.

In all seriousness though, newer versions of OpenSSL add Elliptical Curve Cryptography, and OpenSSH adds a new pubkey type - ECDSA.  This just patches OpenSSH 6.2's ssh-agent so you can store and retreive ECDSA keys in your OS X Keychain automagically just like you currently can do with DSA and RSA keys. 

If you are here, you probably already know why you want ECDSA support, but if not, in brief:
•ECDSA key pairs take much less CPU power than RSA keypair generation.  Give that 25MHz ARM box some love.
•ECDSA keys can be much smaller, a 521-bit ECDSA key equals a 4096-bit RSA Key
•ECDSA keys are slow at signing, so they are best used for things like SSH authentication.


To use, simply do:

brew tap metacollin/openssh

brew install openssh-keychain 

once this completes, do:

sudo nano /System/Library/LaunchAgents/org.openbsd.ssh-agent.plist    

locate the line (line 9 for me) that reads:

<string>/usr/bin/ssh-agent</string>

and change it so it reads:

<string>/usr/local/bin/ssh-agent</string>

Save, launch a new terminal session, and you should be good to go.  You might need to logout and log back in, but it just worked for me. 
