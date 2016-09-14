##Krypterings orakel 2

We start by finding out how the encryption work. If we use a string of only a's we find that the encryption varies between three letters. We find the same if we use a string of only b's. Only this time the letters are one further down the alphabet than for a. It seems like three static rots are cycled. If we test the string ab, we find that we get the first letter from the string of only a's and the first from the string of only b's. So the step of the cycle must be counted separately for each letter in the alphabet. Using this information we can write the following python script which finds all possible decryptions of the flag.

```python
encrypted_flag = "wnz{sIO_msAiS_wgUlX_qeCvY}"
unencrypted_flag = "ctf{"
rot1, rot2, rot3 = 20, 4, 12
used = {'c':1, 't':1, 'f':1}
alpha1, alpha2 = "abcdefghijklmnopqrstuvwxyz", "ABCDEFGHIJKLMNOPQRSTUVWXYZ"

for letter in "abdeghijklmnopqrsuvwxyz": used[letter] = 0

def reverse_rot(rot, letter):
	if letter in alpha1: return alpha1[(alpha1.index(letter) - rot)%26]
	elif letter in alpha2: return alpha2[(alpha2.index(letter) - rot)%26]
	return letter	

def addSolveR(d, letter, unencrypted_flag, index, r):
	letter_lower = letter.lower()
	count_letter = d[letter_lower]
	if (count_letter % 3) == r:
		q = dict(d)
		q[letter_lower] += 1
		solveR(q, index + 1, unencrypted_flag + letter)

def solveR(d, index, unencrypted_flag):
	for index2 in range(index, len(encrypted_flag)):
		letter = encrypted_flag[index2]
		if letter in "{_}": 
			unencrypted_flag += letter
			continue
		r1,r2,r3 = reverse_rot(rot1, letter), reverse_rot(rot2, letter), reverse_rot(rot3, letter)
		addSolveR(d, r1, unencrypted_flag, index2, 0)
		addSolveR(d, r2, unencrypted_flag, index2, 1)
		addSolveR(d, r3, unencrypted_flag, index2, 2)
		break
	if len(unencrypted_flag) == len(encrypted_flag):
		print(unencrypted_flag)

if __name__ == "__main__":
	solveR(dict(used), 4, unencrypted_flag)
```

By running the code we get a bunch of potential flags, as the encryption is not one-to-one. Only one flag seems to be right, that is the flag ctf{yOU_soOoO_smArT_maYbE}
