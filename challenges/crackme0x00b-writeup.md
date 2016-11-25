# Crackme0x00b WriteUp


On the provided VM,  I:

  - navigated to the /tmp folder like so:

  -     cd /tmp
  - navigated into the challenge folder within tmp :

  -     cd /challenges
  - Then ran the crackme0x00b executable :

  -     ./crackme0x00b


At this point:
  - I found a prompt asking for a password. Hmm? How will we find this?
  - So I backed out of the running exe by hitting control-C
  - Then I searched for all strings greater than 4 characters

        strings crackme0x00b

  - None of the strings returned were sufficient passwords, maybe the password appears in a non-conventional way...
  - But I do not know how to use the "strings" keyword to search specifically yet..
  - So I then ended the "strings" command and hex dumped the file :

  -     xxd crackme0x00b

I then saw about the same things I saw in the "strings" search...

Except there was a group of characters spaced out but yet together that seemed like the right password.

         w...0...w...g...r...e...a...t.

Spaced out over a few spaces so that "strings" would not catch it?

I went back into the executable:

   - By typing

            ./crackme0x00b
    - And then typed

    -       w0wgreat


# Voila!
