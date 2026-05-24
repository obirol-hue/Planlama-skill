# Planlama Skill — ITP Analiz ve Konsolidasyon Asistanı

Satınalma Planlama Ekibi için geliştirilmiş Claude Code skill'i.  
İTP/Hyperion satırlarını alım davranışı odaklı analiz eder; birim fiyat yöntemleri üretir ve konsolidasyon fırsatlarını skora dönüştürür.

---

## Kurulum

```powershell
# Windows
Copy-Item planlama.md "$env:USERPROFILE\.claude\commands\planlama.md"
```

Kurulumdan sonra Claude Code'da `/planlama` komutu olarak çalışır.

---

## Modüller

### Modül 1 — ITP Satır Analizi

Her ITP/Hyperion satırını mal grubu odaklı değil, **alım davranışı odaklı** analiz eder.

**Ne zaman kullanılır:**
```
/planlama [ITP satırlarını yapıştır veya dosyayı yükle]
```

**Ne üretir:**

| Çıktı | Açıklama |
|-------|----------|
| Alım Tipi | Abonelik, katalog, cihaz, hizmet, yapım işi vb. 12 tip |
| Birim Fiyat Yeterliliği | ✅ Yeterli / ⚠️ Kısmen Yeterli / 🔴 Yetersiz |
| Birim Fiyat Çalışma Yöntemi | Tedarikçiden tam olarak ne isteneceği |
| Risk Tespiti | Döviz riski, teşvik kontrolü, şüpheli kategori |
| Planlama Notu | Ekip için özet değerlendirme |
| Karar Logu | Denetlenebilir gerekçe |

**Ayırdığı kayıtlar:**
- 🔒 Bütçe Rezervasyonu — birim fiyat ≤ 1 TL veya sembolik kayıtlar
- 📋 Açık Masraf / Mali İşler — kazı, noter, denklik, postdoc, avans, mahsup vb.

**Desteklenen alım tipleri:**

| Tip | Örnek |
|-----|-------|
| Abonelik / Lisans Yenileme | SaaS, portal, yıllık lisans |
| Aylık Sabit Hizmet | Temizlik, güvenlik, taşıma |
| Cihaz Bakım / PM Sözleşmesi | Yıllık bakım anlaşması, kalibrasyon |
| Katalog / Sarf Alımı | Toner, kırtasiye, temizlik malzemesi |
| Tekil Cihaz / Ekipman | Lab cihazı, sunucu, ekipman |
| Büyük Ekipman / Teşvik | Dövizli, yüksek tutarlı, teşvik kapsamlı |
| Açık Sepetli Lab Sarf Çerçevesi | Genel kimyasal/sarf bütçesi |
| Spesifik Cihaz Sarfı / Tek Kaynak | Belirli marka/model sarfı |
| Yazılım Projesi / SaaS | Geliştirme, entegrasyon, lisans |
| Anahtar Teslim Yapım / Tadilat | İnşaat, tadilat, boya |
| Etkinlik / Yemek / Organizasyon | Catering, sempozyum, toplantı |
| Promosyon / Baskı | Logolu ürün, matbaa |

**Girdi formatı:**

Excel'den kopyala-yapıştır veya CSV. Şu alanlar olursa en iyi sonucu verir:

```
İhtiyaç Tanımı | Mal Grubu Kodu | Mal Grubu Adı | Miktar | Ölçü Birimi
Birim Fiyat | Para Birimi | Toplam TRY | Bütçe Türü | Teşvik Bilgisi
```

---

### Modül 2 — Konsolidasyon ve Paketleme Analizi

Dağınık ihtiyaçları otomatik yakalar ve konsolidasyon fırsatlarını skora dönüştürür.

**Ne zaman çalışır:**

```
/planlama konsolidasyon analizi yap
/planlama hangi kalemler birleşir
/planlama çerçeve sözleşme adaylarını bul
/planlama paketleme öner
/planlama ölçek ekonomisi fırsatları nelerdir
```

**Analiz Motoru — 3 Sinyal:**

| Sinyal | Ne Tespit Eder | Ham Skor Formülü |
|--------|---------------|-----------------|
| **Dikey** | Tek MG altında çok birime dağılmış kalemler | √(kalem × birim × milyon_TRY) |
| **Çapraz** | Aynı MG ailesinde farklı kodlara dağılmış kalemler | √(kalem × MG × milyon_TRY) × 1.3 |
| **Yatay** | Aynı ürün/hizmet farklı MG'lerde tekrarlıyorsa | √(kalem × MG × birim × milyon_TRY) |

**Kategori çarpanları:**

| Kategori | Çarpan |
|----------|--------|
| Sarf / katalog | × 1.5 |
| Hizmet | × 1.2 |
| BT donanım | × 1.1 |
| Mobilya / yapım | × 1.0 |
| Cihaz / ekipman | × 0.8 |
| Abonelik / lisans | × 0.4 |
| Tek kaynak / kamu tarife / akademik masraf | × 0.0 |

**Sınıflandırma:**

| Düzeltilmiş Skor | Sınıf | Tasarruf Tahmini |
|-----------------|-------|-----------------|
| ≥ 100 | GÜÇLÜ ADAY | %8–%15 |
| 50–99 | ORTA ADAY | %4–%8 |
| 20–49 | ZAYIF ADAY | %2–%4 |
| < 20 | KONSOLİDASYON ÖNERİLMEZ | — |

**Üretilen çıktılar:**

1. **Konuşma Özeti** — ilk 5 fırsat, genel tablo
2. **Konsolidasyon Skor Tablosu** — tüm fırsatlar skorlanmış
3. **Fırsat Detay Kalemleri** — her fırsata bağlı ITP satırları
4. **Yanlış Sınıflandırma Uyarıları** — mal grubu uyumsuzlukları
5. **Konsolidasyona Uygun Olmayanlar** — tek kaynak, kamu tarife, masraf vb.

**Paketleme Simülasyonu** (ilk 5 fırsat için):
Her fırsat için 4 senaryo karşılaştırması: tek mega ihale / alt paketler / ortak müzakere takvimi / mevcut yapı

---

## Önemli Kural

Bu skill hiçbir zaman doğrudan satınalma kararı vermez.  
Fırsat tespit eder, önceliklendirir, seçenek sunar, gerekçe üretir.  
**Karar kullanıcıya aittir.**

---

## Örnek Kullanım

```
/planlama
[Excel'den kopyaladığınız ITP satırları]
```

```
/planlama konsolidasyon analizi yap
[Excel'den kopyaladığınız ITP satırları]
```
