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

### Untuk Drop/Menghapus
```
df = df.drop('Nama Kolom', axis=1)
```

### Untuk diimputasi
```
df['Nama Kolom'] = df['Nama Kolom'].fillna(df['Nama Kolom'].dropna().mean())
```

## Bagian 4: Duplicated Values

### Untuk Drop/Menghapus
```
df = df.drop_duplicates()
```

## Bagian 5: Outliers
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

## Bagian 6: Construct Data
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

## Bagian 7: Data Reduction
```
df = df.drop('Nama Kolom, axis=1)
```
