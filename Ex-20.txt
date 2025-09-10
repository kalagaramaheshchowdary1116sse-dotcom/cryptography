import hashlib

# Simple RSA (reuse code from Program 16)
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a

def multiplicative_inverse(e, phi):
    d = 0
    x1, x2, y1 = 0, 1, 1
    temp_phi = phi
    while e > 0:
        temp1, temp2 = divmod(temp_phi, e)
        temp_phi, e = e, temp2
        x, y = x2 - temp1 * x1, d - temp1 * y1
        x2, x1, d, y1 = x1, x, y1, y
    if temp_phi == 1:
        return d + phi

def generate_keypair(p, q):
    n = p * q
    phi = (p-1)*(q-1)
    e = 65537
    while gcd(e, phi) != 1:
        e += 2
    d = multiplicative_inverse(e, phi)
    return ((e,n),(d,n))

def sign(message, private_key):
    d, n = private_key
    h = int(hashlib.sha256(message.encode()).hexdigest(), 16)
    return pow(h, d, n)

def verify(message, signature, public_key):
    e, n = public_key
    h = int(hashlib.sha256(message.encode()).hexdigest(), 16)
    return h % n == pow(signature, e, n)

p, q = 61, 53
public, private = generate_keypair(p, q)

msg = input("Enter message: ")
signature = sign(msg, private)

print("Signature:", signature)
print("Verification:", "Valid" if verify(msg, signature, public) else "Invalid")
