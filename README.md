# EX.NO:3 
# HILL CIPHER
```
NAME:NARENDHARAN.M 
REG.NO:212223230134
```
 
## AIM: To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
import numpy as np

# Convert text to numbers
def text_to_numbers(text):
    return [ord(char) - ord('A') for char in text]

# Convert numbers to text
def numbers_to_text(numbers):
    return ''.join(chr(num + ord('A')) for num in numbers)

# Encrypt message
def encrypt(plain_text, key_matrix):
    n = len(key_matrix)
    plain_text = plain_text.upper().replace(" ", "")

    # Padding if needed
    while len(plain_text) % n != 0:
        plain_text += 'X'  
    
    numbers = text_to_numbers(plain_text)
    encrypted_numbers = []
    
    # Apply matrix multiplication
    for i in range(0, len(numbers), n):
        block = np.array(numbers[i:i+n]).reshape(n, 1)
        encrypted_block = np.dot(key_matrix, block) % 26
        encrypted_numbers.extend(encrypted_block.flatten().tolist())

    return numbers_to_text(encrypted_numbers)

# Decrypt message
def decrypt(cipher_text, key_matrix):
    n = len(key_matrix)
    numbers = text_to_numbers(cipher_text)

    # Compute modular inverse of the key matrix
    det = int(round(np.linalg.det(key_matrix)))  # Determinant
    det_inv = pow(det, -1, 26)  # Modular inverse
    
    adjugate = np.round(det * np.linalg.inv(key_matrix)).astype(int) % 26
    key_inv = (det_inv * adjugate) % 26

    decrypted_numbers = []
    
    for i in range(0, len(numbers), n):
        block = np.array(numbers[i:i+n]).reshape(n, 1)
        decrypted_block = np.dot(key_inv, block) % 26
        decrypted_numbers.extend(decrypted_block.flatten().tolist())

    return numbers_to_text(decrypted_numbers)

# Get user input
plaintext = input("Enter the plaintext (only letters): ").upper().replace(" ", "")
size = int(input("Enter the size of the key matrix (e.g., 2 for 2x2, 3 for 3x3): "))

# Get the key matrix from user
key_matrix = []
print(f"Enter the {size}x{size} key matrix row by row (only integers):")
for i in range(size):
    row = list(map(int, input().split()))
    key_matrix.append(row)

key_matrix = np.array(key_matrix)

# Encrypt and decrypt
ciphertext = encrypt(plaintext, key_matrix)
decrypted_text = decrypt(ciphertext, key_matrix)

print("\nPlaintext:", plaintext)
print("Ciphertext:", ciphertext)
print("Decrypted Text:", decrypted_text)
## OUTPUT
![WhatsApp Image 2025-03-27 at 09 02 38_a07b4e9d](https://github.com/user-attachments/assets/878508d9-b64c-43f0-92da-38a320ebaa8b)

## RESULT
thus we did hill cipher
