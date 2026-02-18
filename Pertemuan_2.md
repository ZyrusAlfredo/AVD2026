# PERTEMUAN 2
**Load dataset menggunakan Pandas, EDA & Data Understanding**

## 🎯 Tujuan Pembelajaran

Setelah mengikuti pertemuan ini, mahasiswa diharapkan mampu:

1. ✅ Dapat memuat dataset menggunakan Pandas
2. ✅ Dapat melakukan tahap Data Understanding
3. ✅ Dapat mengeksplorasi data (EDA)

## BAGIAN 1: Load Dataset menggunakan Pandas.
(Anda dapat membaca penjelasan lebih detail pada PPT/Modul yang sudah disiapkan praktisi di Classroom)

### MEMBACA DATASET
```
pd.read_csv('file.csv') → Membaca data dari file CSV
pd.read_excel('file.xlsx') → Membaca data dari file Excel
pd.read_sql() → Membaca data dari database SQL
pd.read_json('file.json') → Membaca data dari file JSON
```

### MENYIMPAN DATASET
```
df.to_csv() → Menyimpan data dalam format CSV
df.to_excel() → Menyimpan data dalam format Excel
df.to_sql() → Menyimpan data ke database SQL
```

!! Kasih tau untuk load dataset dengan format lain seperti .xlsx !!


### PENGECEKAN STRUKTUR DATA
```
df.head(n) → Menampilkan n baris pertama (default 5 row jika tidak diisi jumlah n)
df.tail(n) → Menampilkan n baris terakhir
df.info() → Menampilkan ringkasan dataset, termasuk jumlah baris, kolom, dan tipe data
df.shape → Mengembalikan jumlah baris dan kolom dalam dataset (baris, kolom)
df.dtypes → Menampilkan tipe data dari setiap kolom
```

### STATISTIK DESKRIPTIF
```
df.describe() → Menampilkan statistik ringkasan seperti mean, median, minimum, maksimum, dan kuartil
df.value_counts() → Menghitung jumlah kemunculan nilai unik dalam suatu kolom
df.mean(), df.median(), df.std() → Menghitung rata-rata, median, dan standar deviasi
df.corr() → Menghitung korelasi antar kolom numerik
```

## BAGIAN 2: EDA
(Anda dapat membaca penjelasan lebih detail pada PPT/Modul yang sudah disiapkan praktisi di Classroom)

### COMPARISON/PERBANDINGAN
```
variabel = df.groupby('Kolom 1')['Kolom 2'].sum().sort_values(ascending=False)

plt.figure(figsize=(10,6))
sns.barplot(x=variabel.index, y=keterangan.values, palette='wana', hue=variabel.index, legend=False)
plt.title('Judul')
plt.xlabel('Keterangan X')
plt.ylabel('Keterangan Y')
plt.xticks(rotation=45)
plt.show()
```

### COMPOSITION/KOMPOSISI
```
variabel = df.groupby('Kolom 1')['Kolom 2'].sum().sort_values(ascending=False)
variabe2 = variabel1.head(3)

plt.figure(figsize=(10, 8))
variabel2.plot(kind='pie', autopct='%1.1f%%', startangle=140, colors=plt.cm.Paired.colors)
plt.title('Judul')
plt.ylabel('')
plt.axis('equal')
plt.show()
```

### DISTRIBUTION/DISTRIBUSI
```
plt.figure(figsize=(10, 6))
sns.histplot(df['Kolom1'], bins=20, kde=True)
plt.title('Judul')
plt.xlabel('Keterangan X')
plt.ylabel('Keterangan Y')
plt.show()
```

### RELATIONSHIP/HUBUNGAN
```
plt.figure(figsize=(8, 6))
sns.heatmap(data=df[['Kolom1', 'Kolom2']].corr(),
            annot=True,
            cmap='warna',
            fmt='.2f')
plt.title('Judul')
plt.show()
```

## BAGIAN 3: DATA UNDERSTANDING
(Anda dapat membaca penjelasan lebih detail pada PPT/Modul yang sudah disiapkan praktisi di Classroom)

### CEK TIPE DATA KOLOM
```
df.dtypes
```

### CEK INCOSISTENT VALUES
```
print(df['Kolom'].unique())
```

### CEK MISSING VALUES
```
pd.DataFrame(df.isna().sum() / len(df) * 100, columns=['Null Ratio in %'])
```

### CEK DUPLICATED VALUES
```
df[df.duplicated()]
```

### CEK OUTLIERS VALUES
```
results = []

cols = df.select_dtypes(include=['float64', 'int64'])

for col in cols:
  q1 = df[col].quantile(0.25)
  q3 = df[col].quantile(0.75)
  iqr = q3 - q1
  lower_bound = q1 - 1.5*iqr
  upper_bound = q3 + 1.5*iqr
  outliers = df[(df[col] < lower_bound) | (df[col] > upper_bound)]
  percent_outliers = (len(outliers)/len(df))*100
  results.append({'Kolom': col, 'Persentase Outliers': percent_outliers})

# Dataframe dari list hasil
results_df = pd.DataFrame(results)
results_df.set_index('Kolom', inplace=True)
results_df = results_df.rename_axis(None, axis=0).rename_axis('Kolom', axis=1)

# Tampilkan dataframe
display(results_df)
```

### CEK OUTLIERS MENGGUNAKAN BOXPLOT
```
plt.figure(figsize=(8, 6))
sns.boxplot(y=df['Kolom'])
plt.title('Judul')
plt.ylabel('Keterangan Y')
plt.show()
```
