# Crackme0x02 WriteUp


On the provided VM,  I:

  - navigated to the /tmp folder like so:

  -     cd /tmp
  - navigated into the challenge folder within tmp :

  -     cd /challenges
  - Then ran the crackme0x02 executable :

  -     ./crackme0x02


At this point:
  - I found a prompt asking for a password. Hmm? How will we find this?
  - So I backed out of the running exe by hitting control-C
  - I am going to use a new tool called radare 2

        r2  crackme0x02

  - Then dump the assembly (specifically the main function)

        pdf @ main
  - I found that in the assembly for main there seems to be an user input being compared to the password

        cmp eax, dword [ebp - local_ch]
        jne 0x8048461
        mov dword [esp], str.Password_OK_:__n ;

We can see from this ^^^ that eax register value and the value at [ebp - local_ch] must match .. The matched values is our password!


Reading through the assembly... This is where the real "hacking" is!

         1. mov dword [ebp - local_8h], 0x5a ; 'Z'
         2. mov dword [ebp - local_ch], 0x1ec
         3. mov edx, dword [ebp - local_ch]
         4. lea eax, [ebp - local_8h]
         5. add dword [eax], edx
         6. mov eax, dword [ebp - local_8h]
         7. imul eax, dword [ebp - local_8h]
         8. mov dword [ebp - local_ch], eax
         9. mov eax, dword [ebp - local_4h]
         10. cmp eax, dword [ebp - local_ch]
         11. jne 0x8048461
         12. mov dword [esp], str.Password_OK_:__n



First, since all the "dword"s indicate that the password will be a number, I want to know what the decimal values for 0x5a (line 1) and 0x1ec (line 2) are.

    ? 0x5a
and

    ? 0x1ec

You end up getting the values 90 for 0x5a and 492 for 0x1ec.

As you logically step your way further down the assembly, you find that:
   - 90 and 492 are added
   - and that sum is multiplied by itself
   - The result is 338724 , and that value is stored inside [ebp - local_ch]
###### Meaning that is your password!





I went back into the executable:

   - By typing

            ./crackme0x02
    - And then typed

    -       338724


# Voila!
