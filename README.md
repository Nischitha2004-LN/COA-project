def alu_4bit(A, B, S):
    A = A & 0xF
    B = B & 0xF
    Cout = 0

    if S == 0:  # ADD
        res = A + B
        Cout = 1 if res > 15 else 0
    elif S == 1:  # SUB
        res = (A - B) & 0x1F
        Cout = 1 if A >= B else 0
    elif S == 2:  # AND
        res = A & B
    elif S == 3:  # OR
        res = A | B
    elif S == 4:  # XOR
        res = A ^ B
    elif S == 5:  # SHL
        res = (A << 1) & 0x1F
    elif S == 6:  # SHR
        res = A >> 1
    elif S == 7:  # PASS A
        res = A

    F = res & 0xF
    Z = 1 if F == 0 else 0

    return F, Cout, Z


# Test Cases
tests = [
    (5, 3, 0),
    (5, 3, 1),
    (5, 3, 2),
    (5, 3, 5),
    (0, 0, 0)
]

for A, B, S in tests:
    F, C, Z = alu_4bit(A, B, S)
    print(f"A={A:04b}, B={B:04b}, S={S:03b} => F={F:04b}, C={C}, Z={Z}")
