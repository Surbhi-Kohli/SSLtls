Encryption is one of the essential applications of cryptography. It is used to make data incomprehensible to ensure confidentiality. It’s also widely used over the internet by using modern encryption technologies such as SSL/TLS

## Symmetric encryption

Symmetric encryption is the encryption method which involves one secret key to cipher and decipher the information. It’s one of the old techniques, which uses numbers, words, or strings of random alphabets as a secret key.The data is encrypted on one side using a special key and  then encrypted data is sent to another
side and that another side decrypts received data using the same key.
However, to encrypt and decrypt the message, the recipient must be aware of the secret key. 
Any person or any machine that owns this game has ability to decrypt encrypted data and gain access to original data.And that is a drawback of symmetric encryption.
If you want to use it somewhere for encryption of your data, you should take care of your key.The key should be kept secret and it should not be transferred to any URLs or machines or sent to other people.

Some examples of symmetric encryption algorithm are Blowfish, AES, DES,3DES RC4, RC5 and RC6 .DES and 3Des are obsolete.
For DES, the length of the key is just 56 bits.3DES is a modification of DEs that performs encrytion 3 times.But again, it is vulnerable to different kinds of attacks that give you access to original data. 

The most widely used modern symmetric encryption algorithms are AES-128, AES-192, and AES-256.AES= Advanced Encryption System.This algo allows you to use keys of different lengths.AES-128 algo has key length of 128 bits.AES is much more secure than DEs and 3DES.
AES is used in SSL communication via HTTPS protocol.


## Hashing Overview
Before we have discussed encryption algorithms and symmetric key encryption. Encryption is usually done for making data unreadable for third party.
And of course, this data that is encrypted, transferred over network could be easily changed, compromised or something like that.That will lead to a situation when the receiver will not be able to read original data or will read it with some errors.Thats where hashing comes into picture.  

What is a hash?  
Hash is a fixed length string(maybe 128 bit or 160 bit),And this length depends on the algorithm that is used to for creation of the hash. 

<img width="437" alt="Screenshot 2023-06-14 at 1 23 20 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/8fbcdd05-c3be-4afd-919a-3cad172a75a8">
 
Hash function takes inout data(which may be of any length).It gives out a fixed length hash based on the input.Hash function creates irreversible hash.This means that in case u have a hash and dont know the original data,it is not possible for u to generate input data from the hash.Thats because same hash might get created for unlimited different input.So we can create hash based on any data, but we are not able to retrieve data from the hash.


Another important characteristic of hash function is that each time when you slightly change input data,when you change even a single character or even single bit ,hash will be changed completely.Another characteristic of hash function is that generally they dont require any key for hash creation.But there are some hash functions that also use symmetric key into the hash .
What we accomplish using keys is following:We perform not just the integrity check on the receiver, we also perform authentication of sender.It means that if on the receiver  side we take data,key  to create hash and compare it with received hash and those hashes match, we can be sure that the hash that we have received was created by a party that owns same key as we do.But again, please notice that the keys are optional.


Why do we need hash and hash function??
Consider that you have data ,on which you apply hash function and you get a hash.Now you send   data + hash across the network to reciever.Now receiver takes data and applies same hash function on data and then compares the hash that it got with hash that it generated.And if those hashes match, it means for receiver that this data was not changed or was not mutated during transfer over network.Hash verifies integrity of data(what if data is changed and still same hash is generated?? loophole..doubt)
Also we should also be encripting the data and then create a hash of it.
Hash algorithms work in such a way that even small change of data will lead to creation of completely  different hash.

RSA is assymetric encryption algo
