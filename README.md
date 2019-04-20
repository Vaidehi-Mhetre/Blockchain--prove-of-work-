# Blockchain--prove-of-work-
Using the hash function defined below, “prove of work” is done as follows. Suppose the hash function is H() and your full name is NAME. This program finds a random string NONCE with 25 characters such that the output of H(NAME||NONCE) has at least 2 leading “a”, i.e., the output is aa ∗∗∗, where ∗ can be any character. The program also output the number of random strings tried. If your full name is less than 25 characters, then some spaces are used as padding.



A hash function is implemented as follows. The input of the hash function is English which include 26 letters and the space. So we will compute in Z27. The input text will be divided into blocks of 25 letters, the output will be 5 letters. Use an array OUT[5] to store the output. Initialize OUT[5] with all 0’s. 

The hash process include 3 rounds:

Round 1 

Write the 25 letters as a row-wise 5×5 block text and covert it to numbers.
For example, if the input is: “abcdefghi jklmnopqrstuvwx”, then we have
a b c d e 	0 1 2 3 4
f g h i 5 	6 7 8 26
j k l m n 	9 10 11 12 13
o p q r s 	14 15 16 17 18
t u v w x 	19 20 21 22 23

Add numbers in ith column in Z27 and plus the resulting number to OUT[i] to
update the value of OUT[i].

In this example, the updated value will be [20, 25, 3, 8, 3]. (e.g., 0 + 5 + 9 + 14 + 19 ≡ 20 (mod 27)).

Round 2 

Shift ith row left i times for i = 1, 2, 3, 4. Then add numbers in each column as in Round 1 and update OUT. For the above example, we have
b c d e a 	1 2 3 4 0
h i f g 	7 8 26 5 6
m n j k l	12 13 9 10 11
s o p q r 	18 14 15 16 17
t u v w x 	19 20 21 22 23

The sums of columns are: 3, 3, 20, 3, 3. So the updated OUT will be [23, 1, 23, 11, 6].

Round 3

Shift ith column down i times for i = 1, 2, 3, 4. Then add numbers in each row. The results are used to update OUT, i.e. the sum si of the ith row is used
to update OUT[i] (OUT[i] = OUT[i]+si). For the example, we have

t o j f a	 19 14 9 5 0
b u p k g 	1 20 15 10 6
h c v q l 	7 2 21 16 11
m i d w r 	12 8 3 22 17
s n e x 	18 13 26 4 23

The sums of rows are: 20, 25, 3, 8, 3. Now the updated OUT is [16, 26, 26,19, 9]
If we have more blocks, then the next block will go through the hash process and keep update the OUT until all the plaintext finished. The output of the hash function
is the final value stored in OUT which is changed back to letters. 

For the example, we only have one block. So the output will be “Q TJ” (16, 26, 26, 19, 9).
