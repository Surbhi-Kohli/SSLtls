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

Q.The sender is sending both "data" and "hash".  If someone in the middle wants to change the content, why can't he send the "modified data" and "modified hash" in the packet?  In this way they can modify right?
A.if we talk about general MD5 or SHA1 hashing algorithms then what you have written is true.It is very simple to re-generate hash after modification of data.
Such plain hashing algorithms are used for example for storage of the passwords in DBs.But for data integrity additional key is added to the hashing process and without knowing this key it's not possible to generate correct hash for the modified data.

<img width="788" alt="Screenshot 2023-06-16 at 10 13 42 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/37f3bdb1-4947-4c48-b052-8aefa4f9d730">
## MD5
MD5 creates fixed length hash of 128 bit from any length of input data.It has many use cases.Again, a goal of the hash algorithm is to create one way hash and other sites may perform the same actions or take input data, create hash and compare it to hashes.And if hashes match, then data was not mutated, was not changed.

For example, hashing is often used for password storage, password that was enteredby user somewhere in any application or on any website may be stored not as a plain text password instead as hash.And each time when user enters its password, website or application creates a hash again and compares that hash with a hash that are stored in database.And if there is a match, we can be sure that the user has entered password correctly.

## MD5 algo in action
Open terminal and create a file .Then generate md5 hash for that file.  
<img width="483" alt="Screenshot 2023-06-16 at 10 34 50 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/519200a8-37df-4907-b3af-86cb3f113dfa">
You see that `md5 file1.txt` will generate a hash for the file.
If we open the file and add some text within and regenerate hash, we see that a different hash is generated.

<img width="1008" alt="Screenshot 2023-06-16 at 10 38 09 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/dc5b4bbc-8ec2-4fd1-89ea-11d80a601366">
Hence we see that the hash function within mac generates hash based on content of file.
Bothe the hashes are of 128bits.What we see here are hexadecimal numbers.Each hexadecimal number is 4 bits long.The generated hash has 32 hexa chars and hence 128 bits.

## SHA hashing algo:
The sha algo has different versions eg SHA-1(160 bits hash) , SHA-256, SHA-512.Most popular is SHA-256 which generates a hash of 256 bits.

SHA in action
<img width="575" alt="Screenshot 2023-06-16 at 10 51 23 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/a14f9879-f9c4-4990-89bc-f9e6fd155bbd">
The above generates a 160 bits long or 40 hex chars.
To generate hash of 256 bits, we use `shasum -a 256`
<img width="557" alt="Screenshot 2023-06-16 at 10 54 57 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/3bdb5a51-0d51-4be4-8757-27f1a812f14f">
We get hash with longer length.
We can also try with `shasum -a 500 <file name>`
Also keep in mind that each time the contents of file are changed, the generated hash will be different.

## HMAC algorithm:
HMAC algo may be used standalone but it is usually used in combination with either md5 or sha algo.The main purpose of this algo is adding special secret key into hashing process.And it means that with HMAC algorithm, we take not just input data.We also take a special secret key or password and utilize it during the creation of the hash.

For HMAC, Data+ secret key ==> hash
And with HMAC algorithm, we create hash that is based not just on data but also on secret password.And that means that the other side may create same has only if it has same secret key.And therefore this algorithm adds additional level of security and it also allows us to perform authentication of the sender.

RSA is assymetric encryption 
