
Ammon Harps
NetID: ah695

## Self-Attack


| Item           | Result                                                                                                                                                                                                                                                                                     |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Date           | April 15, 2025                                                                                                                                                                                                                                                                             |
| Target         | pizza.listentotalks.click                                                                                                                                                                                                                                                                  |
| Classification | Injection                                                                                                                                                                                                                                                                                  |
| Severity       | 1                                                                                                                                                                                                                                                                                          |
| Description    | Using SQL injection, I was able to update users that were not associated with the token I was using. Thus, I could set all passwords in the database (including admin ones) to a particular value, and gain administrator privileges while locking all other users out of the application. |
| Corrections    | I altered my database code to prevent SQL injections by replacing string concatenation with more secure methods of database access.                                                                                                                                                        |

| Item           | Result                                                                                                                                                                                                                   |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Date           | April 15, 2025                                                                                                                                                                                                           |
| Target         | pizza.listentotalks.click                                                                                                                                                                                                |
| Classification | Security Misconfiguration                                                                                                                                                                                                |
| Severity       | 2                                                                                                                                                                                                                        |
| Description    | Since many of the testing admin roles had not been removed from the database, I was able to brute force many of their simple passwords (e.g. "testing1", "testing2"). This allowed me to gain administrator privileges.  |
| Corrections    | I altered my code to require a certain level of password security (certain combination of chars, length, etc). Thus, no password should be able to be easily brute forced. Testing users were removed from the database. |

| Item           | Result                                                                                                                                                                                                                 |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Date           | April 15, 2025                                                                                                                                                                                                         |
| Target         | pizza.listentotalks.click                                                                                                                                                                                              |
| Classification | Cryptographic Failures                                                                                                                                                                                                 |
| Severity       | 3                                                                                                                                                                                                                      |
| Description    | The outgoing requests for orders is editable from chrome dev tools, which allows the values to be changed. This means that I was able to order pizzas for free or change other values before the server receives them. |
| Corrections    | Some possible corrections would be to encrypt the price and value of the pizza in transit and decrypt it on the server so that it cannot be changed while in transit or on the client side.                            |

## Peer Attack

After the in-class demo that wiped all of our production databases due to a dependency on the malicious npm package created by Prof Jensen, my prod database was erased. I was unable to restore it properly. I restored from a snapshot in AWS, but then had a lot of trouble connecting everything properly again. Unfortunately this process took significantly longer than I had hoped, to the point that there was no longer time in the evening for a peer to review my code and try to attack it. 

Thus, although I was able to attack my production locally, I wasn't able to complete the peer part of this assignment, though I wanted to. I sent a message to Stephen over Discord but I think it was too late by that point. Please let me know if there is any way for me to make this up.

## Summary of Learnings

I've learned quite a few things from this experience, namely:
- I need to be on the defensive when I code. It's been really interesting to view the JWT-Pizza code from a completely different angle, and with more malicious intent. It's easy to define the path a user is supposed to take through my application, but it's a lot harder to predict every possible combination of inputs that could cause unwanted behavior.
- Injection attacks are powerful and easy to forget about! It's been really interesting to me to see just how easy it can be to exploit even just a simple mistake in input sanitation.
- Layers, layers, layers! The more security layers and hoops the attacker has to jump through, the less likely they'll be able to extract any relevant information before they are detected. Information is everything, and if I can slow them down, I can get the upper hand.
- Don't trust code from other people! If I don't know where something came from, I need to apply some "stranger danger." Unfortunately, I learned this the very hard way, and likely at the cost of half of my points on this assignment.

This experience has taught me a lot! And honestly, it's mostly been from trial by fire (especially from my database being wiped which prevented me from having a functional production environment to give to a peer!). DevOps is hugely interesting to me and I love it, even if I'm not the best at it yet. I hope to continue to learn more and put these concepts and technologies into practice in my personal projects and professional career!
