# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC
### Muthulakshmi D - 212223040122
## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:
```
MAC_SIZE = 32  # MAC size in bytes

def compute_mac(key: str, message: str) -> bytes:
    key_bytes = key.encode()
    msg_bytes = message.encode()
    mac = bytearray(MAC_SIZE)

    for i in range(MAC_SIZE):
        mac[i] = key_bytes[i % len(key_bytes)] ^ msg_bytes[i % len(msg_bytes)]
    return bytes(mac)

# Step 1: Input key and message
key = input("Enter the secret key: ")
message = input("Enter the message: ")

# Step 2: Compute MAC
mac = compute_mac(key, message)

# Step 3: Display MAC in hexadecimal
hex_mac = mac.hex()
print("Computed MAC (in hex):", hex_mac)

# Step 4: Input received MAC in hex (as string)
received_hex = input("Enter the received MAC (as hex): ")

# Convert received MAC hex string to bytes
try:
    received_mac = bytes.fromhex(received_hex)
except ValueError:
    print("Invalid hex input.")
    exit()

# Step 5: Verify MAC
if received_mac == mac:
    print("MAC verification successful. Message is authentic.")
else:
    print("MAC verification failed. Message is not authentic.")
```
## Output:

![image](https://github.com/user-attachments/assets/704fcb53-30f5-4199-b6c4-09010a5d9e74)


## Result:
The program is executed successfully.
