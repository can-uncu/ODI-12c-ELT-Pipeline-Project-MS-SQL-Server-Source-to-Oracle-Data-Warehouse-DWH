# ODI-12c-ELT-Pipeline-Project-MS-SQL-Server-Source-to-Oracle-Data-Warehouse-DWH

Bu proje, Microsoft AdventureWorks2022 veritabanını kullanarak uçtan uca bir **ETL – Staging – Data Warehouse** mimarisi kurmak amacıyla geliştirilmiştir. Proje boyunca kaynak sistem SQL Server, ETL aracı Oracle Data Integrator (ODI 12c) ve hedef sistem Oracle veri tabanı kullanılmıştır.

---

## 🚀 Projenin Amacı

Bu projenin hedefi, operasyonel (OLTP) verinin;
- Kaynaktan okunması,
- Staging katmanında temizlenip dönüştürülmesi,
- Boyut (Dimension) ve Olgu (Fact) tablolarına yüklenmesi,
- Kurumsal bir Data Warehouse mimarisinin oluşturulmasıdır.

---

📘 **Mimari Diyagramı:**

<div align="center">
  <img src="https://github.com/can-uncu/ODI-12c-ELT-Pipeline-Project-MS-SQL-Server-Source-to-Oracle-Data-Warehouse-DWH/blob/main/etl-architecture-diagram.jpg" alt="Mimari Diagram" width="1669" height="334"/>
</div>

## 🏛️ Mimari Yapı

### **1. Kaynak Sistem (Source)**
- **Veritabanı:** SQL Server 2022  
- **Şema:** AdventureWorks2022  
- **Kullanılan Tablolar:**
  - Customer, Person, EmailAddress
  - Product, ProductCategory, ProductSubcategory
  - Address, StateProvince, CountryRegion
  - SalesOrderHeader, SalesOrderDetail
  - SalesPerson, Employee

### **2. ETL Katmanı**
- **Araç:** Oracle Data Integrator 12c (ODI)
- **Kullanılan KM'ler:**
  - LKM SQL to Oracle (DB LINK)
  - IKM Oracle Control Append

### **3. Staging Katmanı**
- **Veritabanı:** Oracle  
- Kaynaktan gelen verilerin:
  - Join edilmesi
  - Temizlenmesi
  - Tip dönüşümlerinin yapılması
  - ETL metadata kolonlarının eklenmesi
- **Oluşturulan STG Tablolar:**
  - STG_CUSTOMER  
  - STG_PRODUCT  
  - STG_PRODUCTCATEGORY  
  - STG_PRODUCTSUBCATEGORY  
  - STG_ADDRESS  
  - STG_STATEPROVINCE  
  - STG_COUNTRYREGION  
  - STG_EMPLOYEE  
  - STG_SALESPERSON  
  - STG_SALESORDERHEADER  
  - STG_SALESORDERDETAIL  

### **4. Data Warehouse Katmanı**

Boyut ve Olgu tabloları oluşturularak kurumsal yıldız şema tasarımı hazırlanmıştır:
- DIM_CUSTOMER  
- DIM_PRODUCT  
- DIM_ADDRESS  
- DIM_SALESPERSON  
- FACT_SALES

---

## 🧩 ETL Süreci

### **1) Source → Staging**
- Normalize tablolar join edildi (Customer + Person + EmailAddress gibi)
- Null & boşluk temizliği
- Tip dönüşümleri (nvarchar → varchar2, datetime → date)
- Dönüşüm kuralları (TRIM, NVL, REPLACE)
- ETL yükleme tarihi eklendi (ETL_LOAD_DATE)
- Her yüklemede STG tablosu TRUNCATE edildi

### **2) Staging → DWH**
- Surrogate key üretimi
- Slowly Changing Dimension (SCD Type 1)
- Fact tablosu hesaplamaları
- Star schema modelleme


⭐ **Star Schema:**

<div align="center">
  <img src="https://github.com/can-uncu/ODI-12c-ELT-Pipeline-Project-MS-SQL-Server-Source-to-Oracle-Data-Warehouse-DWH/blob/main/Star%20Schema.jpg" alt="Mimari Diagram" width="1000"/>
</div>





---

## 📦 Proje Çıktıları
- Tamamlanmış ETL süreçleri (ODI 12c)
- Çalışan Source → STG mapping setleri
- Yıldız şema DWH modeli
- Veri kalitesi kontrolleri
- Yükleme paketleri (Batch & Master Package)

---

## 🛠 Kullanılan Teknolojiler
- **Oracle Data Integrator (ODI 12c)**
- **SQL Server 2022**
- **Oracle (DWH) SQL Developer**

---

## ✨ Öğrenilen / Gösterilen Yetkinlikler
- Uçtan uca ETL pipeline geliştirme
- Staging & DWH mimarisi
- ODI Topology, Model, Mapping, Packages kullanımı
- Performans odaklı ETL tasarımı
- Boyut & Olgu modelleme

---

## 📬 İletişim

Eğer proje hakkında daha fazla bilgi almak isterseniz bana ulaşabilirsiniz.
