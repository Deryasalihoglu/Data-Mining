# Data Mining Project: Academic Publication Analysis

## 📋 Proje Özeti / Project Summary

Bu proje, akademik yayınlar veritabanından Bilgisayar Bilimleri alanındaki makaleleri çıkarmak, analiz etmek ve modellemek için gerekli verileri hazırlamayı amaçlamaktadır.

**EN:** This project aims to extract Computer Science academic articles from a publication database, analyze them, and prepare the data for text mining and clustering models.

---

## 🎯 Proje Hedefleri / Project Goals

- ✅ Veritabanı yapısını analiz etmek ve ilişkileri anlamak
- ✅ Bilgisayar Bilimleri alanındaki makaleleri filtrelemek
- ✅ Makalelerin dağılımını ve istatistiklerini incelemek
- ✅ Modelleme için temiz bir veri seti hazırlamak
- ✅ Metin analizi ve kümeleme için özet verilerini çıkarmak

**EN:**
- ✅ Analyze database structure and relationships
- ✅ Filter Computer Science articles
- ✅ Examine article distribution and statistics
- ✅ Prepare a clean dataset for modeling
- ✅ Extract abstracts for text analysis and clustering

---

## 📁 Proje Yapısı / Project Structure

```
DM-Final/
├── README.md                          # Proje belgelendirmesi / Project documentation
├── data/
│   ├── CompSciencePub.bak            # Veritabanı yedekleme dosyası / Database backup
│   └── CompSciencePub.sqlite         # Ana veritabanı / Main database
└── notebooks/
    └── data_extract.ipynb            # Veri çıkarma ve analiz notebook'u / Data extraction notebook
```

---

## 🗄️ Veritabanı Şeması / Database Schema

### Ana Tablolar / Main Tables

| Tablo | Açıklama |
|-------|----------|
| **AcademicRecord** | Akademik yayın kayıtları / Academic publication records |
| **AcademicRecordAbstract** | Makalelerin özetleri / Article abstracts |
| **Publication** | Dergi bilgileri / Journal information |
| **AcademicSubject** | Akademik disiplinler / Academic disciplines/subjects |
| **AcademicRecordSubject** | Makaleler-Disiplin ilişkisi / Article-Subject relationships |
| **AcademicRecordKeywordPlus** | Makale anahtar kelimeleri / Article keywords |

### Veri İlişkileri / Data Relationships

```
AcademicRecord
    ├── AcademicRecordAbstract (1:1)
    ├── Publication (Many:1)
    ├── AcademicRecordSubject (Many:Many)
    │   └── AcademicSubject
    └── AcademicRecordKeywordPlus (Many:1)
```

---

## 📊 Notebook Analizi / Notebook Analysis

### `data_extract.ipynb`

Notebook'ta yapılan ana analiz adımları:

#### 1️⃣ **Veritabanı Bağlantısı ve İlk Keşif**
- SQLite veritabanına bağlanma
- Tüm makaleler, dergiler ve soyutlamalar hakkında genel istatistikler

#### 2️⃣ **Akademik Disiplinler Analizi**
- Mevcut tüm akademik konuları listeleme
- Bilgisayar Bilimleri kategorilerini tanımlama
- Farklı CS alt disiplinlerinin dağılımını gösterme

#### 3️⃣ **Hedef Veri Seti Oluşturma**
- "Computer Science%" kategorisine ait makaleleri filtreleme
- Soyutlamaya sahip makaleleri seçme
- Geleneksel (traditional) CS kategorilerine odaklanma

#### 4️⃣ **İstatistiksel Analiz**
- Derg sayısı ve makale sayısı hesaplaması
- Bilgisayar Bilimleri alt alanlarına göre dağılım
- Anahtar kelime ve soyutlama mevcudiyeti kontrolü

#### 5️⃣ **Özel Alt Alanlar İncelemesi**
- Yapay Zeka (AI) makaleleri
- Donanım & Mimarı (Hardware & Architecture) makaleleri

---

## 📈 Temel Bulgular / Key Findings

Notebook'tan elde edilen temel sonuçlar:

| Metrik | Değer |
|--------|-------|
| **Toplam CS Makalesi** | ~7,711+ |
| **Benzersiz Dergiler** | 100+ |
| **CS Alt Kategorileri** | 30+ |
| **Soyutlaması Olan Makaleler** | %90+ |
| **Anahtar Kelimesi Olan Makaleler** | Değişken |

---

## 🔧 Gereksinimler / Requirements

### Python Kütüphaneleri / Python Libraries

```python
sqlite3      # SQLite veritabanı bağlantısı / SQLite database connection
pandas       # Veri analizi ve manipülasyon / Data analysis and manipulation
numpy        # Sayısal işlemler / Numerical operations
matplotlib   # Görselleştirme / Visualization
seaborn      # İstatistiksel görselleştirme / Statistical visualization
```

### Kurulum / Installation

```bash
pip install pandas numpy matplotlib seaborn
```

---

## 🚀 Kullanım / Usage

### Notebook'u Çalıştırma / Running the Notebook

1. Jupyter Notebook ortamını başlatın:
```bash
jupyter notebook
```

2. `notebooks/data_extract.ipynb` dosyasını açın

3. Hücreleri sırayla çalıştırın (Shift + Enter)

4. Veritabanı sorguları çalıştırılacak ve sonuçlar ekranda görüntülenecektir

### Özel Sorgular / Custom Queries

Veritabanından özel veriler çıkarmak için:

```python
import sqlite3
import pandas as pd

conn = sqlite3.connect('./data/CompSciencePub.sqlite')

query = """
SELECT AcademicRecordid, AbstractText
FROM AcademicRecord ar
JOIN AcademicRecordAbstract aa ON ar.AcademicRecordid = aa.AcademicRecordid
WHERE ar.AcademicRecordid IN (1, 2, 3)
"""

df = pd.read_sql_query(query, conn)
print(df)

conn.close()
```

---

## 🔄 Sonraki Adımlar / Next Steps

1. **Metin Ön İşlemi** - Soyutlamalar üzerinde temizleme ve normalleştirme
2. **Özellik Çıkarma** - TF-IDF, Word2Vec, BERT embedding'i
3. **Kümeleme** - K-Means, DBSCAN, Hierarchical Clustering
4. **Konusu Modelleme** - LDA, NMF, Top2Vec
5. **Görselleştirme** - t-SNE, UMAP projeksiyonları
