import random

# Diffie-Hellman simulation
P = 23
G = 5

alice_private = random.randint(1, P-1)
bob_private = random.randint(1, P-1)

alice_public = pow(G, alice_private, P)
bob_public = pow(G, bob_private, P)

shared_alice = pow(bob_public, alice_private, P)
shared_bob = pow(alice_public, bob_private, P)

print("Alice Public:", alice_public)
print("Bob Public:", bob_public)
print("Shared Secret (Alice):", shared_alice)
print("Shared Secret (Bob):", shared_bob)

session_key = hashlib.sha256(str(shared_alice).encode()).hexdigest()
print("Derived Session Key:", session_key)
