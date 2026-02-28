# PERTEMUAN 3
**Data Preparation**

## 🎯 Tujuan Pembelajaran

Setelah mengikuti pertemuan ini, mahasiswa diharapkan mampu:

1. ✅ Dapat Mengetahui Metode Penanganan Data yang Bermasalah
2. ✅ Dapat Melakukan Analisis Terhadap Kolom yang Bermasalah
3. ✅ Dapat Melakukan Penanganan Data Dengan Metode yang Tepat

## BAGIAN 1: Penanganan Tipe Data
(Anda dapat membaca penjelasan lebih detail pada PPT/Modul yang sudah disiapkan praktisi di Classroom)

**!! UNTUK KOLOM YANG MAU DIUBAH TIPE DATA NYA (KE NUMERIK)** wajib menjalankan kode ini terlebih dahulu !!
```
df['nama_kolom'] = pd.to_numeric(df['nama_kolom'], errors='coerce')
```

**!! UNTUK KOLOM YANG MAU DIUBAH TIPE DATA NYA (KE OBJECT)** wajib menjalankan kode ini terlebih dahulu !!
```
df['nama_kolom'] = df['nama_kolom'].astype(str)
```

### Untuk mengubah ke Int64
```
df['nama_kolom'] = df['nama_kolom'].astype('Int64')
```

### Untuk mengubah ke Float64
```
df['nama_kolom'] = df['nama_kolom'].astype('Float64')
```

### Untuk mengubah ke Object
```
df['nama_kolom'] = df['nama_kolom'].astype('object')
```

## BAGIAN 2: Incosistent Values
(Anda dapat membaca penjelasan lebih detail pada PPT/Modul yang sudah disiapkan praktisi di Classroom)

### Untuk Kolom Date yang Bermasalah (Tipe Data & Incosistent Values)
```
df["Nama Kolom"] = pd.to_datetime(df["Nama Kolom"], format="mixed")
df["Nama Kolom"].head(5)
```

### Mapping (menangani kalimat/mengganti kalimat)
```
df['nama kolom'] = df['nama kolom'].replace({
    'Kalimat Salah': 'Kalimat Benar', 
    'Kalimat Salah': 'Kalimat Benar',
    'Kalimat Salah': 'Kalimat Benar',
    'Kalimat Salah': 'Kalimat Benar'
})

for col in ['nama kolom']:
    print(df[col].unique())
```

### Untuk Membuat Teks Upper (KAPITAL Semua) - HALO DUNIA
```
df['Nama Kolom'] = df['Nama Kolom'].str.upper()
print(df['Nama Kolom'].unique())
```

### Untuk Membuat Teks Lower (kecil Semua) - halo dunia
```
df['Nama Kolom'] = df['Nama Kolom'].str.lower()
print(df['Nama Kolom'].unique())
```

### Untuk Membuat Teks Kalimat Pertama yang Besar (Capitalize) - Halo dunia
```
df['Nama Kolom'] = df['Nama Kolom'].str.capitalize()
print(df['Nama Kolom'].unique())
```

### Untuk Membuat Huruf Pertama Setiap kata Besar (Title) - Halo Dunia
```
df['Nama Kolom'] = df['Nama Kolom'].str.title()
print(df['Nama Kolom'].unique())
```

## BAGIAN 3: Missing Values
(Anda dapat membaca penjelasan lebih detail pada PPT/Modul yang sudah disiapkan praktisi di Classroom)

### Untuk mengatasi missing values pada kolom tanggal

**a. Dihapus**
```
df = df.dropna(subset=['nama kolom'])
```

**b. Dengan Forwardwill (pakai tanggal sebelumnya)**
```
df['nama kolom'] = df['nama kolom'].fillna(method='ffill')
```

**c. Dengan Backward Fill (pakai tanggal setelahnya)**
```
df['nama kolom'] = df['nama kolom'].fillna(method='bfill')
```

**d. Mengisi berdasarkan kolom lain (jika ada kolom tanggal lagi di dataset mu, jadi kolom itu akan jadi acuan)**
```
df['nama kolom yang bermasalah'] = df['nama kolom yang bermasalah'].fillna(df['nama kolom yang akan dijadikan acuan'])
```

### Untuk Drop/Menghapus
```
df = df.drop('Nama Kolom', axis=1) // Hapus Kolom
```

```
df = df[df['nama kolom'] != 'Kalimat yang mau dihapus'] // Hapus Baris
```

### Untuk diimputasi
```
df['Nama Kolom'] = df['Nama Kolom'].fillna(df['Nama Kolom'].dropna().mean())
```
```
df['Nama Kolom'] = df['Nama Kolom'].fillna(df['Nama Kolom'].dropna().median())
```
```
df['Nama Kolom'] = df['Nama Kolom'].fillna(df['Nama Kolom'].dropna().mode()[0]) // Modus
```

## BAGIAN 4: Duplicated Values

### Untuk Drop/Menghapus
```
df = df.drop_duplicates()
```

## BAGIAN 5: Outliers
```
columns_to_impute = ["Nama Kolom 1", "Nama Kolom 2"]

for col in columns_to_impute:
    Q1 = df[col].quantile(0.25)
    Q3 = df[col].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR

    # Menggunakan .loc[] agar tidak muncul SettingWithCopyWarning
    df.loc[:, col] = df[col].clip(lower=lower_bound, upper=upper_bound)
```

## BAGIAN 6: Construct Data
(Disesuaikan dengan kebutuhan kalian) Disini saya mau mencontohkan untuk membuat kolom baru.
```
def VARIABEL(NAMA KOLOM RELEVAN):
    if profit > 0:
        return 'KETERANGAN'
    elif profit < 0:
        return 'KETERANGAN'
    else:
        return 'KETERANGAN'

df['NAMA KOLOM BARU'] = df['NAMA KOLOM RELEVAN'].apply(VARIABEL)
```

## BAGIAN 7: Data Reduction

**a. Untuk hapus kolom**
```
df = df.drop('Nama Kolom, axis=1)
```

**b. untuk menghapus baris**
```
df = df[df['nama kolom'] != 'Kalimat yang mau dihapus']
```
