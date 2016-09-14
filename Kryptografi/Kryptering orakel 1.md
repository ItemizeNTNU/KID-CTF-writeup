##Krypterings orakel 1

We start by finding out how the encryption work. If we use a string of only a's we find that the encryption uses a ceaser cipher with a changing root for each letter of the string. We can also see that the rot starts at 1, then its 2, 4, 7, 11, 16, ... Which means that the index of the letter is added to the rot for each letter. Using this information we can write a simple python script to decrypt the string

```python
from codecs import encode

encrypted_string = "dvj{nHUsei_bBgvvy_cjBzy}"
unencrypted_string = ""
rot = 1
alpha1, alpha2 = "abcdefghijklmnopqrstuvwxyz", "ABCDEFGHIJKLMNOPQRSTUVWXYZ"

for index,letter in enumerate(encrypted_string):
	rot = (rot + index)%26
	if letter in alpha1:
		unencrypted_string += alpha1[(alpha1.index(letter) - rot)%26]
	elif letter in alpha2:
		unencrypted_string += alpha2[(alpha2.index(letter) - rot)%26]
	else:
		unencrypted_string += letter

print(unencrypted_string)
```

By running the code we get the flag ctf{cRYpto_mAster_maYbe}
