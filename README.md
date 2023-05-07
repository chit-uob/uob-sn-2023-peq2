# Speculated answer for Past Exam Questions 2 for Security and Networking 2023
link to questions: [https://canvas.bham.ac.uk/courses/65776/files/14535754](https://canvas.bham.ac.uk/courses/65776/files/14535754)

link to Questions 1: [https://github.com/chit-uob/uob-sn-2023-peq1](https://github.com/chit-uob/uob-sn-2023-peq1)

# DISCLAIMER
The following answer is **NOT** official. It is based solely on my understanding and interpretation of the lecture material. I am not responsible for any marks lost by following this answer.

In light of not having an official answer, I am hoping to make a collaborative effort to make a set of answer, to help students to better revise.

If you see any answer you don't agree on, please submit a [pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) to correct it, explaining why you think it is wrong. Or you can also contact me on Discord. Feel free to submit pull requests to improve the answers too.

## Question 1
### a)
Modern ciphers works on block of plain text instead of single symbols. A block cipher mode is a way to encrypt a sequence of blocks. The most simple way is to encrypt all blocks the same way, but then same blocks within the sequence will be encrypted into the same thing, making it easy to guess the content. Another block cipher mode is CBC, which using an initiation vector, and XOR the previous block with the current block before encrypting it. This way, even if the same block is encrypted, it will be encrypted into different things.

### b)
Yes, it is possible. Bob sends the same shared key to the broker using the broker's public key, as both the shared key and broker's public key doesn't change, the ciphertext is always the same. The second message is encrypted using the broker's public key, which is available for everyone. 

Therefore, if an attacker manages to encrypted messages, they can first send the ciphertext to the broker, when the broker decrypts it, the broker will see that it is Bob's shared key, then the attack can encrypt an instruction using the broker's public key and send it to the broker, and the broker will decrypt it and think that it is from Bob as the first message supposedly authenticated Bob.

### c)
Yes, it is possible to change the message can construct a matching signature. As AES counter mode is susceptible to known plain text attack, where if the attacker knows the plain text and the cipher text, they can modify the ciphertext to decrypt into something different. Also, El-Gamal is malleable, if you know the ciphertext for a given plaintext, you can construct a valid ciphertext for any other plaintext as well.

Therefore, the attacker can change the "Pay Tom 1000 pounds" to "Pay Bob 9999 pounds" using the known plain text attack, then reconstruct the El-Gamal ciphertext to match the new AES ciphertext.


## Question 2
### a)
A replay attack is an attack where the attacker intercepts a message, and retransmit it at a later time. Like if Alice sends Bob an encrypted text to pay Tom, although the attacker doesn't know the encryption key and hence can't encrypt messages themself, the attacker can simply replay the intercepted message, in which case Bob will receive the message, decrypt it, and think he needs to pay Tom again.

### b)
No, it is not safe to replace a nonce with a timestamp. A nonce is supposed to be a random number where the attacker have no chances to guessing. So if the other party can proof that they know the nonce you sent them, this adds to the authenticity of message. However, a timestamp is not random, and the attacker can easily guess it by reading the current time, and use it to verify themself.




# Checked by
If you find these answers correct, you can submit a pull request to add your name here, to add to the credibility of the answers.
- Chit

# Plug
If you find this helpful, please consider following my blog on [Chit's Programming Blog](https://blog.cpbprojects.me), where I post about my programming projects, and other things I find interesting.

You can also give this repository a star ⭐, so that more people can find it.
