---
name: planlama
description: Bulk planlama satırlarını al; birim fiyat çalışılabilirliğini değerlendir, çalışılabilir ve çalışılamaz kalemleri ayırt et, revizyon gerektirenleri raporla.
---

Bulk planlama satırlarını al; birim fiyat çalışılabilirliğini değerlendir, çalışılabilir ve çalışılamaz kalemleri ayırt et.

## Görevin adımları:

**1. Satırları oku**
Her satır için şunları tespit et:
- Kalem adı / tanımı
- Miktar ve birimi (adet, kg, m², saat, vb.)
- Birim fiyat

**2. Birim Fiyat Çalışılabilirlik Değerlendirmesi**
Her satır için aşağıdaki kriterleri uygula:

✅ **Çalışılabilir** — şu koşulların tümü sağlanıyorsa:
- Birim fiyat girilmiş ve sıfırdan büyük
- Kalem tanımına ve birimine göre makul bir değer
- Bütçe hesabı yapılabilecek düzeyde yeterli bilgi var

🔴 **Çalışılamaz** — şu koşullardan biri varsa:
- Birim fiyat boş veya girilmemiş
- Fiyat 0, 1 veya açıkça placeholder
- Birim tanımlanmamış (fiyat var ama neyin fiyatı belirsiz)
- Kalem tanımı ile fiyat arasında belirgin uyumsuzluk
- Fiyatın kullanılabilmesi için ek bilgi gerekiyor

**3. Çıktı**

## Çalışılabilir Kalemler ✅

| # | Kalem | Miktar | Birim | Birim Fiyat | Not |
|---|-------|--------|-------|-------------|-----|
| 1 | ... | ... | ... | ... | ... |

---

## Çalışılamaz Kalemler 🔴

| # | Kalem | Sorun | Gerekli Aksiyon |
|---|-------|-------|----------------|
| 1 | ... | Fiyat boş / Placeholder / Birim yok / Tanım-fiyat uyumsuzluğu | ... |

---

**4. Özet**
- Toplam satır sayısı
- ✅ Çalışılabilir: X kalem
- 🔴 Çalışılamaz: X kalem
- En sık tekrarlayan sorun türü
- Önerilen sıradaki adım

---
Planlama satırları: $ARGUMENTS
