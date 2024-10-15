# Crypto

enkripsi menggunakan Playfair Cipher dengan kunci "TEKNIK INFORMATIKA":

```python
# Fungsi untuk membuat matriks Playfair 5x5 berdasarkan kunci
def create_playfair_matrix(key):
    # Hilangkan huruf yang berulang dan anggap 'I' sama dengan 'J'
    key = "".join(sorted(set(key.replace('J', 'I')), key=lambda x: key.index(x)))
    
    # Isi matriks dengan huruf dari kunci dan sisa huruf alfabet
    alphabet = "ABCDEFGHIKLMNOPQRSTUVWXYZ"
    matrix = []
    used = set(key)
    
    for char in key:
        matrix.append(char)
    
    for char in alphabet:
        if char not in used:
            matrix.append(char)
    
    # Membuat matriks 5x5
    return [matrix[i:i+5] for i in range(0, len(matrix), 5)]

# Fungsi untuk mempersiapkan plaintext
def prepare_text(text):
    # Hilangkan spasi, atur huruf yang sama, dan buat pasangan
    text = text.replace("J", "I").replace(" ", "").upper()
    pairs = []
    i = 0
    while i < len(text):
        a = text[i]
        if i+1 < len(text):
            b = text[i+1]
            if a == b:
                pairs.append(a + 'X')
                i += 1
            else:
                pairs.append(a + b)
                i += 2
        else:
            pairs.append(a + 'X')
            i += 1
    return pairs

# Fungsi untuk menemukan posisi huruf di dalam matriks
def find_position(matrix, char):
    for row in range(5):
        for col in range(5):
            if matrix[row][col] == char:
                return row, col
    return None

# Fungsi untuk enkripsi pasangan huruf
def encrypt_pair(matrix, pair):
    row1, col1 = find_position(matrix, pair[0])
    row2, col2 = find_position(matrix, pair[1])
    
    if row1 == row2:
        return matrix[row1][(col1 + 1) % 5] + matrix[row2][(col2 + 1) % 5]
    elif col1 == col2:
        return matrix[(row1 + 1) % 5][col1] + matrix[(row2 + 1) % 5][col2]
    else:
        return matrix[row1][col2] + matrix[row2][col1]

# Fungsi utama untuk enkripsi Playfair Cipher
def encrypt_playfair(plaintext, key):
    matrix = create_playfair_matrix(key)
    pairs = prepare_text(plaintext)
    ciphertext = ""
    for pair in pairs:
        ciphertext += encrypt_pair(matrix, pair)
    return ciphertext

# Input kunci dan plaintext
key = "TEKNIK INFORMATIKA"
plaintext_1 = "GOOD BROOM SWEEP CLEAN"
plaintext_2 = "REDWOOD NATIONAL STATE PARK"
plaintext_3 = "JUNK FOOD AND HEALTH PROBLEMS"

# Gabungkan semua plaintext
combined_plaintext = plaintext_1 + " " + plaintext_2 + " " + plaintext_3

# Enkripsi untuk plaintext gabungan
encrypted_combined_text = encrypt_playfair(combined_plaintext, key)

# Cetak hasil enkripsi
print("Ciphertext:", encrypted_combined_text)
```

### Penjelasan Kode:
1. **create_playfair_matrix**: Membuat matriks Playfair 5x5 berdasarkan kunci yang diberikan, memastikan huruf tidak berulang dan menganggap `I` sebagai `J`.
2. **prepare_text**: Mempersiapkan teks untuk dienkripsi dengan menghilangkan spasi, memisahkan huruf berpasangan, dan menambahkan `X` jika diperlukan.
3. **find_position**: Menemukan posisi huruf dalam matriks.
4. **encrypt_pair**: Mengenkripsi sepasang huruf sesuai aturan Playfair Cipher.
5. **encrypt_playfair**: Fungsi utama yang memproses seluruh teks untuk dienkripsi.

### Hasil Enkripsi:
Setelah menjalankan kode, Anda akan mendapatkan ciphertext dari gabungan semua plaintext yang dienkripsi.

![image](https://github.com/user-attachments/assets/3c98bca6-1b7f-4f54-b43d-6b4a8702c5e9)
