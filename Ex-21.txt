import hmac
import hashlib

def generate_mac(message, key):
    return hmac.new(key.encode(), message.encode(), hashlib.sha256).hexdigest()

message = input("Enter message: ")
key = input("Enter secret key: ")

mac = generate_mac(message, key)
print("Generated MAC:", mac)

# Verification
recv_mac = input("Re-enter MAC to verify: ")
if recv_mac == mac:
    print("MAC Verified: Message Authentic")
else:
    print("MAC Verification Failed!")
