def affine_encrypt(text, a, b):
    result = ""
    for char in text.upper():
        if char.isalpha():
            result += chr(((a * (ord(char) - 65) + b) % 26) + 65)
        else:
            result += char
    return result

def affine_decrypt(cipher, a, b):
    result = ""
    a_inv = pow(a, -1, 26)
    for char in cipher:
        if char.isalpha():
            result += chr(((a_inv * ((ord(char) - 65) - b)) % 26) + 65)
        else:
            result += char
    return result

msg = input("Enter plaintext: ")
a = int(input("Enter a (must be coprime with 26): "))
b = int(input("Enter b: "))

enc = affine_encrypt(msg, a, b)
print("Encrypted:", enc)
print("Decrypted:", affine_decrypt(enc, a, b))
