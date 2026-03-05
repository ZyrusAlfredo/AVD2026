# PERTEMUAN 4
**MATPLOTLIB & SEABORN**

## 🎯 Tujuan Pembelajaran

Setelah mengikuti pertemuan ini, mahasiswa diharapkan mampu:

1. ✅ Dapat Membaca & Mengetahui Jenis-Jenis Visualisasi
2. ✅ Dapat Mengetahui Apa itu Matplotlib & Seaborn serta Perbedaannya
3. ✅ Dapat Membuat Visualisasi pada Google Colab

# BAR CHART (MATPLOTLIB)
```
VARIABEL = df['KOLOM'].value_counts().head(5).sort_values(ascending=False) # head() jumlah yang mau ditampilkan & Urutan

plt.figure(figsize=(10, 6)) # Ukuran
plt.bar(VARIABEL.index, VARIABEL.values, color='skyblue') # color warna
plt.xlabel('X') # keterangan X label
plt.ylabel('Y') # keterangan y label
plt.title('JUDUL') # Judul
plt.xticks(rotation=45, ha='right') # rotasi teks
plt.tight_layout()
plt.show()
```

# BAR CHART (SEABORN)
```
VARIABEL1 = df['KOLOM 1'].value_counts().head(5).sort_values(ascending=False) # head() jumlah yang mau ditampilkan & Urutan
VARIABEL2 = df[df['KOLOM 1'].isin(VARIABEL1.index)]

plt.figure(figsize=(10, 6)) # Ukuran
sns.countplot(x='KOLOM 1', data=VARIABEL2, hue="KETERANGAN KOTAK KECIL", palette='pastel', order=VARIABEL1.index) # palette (warna)
plt.title('JUDUL') # Judul
plt.xlabel('X') # Keterangan X
plt.ylabel('Y') # Keterangan Y
plt.xticks(rotation=45)
plt.show()
```

# PIE CHART (MATPLOTLIB) (HANYA 1 KOLOM)
```
plt.figure(figsize=(10, 6)) # ukuran
plt.pie(df['KOLOM 1'].value_counts(), labels=df['KOLOM 1'].value_counts().index, autopct='%1.1f%%', colors=['lightcoral', 'lightblue', 'lightgreen', 'gold']) # colors (warna)
plt.title('JUDUL') # Judul
plt.show()
```

# PIE CHART (MATPLOTLIB) (BERDASARKAN KOLOM LAIN)
```
VARIABEL1 = df.groupby('KOLOM 1')['KOLOM 2'].sum().sort_values(ascending=False)
VARIABEL2 = VARIABEL1.head(3)

plt.figure(figsize=(10, 8)) # Ukuran
VARIABEL2.plot(kind='pie', autopct='%1.1f%%', startangle=140, colors=plt.cm.Paired.colors) 
plt.title('JUDUL') # Judul
plt.ylabel('') # Keterangan Y
plt.axis('equal')
plt.show()
```

# LINE CHART (MATPLOTLIB) BERDASARKAN BULAN
```
# Pastikan kolom bertipe datetime

# Group by month
VARIABEL1 = df.groupby(df['KOLOM 1'].dt.to_period('M')).size()

plt.figure(figsize=(20, 6)) # Ukuran figure diperbesar untuk kejelasan
plt.plot(VARIABEL1.index.astype(str), VARIABEL1.values, marker='o', color='blue') # Mengubah warna agar berbeda
plt.title('JUDUL', fontsize=16) # Judul
plt.xlabel('X', fontsize=12) # X Keterangan
plt.ylabel('Y', fontsize=12) # Y Keterangan
plt.grid(True)
plt.gcf().autofmt_xdate() # Otomatis mengatur format dan rotasi di sumbu X
plt.tight_layout()
plt.show()
```

# LINE CHART (MATPLOTLIB) BERDASARKAN TAHUN
```
# Pastikan kolom bertipe datetime
df['KOLOM 1'] = pd.to_datetime(df['KOLOM 1'])

# Group by day
VARIABEL1 = df.groupby('KOLOM 1').size()

plt.figure(figsize=(20, 6)) # Ukuran figure diperbesar untuk kejelasan
plt.plot(VARIABEL1.index, VARIABEL1.values, marker='o', color='red') # Mengubah warna agar berbeda
plt.title('JUDUL', fontsize=16) # Judul
plt.xlabel('X', fontsize=12) # X Keterangan
plt.ylabel('Y', fontsize=12) # Y Keterangan
plt.grid(True)
plt.gcf().autofmt_xdate() # Otomatis mengatur format dan rotasi di sumbu X
plt.tight_layout()
plt.show()
```

