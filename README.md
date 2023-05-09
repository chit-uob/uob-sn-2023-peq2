# Speculated answer for Past Exam Questions 2 for Security and Networking 2023
link to questions: [https://canvas.bham.ac.uk/courses/65776/files/14535754](https://canvas.bham.ac.uk/courses/65776/files/14535754)

link to Questions 1: [https://github.com/chit-uob/uob-sn-2023-peq1](https://github.com/chit-uob/uob-sn-2023-peq1)

# DISCLAIMER
The following answer is **NOT** official. It is based solely on my understanding and interpretation of the lecture material. I am not responsible for any marks lost by following this answer.

In light of not having an official answer, I am hoping to make a collaborative effort to make a set of answer, to help students to better revise.

If you see any answer you don't agree on, please submit a [pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) to correct it, explaining why you think it is wrong. Or you can also contact me on Discord. Feel free to submit pull requests to improve the answers too.

## Question 1
### a)
Modern ciphers normally work on blocks of plain text instead of single symbols. A block cipher mode is a way to encrypt a sequence of blocks. The most simple way is to encrypt all blocks the same way, but then same blocks within the sequence will be encrypted into the same thing, making it easy to guess the content. Another block cipher mode is CBC, which uses an initiation vector, and performs an XOR on the previous block with the current block before encrypting it. This way, even if the same block is encrypted, it will be encrypted into different things. Block cipher modes vary in security and complexity, and have a variety of different applications.

### b)
Yes, it is possible. Bob sends the same shared key to the broker using the broker's public key, as both the shared key and broker's public key doesn't change, the ciphertext is always the same. The second message is encrypted using the broker's public key, which is available for everyone. 

Therefore, if an attacker manages to intercept the messages, they can replay that first message, when the broker decrypts it, the broker will see that it is Bob's shared key. Then the attacker can encrypt an instruction using the broker's public key and send it to the broker, and the broker will accept it as the replayed encrypted key is valid.

### c)
Yes, it is possible to change the message can construct a matching signature. As AES counter mode is susceptible to known plain text attack, where if the attacker knows the plain text and the cipher text, they can modify the ciphertext to decrypt into something different. Also, El-Gamal is malleable, if you know the ciphertext for a given plaintext, you can construct a valid ciphertext for any other plaintext as well.

Therefore, the attacker can change the "Pay Tom 1000 pounds" to "Pay Bob 9999 pounds" using the known plain text attack, then reconstruct the El-Gamal ciphertext to match the new AES ciphertext.


## Question 2
### a)
A replay attack is an attack where the attacker intercepts a message, and retransmit it at a later time. Like if Alice sends Bob an encrypted text to pay Tom, although the attacker doesn't know the encryption key and hence can't encrypt messages themself, the attacker can simply replay the intercepted message, in which case Bob will receive the message, decrypt it, and think he needs to pay Tom again.

### b)
No, it is not safe to replace a nonce with a timestamp. A nonce is supposed to be a random number, so an attacker cannot easily discover it. So if the other party can prove that they know the nonce you sent them, this adds to the authenticity of message. However, a timestamp is not random, and the attacker can easily guess it by reading the current time, and use it to verify themself. This reduces the security of the protocol greatly.

### c)
![1](http://github.com/chit-uob/uob-sn-2023-peq2/blob/main/img/1.png?raw=true)
It is possible to attack this protocol by using a replay attack, since for the same payment message, it will be signed with the same signature, and the encrypted message will be the same. Therefore, after the first protocol run. Eve can intercept the message from Bob to Alice, and replace the second part of the message with the intercepted message from the first protocol run. This means Eve can make all future messages "Pay Elvis £5".

//The question specifies that different protocol runs produce different payment messages. If this means that identical payment messages are refused, this attack would not work. However, as it just says "produce", the replay attack is assumedly still possible.

### d)
![2](http://github.com/chit-uob/uob-sn-2023-peq2/blob/main/img/2.png?raw=true)
From the NIST, key agreement is a key-establishment procedure where resultant keying material is a function of information contributed by two or more participants, so that no party can predetermine the value of the keying material independently of the other party’s contribution. In this protocol, it doesn't satisfy key agreement because the attacker can make it so that both parties end up with different keys, although the attacker cannot decrypt all future messages.

The attacker Eve can intercept the first message from Alice, and replace the message with one using her own nonce and signature. This will mean that Bob now thinks he is communicating with Eve. Then Bob will send to Eve his nonce encrypted with Eve's public key, which Eve then decrypts and sends to Alice encrypted with Alice's public key. Then Alice confirms to Bob that they know Bob's nonce, which Eve forwards to Bob. Then Alice has the key N_A N_B, but B has the key N_C N_B. Therefore, the attacker can make it so that both parties end up with different keys, thus not satisfying key agreement.


## Question 3
### a)
#### i)
--Top of stack frame--

password_buffer[0] (1 byte character)

... (14 character variables, one byte each)

password_buffer[15] (one byte, start of array)

authenticated (4 bytes for integer)

old EBP (4 byte pointer)

old EIP/return address (4 byte pointer)

*password (4 byte pointer)

--Bottom of stack frame--

#### ii)
The code is vulnerable to buffer overflow attack. Strcpy copies until a terminator, and doesn't check for length. This means at the stage of copying the content of password to password_buffer, a string of any length can be copied. That means any data longer than 16 bytes will overflow to the stack.

#### iii)
If the input password is 20 characters long, since the password_buffer is only 16 bytes long, the remaining 4 bytes will overflow to the next item on the stack, which is the authenticated integer variable which is 4 bytes long. Therefore, an attacker can overwrite the value of the integer authenticated.

### b)
#### i)
To circumvent the password check, we can craft a 20 bytes password, the first 16 bytes can all be the character 'a', then the last 4 bytes should contain the byte representation of the integer 1. Then the last 4 bytes will overflow to the authenticated integer, and change it to 1, which will pass the password check.

#### ii)
To achieve arbitrary code execution, we can craft a very long message, the first 24 bytes can be all 'a', then the next 4 bytes will be the return address of the function, so the attacker must either know the data layout (in which case they can put the exact return address of following attack code), or the attacker can guess a return address. Then the remaining data can be a NOP slide followed by the attack code. So when the program executes, after the check_authentication function is called, it will return to the new return address. If the attacker guessed the return address, they can bet on the return address pointing to some part of the NOP slide, which will then slide to the attack code.

### c)
The checks do not achieve the intended purpose because strcpy is executed before setting the last character to the null terminator. Therefore, the buffer will overflow before the null terminator is set. The change we need to make to the code is to 1) only copy 16 bytes of code from password, then 2) set the last byte of password_buffer to null terminator.

# Checked by
If you find these answers correct, you can submit a pull request to add your name here, to add to the credibility of the answers.
- Chit
- Tom
# Plug
If you find this helpful, please consider following my blog on [Chit's Programming Blog](https://blog.cpbprojects.me), where I post about my programming projects, and other things I find interesting.

You can also give this repository a star ⭐, so that more people can find it.
