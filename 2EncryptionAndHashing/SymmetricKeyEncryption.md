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
 



RSA is assymetric encryption algo
