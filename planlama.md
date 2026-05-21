Bir planlama raporu, veri özeti veya durum bilgisi al. Oku, analiz et ve somut öneriler sun.

Platform bağlamı: ITA (İhale Platformu), SAP, EBYS, OIS, Depo/Lojistik, Power BI.

---

## Görevin adımları:

**1. Girdiyi anla**
- Ne tür bir veri veya rapor sunuluyor? (talep listesi, ihale takvimi, bütçe özeti, gecikme raporu, vb.)
- Zaman dilimi nedir?
- Hangi platform(lar) veya süreç(ler) kapsanıyor?
- Girdide eksik veya belirsiz bilgi var mı? Varsa en sona "Netleşmesi gerekenler" tablosuna yaz.

**2. Mevcut durum analizi**
Her kategoriyi değerlendir; ilgisiz olanları atla.

**2a. Beklemede / Gecikmiş Kalemler**
- Hangi talepler, ihaleler veya süreçler beklemede?
- Bekleme süresi ne kadar? Kritik eşiği geçmiş mi?
- Gecikmenin nedeni: onay bekleme, eksik belge, kaynak yokluğu, tedarikçi gecikmesi?

**2b. Kritik Yol Riski**
Tedarik kritik yolu: Talep → İhale → Teklif → Komisyon Kararı → Sözleşme → SAS → Mal Kabul → Birime Teslim
- Hangi adımda tıkanma var?
- Bu tıkanma aşağı akışı blokluyor mu?

**2c. Kapasite ve Yük Dağılımı**
- Belirli bir onay makamı veya kullanıcı aşırı yüklü mü?
- Aynı dönemde çok sayıda ihale/komisyon kararı çakışıyor mu?

**2d. Bütçe ve Tahmini Bedel**
- Bütçe üstü risk var mı?
- Tahmini bedel belirsiz olan kalemler var mı?

**2e. Platform Uyarıları**
- ITA'da statüsü uzun süredir değişmeyen kayıt var mı?
- SAP'ta bekleyen belge (fatura kontrol, mal girişi) var mı?
- EBYS'de imza bekleme süresi uzun olan evrak var mı?
- OIS'te yanıt vermeyen tedarikçi var mı?

**3. Öncelik Matrisi**
Bulguları aşağıdaki formatta özetle:

| # | Kalem / Süreç | Platform | Durum | Etki | Öncelik |
|---|--------------|----------|-------|------|---------|
| 1 | ... | ... | Beklemede / Gecikmiş / Risk | 🔴 Yüksek / 🟡 Orta / 🟢 Düşük | 🔴 Acil / 🟡 Bu hafta / 🟢 Planlı |

Öncelik mantığı:
- 🔴 Acil: Kritik yolu blokluyor VEYA yasal/sözleşme son tarihi geçmek üzere
- 🟡 Bu hafta: Gecikme başladı ama henüz kritik değil
- 🟢 Planlı: Gündemde tutulmalı, acil değil

**4. Öneriler**
Her 🔴 ve 🟡 kalem için somut, uygulanabilir öneri. Alakasız kategorileri atla.

```
## Öneriler

⚡ Hemen Yapılacaklar
- [ ] ...

📅 Bu Hafta İçinde
- [ ] ...

🔧 Süreç İyileştirme
- [ ] ...

📊 Raporlama / Görünürlük
- [ ] ...
```

**5. Özet**
- Toplam kaç kalem incelendi
- 🔴 Acil / 🟡 Bu hafta / 🟢 Planlı dağılımı
- En kritik 1-2 eylem
- Sıradaki adım

---

**Netleşmesi Gerekenler** (varsa)

| # | Soru | Kimin Yanıtlaması Gerekiyor |
|---|------|---------------------------|
| 1 | ... | ... |

---
Rapor veya planlama verisi: $ARGUMENTS
