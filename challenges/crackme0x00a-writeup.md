# Crackme0x00a WriteUp


First, I downloaded the VM provided on the RPI MBE site. The VM is of Ubuntu 14 and contains the stuff necessary for the course.

On the VM,  I:

  - navigated to the /tmp folder like so:

  -     cd /tmp
  - Then downloaded the challenge files by typing this :

  -     wget http://security.cs.rpi.edu/courses/binexp-spring2015/lectures/2/challenges.zip
  - After downloading, unzipped the files :

  -     unzip challenges.zip
  - navigated into the challenge folder within tmp :

  -     cd /challenges
  - Then ran the crackme0x00a executable :

  -     ./crackme0x00a


At this point:
  - I found a prompt asking for a password. Hmm? How will we find this?
  - So I backed out of the running exe by hitting control-C
  - Then hex dumped the file :

  -     xxd crackme0x00a

I then saw a hex dump side-by-side to a slightly more coherent version of the dump;

I navigated through and saw some oddities, including a couple key words worth attempting as a password.

I went back into the executable:

   - By typing

            ./crackme0x00a
    - And then typed

    -       g00dJ0B!


# Voila!




##### Alternative Way:

Doing everything the same until the hex dump as before:
    -You can type


        strings crackme0x00a

What this does, is to output every string in the dump greater than 4 characters, searching through this list, we can find our eventual password:

            g00dJ0B!
