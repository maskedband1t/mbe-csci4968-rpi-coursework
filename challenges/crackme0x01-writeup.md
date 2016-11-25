# Crackme0x01 WriteUp


On the provided VM,  I:

  - navigated to the /tmp folder like so:

  -     cd /tmp
  - navigated into the challenge folder within tmp :

  -     cd /challenges
  - Then ran the crackme0x01 executable :

  -     ./crackme0x01


At this point:
  - I found a prompt asking for a password. Hmm? How will we find this?
  - So I backed out of the running exe by hitting control-C
  - I dump the assembly code

        gobjdump -d crackme0x01

  - I then navigated to the main function and looked at its assembly
  - I found that in the assembly for main, there is a cmp function comparing an integer input vs. 0x149a

This is what we want, just not in hex, we want it in decimal.

         5274



I went back into the executable:

   - By typing

            ./crackme0x01
    - And then typed

    -       5274


# Voila!