# HISTOGRAM (MATPLOTLIB)
```
plt.figure(figsize=(8, 5))
plt.hist(df['KOLOM'], bins=20, color='blue', edgecolor='black')
plt.title('JUDUL')
plt.xlabel('X')
plt.ylabel('Y')
plt.show()
```

# HISTOGRAM (SEABORN)
```
plt.figure(figsize=(8, 5))
sns.histplot(df['KOLOM'], bins=20, kde=True, color='blue')
plt.title('JUDUL')
plt.xlabel('X')
plt.ylabel('Y')
plt.show()
```

# BOX PLOT (MATPLOTLIB)
```
VARIABEL1 = df['KOLOM 1'].value_counts().head(5).index
VARIABEL2 = df[df['KOLOM 1'].isin(VARIABEL1)]

plt.figure(figsize=(12, 7)) # Ukuran figure
VARIABEL2.boxplot(column='KOLOM 2', by='KOLOM 1', ax=plt.gca(), grid=False, patch_artist=True, medianprops=dict(color='red'))
plt.title('JUDUL', fontsize=16) # Judul
plt.xlabel('X', fontsize=12) # X Keterangan
plt.ylabel('Y', fontsize=12) # Y Keterangan
plt.xticks(rotation=45, ha='right')
plt.suptitle('') # Menghilangkan judul default dari boxplot.by
plt.tight_layout()
plt.show()
```

# BOX PLOT (SEABORN)
```
VARIABEL1 = df['KOLOM 1'].value_counts().head(5).index
VARIABEL2 = df[df['KOLOM 1'].isin(VARIABEL1)]

plt.figure(figsize=(12, 7)) # Ukuran figure
sns.boxplot(x='KOLOM 1', y='KOLOM 2', data=VARIABEL2, palette='viridis', order=VARIABEL1, hue='KOLOM 1', legend=False)
plt.title('JUDUL', fontsize=16) # Judul
plt.xlabel('X', fontsize=12) # X Keterangan
plt.ylabel('Y', fontsize=12) # Y Keterangan
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```

# SCATTER PLOT (MATPLOTLIB)
```
plt.figure(figsize=(10, 6)) # Ukuran
plt.scatter(df['KOLOM 1'], df['KOLOM 2'], alpha=0.7, color='teal') # Color (Warna)
plt.title('JUDUL', fontsize=16) # Judul
plt.xlabel('X', fontsize=12) # X Keterangan
plt.ylabel('Y', fontsize=12) # Y Keterangan
plt.grid(True)
plt.tight_layout()
plt.show()
```

# SCATTER PLOT (SEABORN)
```
plt.figure(figsize=(10, 6)) # Ukuran
sns.scatterplot(x='KOLOM 1', y='KOLOM 2', hue='KET.KOTAK KECIL', data=df)
plt.title('JUDUL') # Judul
plt.xlabel('X') # X Keterangan
plt.ylabel('Y') # Y Keterangan
plt.legend(title='KET.KOTAK KECIL') # Keterangan dalam kotak kecil
plt.show()
```

# BUBBLE CHART (SEABORN)
```
plt.figure(figsize=(12, 8))
sns.scatterplot(x='KOLOM 1', y='KOLOM 2', size='KOLOM 3', hue='KOLOM 4', data=df, sizes=(50, 1000), alpha=0.7, palette='viridis')
plt.title('Penjualan vs Keuntungan (Ukuran: Kuantitas, Warna: Kategori)', fontsize=16)
plt.xlabel('Penjualan', fontsize=12)
plt.ylabel('Keuntungan', fontsize=12)
plt.grid(True)
plt.legend(title='KOLOM 4', bbox_to_anchor=(1.05, 1), loc='upper left')
plt.tight_layout()
plt.show()
```

# HEATMAP (SEABORN)
```
plt.figure(figsize=(8, 6))
sns.heatmap(data=df[['KOLOM 1', 'KOLOM 2', 'KOLOM 3']].corr(),
            annot=True,
            cmap='viridis',
            fmt='.2f')
plt.title('JUDUL')
plt.show()
```
