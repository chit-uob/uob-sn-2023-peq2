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


# Checked by
If you find these answers correct, you can submit a pull request to add your name here, to add to the credibility of the answers.
- Chit

# Plug
If you find this helpful, please consider following my blog on [Chit's Programming Blog](https://blog.cpbprojects.me), where I post about my programming projects, and other things I find interesting.

You can also give this repository a star ⭐, so that more people can find it.
