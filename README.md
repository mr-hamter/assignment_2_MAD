import math

MOD1 = 9999
MOD2 = 999

#Câu 1.1
def a_n(n):
    return pow(3, n, MOD1)

# phần tử thứ k của S_n
def kth_string_Sn(n, k):
    A = ['a', 'b', 'c']
    s = ""
    for i in range(n):
        s = A[k % 3] + s
        k //= 3
    return s

#Câu 1.2
def b_n(n):
    return pow(3, (n + 1) // 2, MOD1)
#biến chuoi : chuỗi, lưu lại biến nhận được ví dụ (a,b,c)
#chuoi_day_du : chuỗi đầy đủ sau khi nhận xong chuỗi sẽ nhận vào biến từ sau khi hoàn thành thì cho danh sách restore nhận
#res : restore nhận chuỗi đầy đủ  
def palindromes_n(n):
    A = ['a', 'b', 'c']
    half = (n + 1) // 2
    res = []
    total = 3 ** half
    for num in range(total):
        chuoi = ""
        k = num
        for _ in range(half):
            chuoi += A[k % 3]
            k //= 3
        if n % 2 == 0:
            chuoi_day_du = chuoi + chuoi[::-1] # đảo ngược chuỗi
        else:
            chuoi_day_du = chuoi + chuoi[-2::-1] #[bắt đầu, kết thúc, bước nhảy]
        res.append(chuoi_day_du)
    return sorted(res) 

#Câu 1.3
def cijk(i, j, k):
    n = i + j + k
    num = math.comb(n, i) * math.comb(n - i, j)
    return num % MOD1

#Câu 1.4
def d_n(n):
    d = [0]*(n+2)
    d[1] = 3
    d[2] = 8
    for i in range(3, n+1):
        d[i] = (2*d[i-1] + 2*d[i-2]) % MOD1
    return d[n]

#Câu 1.5
def e_n(n):
    e = [0]*(n+2)
    e[1] = 3
    e[2] = 8
    for i in range(3, n+1):
        e[i] = (3*e[i-1] - e[i-2]) % MOD2
    return e[n]

#Câu 2
def ab_seq(n):
    a, b = 1, 0
    for _ in range(n):
        a, b = (3*a - 7*b), (3*b - a)
    return (a, b)

def q2_result(n):
    a, b = ab_seq(n)
    return (a + b) % MOD2

print("a_1000 mod 9999 =", a_n(1000))
print("100th of S10 =", kth_string_Sn(10, 99))
print("b_1000 mod 9999 =", b_n(1000))
print("c(100,90,80) mod 9999 =", cijk(100,90,80))
print("d_1000 mod 9999 =", d_n(1000))
print("e_1000 mod 999 =", e_n(1000))
print("(a1000 + b1000) mod 999 =", q2_result(1000))

p10 = palindromes_n(10)
print("100th palindrome in P10 =", p10[99])
