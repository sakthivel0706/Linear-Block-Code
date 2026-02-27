# NAME : SAKTHIVEL E
# REG NO : 212224060230
# EXP NO : 6
# Linear-Block-Code
### AIM
To perform Linear Block Code operation for the specified input.

### TOOLS REQUIRED
Python: A versatile programming language used for scientific computing and signal processing.
NumPy: A powerful numerical library in Python for performing array-based operations and mathematical computations.
Matplotlib: A plotting library for generating high-quality graphs and visualizations of data, essentialfor demonstrating the sampling process.

### PROGRAM:
```
import numpy as np

pb = []
col = int(input("Enter the Parity bits : "))      # n-k
row = int(input("Enter the Message bits : "))     # k

# -----------------------------
# Construct Parity Matrix P
# -----------------------------
for i in range(row):
    p = list(map(int, input(f"Enter row {i+1} (space separated) : ").split()))
    pb.append(p)

P = np.array(pb, dtype=int)

# -----------------------------
# Generator Matrix G = [P | I]
# -----------------------------
I_k = np.eye(row, dtype=int)
G = np.hstack((P, I_k))

print("\nGenerator Matrix (G):")
for r in G:
    print(" ".join(map(str, r)))

# Code parameters
k = row
n = G.shape[1]

# -----------------------------
# Generate all possible messages
# -----------------------------
messages = np.array([[int(x) for x in format(i, f'0{k}b')] for i in range(2**k)])

# Generate codewords
codewords = np.mod(np.dot(messages, G), 2)

print("\nMessage   Codeword   Weight")
weights = []

for i in range(len(messages)):
    wt = np.sum(codewords[i])
    weights.append(wt)
    print(" ".join(map(str, messages[i])), "   ",
          " ".join(map(str, codewords[i])), "   ", wt)

# Minimum Hamming distance
d_min = np.min([w for w in weights if w != 0])
print("\nMinimum Hamming Distance:", d_min)

# -----------------------------
# Parity Check Matrix H = [I | P^T]
# -----------------------------
I_r = np.eye(col, dtype=int)
H = np.hstack((I_r, P.T))

print("\nParity Check Matrix (H):")
for r in H:
    print(" ".join(map(str, r)))

H_T = H.T

# -----------------------------
# Receive Codeword
# -----------------------------
rc = list(map(int, input("\nEnter the received codeword : ").split()))
r = np.array(rc)

# Syndrome
S = np.mod(np.dot(r, H_T), 2)

print("Syndrome :", " ".join(map(str, S)))

# -----------------------------
# Error Detection & Correction
# -----------------------------
error = np.zeros(n, dtype=int)

for i in range(n):
    if np.array_equal(H_T[i], S):
        error[i] = 1
        break

print("Error Vector :", " ".join(map(str, error)))

# Corrected codeword
corrected = np.mod(r + error, 2)
print("Corrected Codeword :", " ".join(map(str, corrected)))
```
### OUTPUT:
<img width="805" height="679" alt="image" src="https://github.com/user-attachments/assets/402b4d66-16ff-41e3-83e7-f11c4c497c14" />


### RESULT:
Thus linear block code operation for the given input is successfully verified.
