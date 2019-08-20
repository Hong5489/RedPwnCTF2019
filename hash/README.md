# Super Hash
```
Written by: NotDeGhost

Does hashing something multiple times make it more secure? I sure hope so. I've hashed my secret ten times with md5! Hopefully this makes up for the fact that my secret is really short. Wrap the secret in flag{}.

Note: Follow the format of the provided hash exactly

Hash: CD04302CBBD2E0EB259F53FAC7C57EE2
```

Basically, we need to brute force the plaintext using the hash given

The encryption process looks like this:
```
Example :
plaintext = 'hello'

1st time
hello -> md5 -> 5D41402ABC4B2A76B9719D911017C592 
						|
2nd time                v
5D41402ABC4B2A76B9719D911017C592 -> md5 -> F872A18EB88181EB00816510E762FEE6
						|
						v
3rd time
...
...
...
						|
						v
10th time
Result: 2E03744900CDEFC1B3092BF4FCC954C0
```

Since it state the secret is **really short**, so i guess its only one character

I used python to solve this:
```python
import hashlib
import string
text = "CD04302CBBD2E0EB259F53FAC7C57EE2"

for character in string.printable:
	cipher = hashlib.md5(character).hexdigest().upper()
	for j in range(9):
		cipher = hashlib.md5(cipher).hexdigest().upper()
	if cipher == text:
		print character
```
Result:
```
^
[Finished in 0.1s]
```

That it! The flag is `flag{^}`