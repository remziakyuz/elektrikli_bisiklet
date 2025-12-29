# Bafang M615MM G320.750/1000.C (BBS02B / BBSHD)  
## Motor + Batarya + Aksesuar (36T başlangıç) “Tam Paket” Teknik Notlar

### Bu belgenin amacı
Günümüzde 500W / 750W / 1000W sınıfında orta göbek (mid-drive) motorlarla elektrikli bisikletler **özel ihtiyaçlara göre** kuruluyor veya satın alınıyor.  
Ancak pratikte, sistemin en kritik parçalarından biri olan **batarya/pil** tarafında gerekli **sürekli akım (BMS) kapasitesi** ve buna bağlı **tepe güç** gereksinimleri çoğu zaman göz ardı ediliyor.

Örneğin “1000W nominal” olarak geçen bir motor, kontrolcü limitleriyle birlikte **~1440–1560W** seviyelerine çıkabilen **tepe elektriksel giriş gücü** talep edebilir. Buna rağmen sistem, bazen 500–600W seviyesinde kalabilen (veya düşük sürekli akım verebilen) bataryalarla eşleştiriliyor.  
Ayrıca **aynı anda** yanlış aynakol (dişli), zincir, lastik ve fren seçimleri de yapılabiliyor.

Sonuç olarak:
- Voltaj sarkması → güç düşüşü  
- Isınma / verimsizlik  
- Aktarma organlarında aşırı yük (zincir/ruble/dişli)  
- Beklenen performansın çok altında sürüş

Bu repo ve ek dosyalar, **motor + batarya + aksesuar** uyumunu daha doğru kurgulamak için; özellikle **minimum batarya/BMS akımı** ve **36T’den başlayan doğru dişli yaklaşımı** üzerinden pratik bir rehber sunmak amacıyla hazırlanmıştır.

---

## İçindekiler
1. [Motor Modelleri ve Özet Specler](#1-motor-modelleri-ve-özet-specler)  
2. [Batarya Boyutlandırma: BMS, Ah ve Wh](#2-batarya-boyutlandırma-bms-ah-ve-wh)  
3. [Aynakol (Dişli) Seçimi: 36T ile başla](#3-aynakol-dişli-seçimi-36t-ile-başla)  
4. [Sürekli Güç & Isı: Pratik Derating](#4-sürekli-güç--ısı-pratik-derating)  
5. [Elektrik & Güvenlik: Kablo, Konnektör, Sigorta](#5-elektrik--güvenlik-kablo-konnektör-sigorta)  
6. [Senaryo Bazlı Öneriler](#6-senaryo-bazlı-öneriler)  
7. [Menzil Hesabı Şablonu](#7-menzil-hesabı-şablonu)  
8. [BOM: Parça Listesi (Motor/Batarya/Aksesuar)](#8-bom-parça-listesi-motorbataryaaksesuar)  
9. [Toplam Özet Şablonu](#9-toplam-özet-şablonu)  
10. [Ek Notlar ve Varsayımlar](#10-ek-notlar-ve-varsayımlar)

---

## 1) Motor Modelleri ve Özet Specler

> Not: “Tepe güç” burada yaygın pratik yaklaşımla **yaklaşık Voltaj × Kontrolcü Akımı** üzerinden ifade edilen **tepe elektriksel giriş gücü**dür. Gerçek mekanik tepe; hız, kadans, vites, ısı ve yüke göre değişir.

| Motor kodu | Piyasa adı | Nominal / Sürekli (W) | Voltaj | Kontrolcü akımı (tipik) | Tepe (≈V×A) | Tork | BB uyumu (mm) | Ağırlık | İdeal batarya (BMS) |
|---|---|---:|---:|---:|---:|---|---|---:|---|
| MM G320.750.C | BBS02B | 750 | 48V | 25A | ≈1200W | ≈120–160 Nm *(piyasada farklı yazılabilir)* | 68 / 73 / 83 / 90 / 100 / 110 / 120 | 5.6 kg | **48V BMS ≥30A** *(35A öneri)* |
| MM G320.1000.C | BBSHD | 1000 | 48V | 30A | ≈1440W | 160 Nm *(Peak 200)* | 68 / 73 / 83 / 90 / 100 / 110 / 120 | 5.6 kg | **48V BMS ≥40A** *(45A öneri)* |
| MM G320.750.C | BBS02B (52V) | 750 | 52V | 25A | ≈1300W | ≈120–160 Nm | 68 / 73 / 83 / 90 / 100 / 110 / 120 | 5.6 kg | **52V BMS ≥30A** *(35A öneri)* |
| MM G320.1000.C | BBSHD (52V) | 1000 | 52V | 30A | ≈1560W | 160 Nm *(Peak 200)* | 68 / 73 / 83 / 90 / 100 / 110 / 120 | 5.6 kg | **52V BMS ≥40A** *(45A öneri)* |

---

## 2) Batarya Boyutlandırma: BMS, Ah ve Wh

### 2.1 Kısa formül
- **Enerji (Wh) = Voltaj (V) × Kapasite (Ah)**
- “Güçlü sistem” için sadece Wh değil; özellikle **BMS sürekli akım (A)** önemlidir.

### 2.2 Öneri tablosu (min / rahat)
| Senaryo | V | Kontrolcü A | Önerilen BMS sürekli A | Min Ah | Rahat Ah | Min Wh | Rahat Wh | Not |
|---|---:|---:|---:|---:|---:|---:|---:|---|
| BBS02B 48V | 48 | 25 | ≥30A | 17 | 24 | 816 | 1152 | Şehir + orta yokuş: 24Ah+ daha stabil |
| BBSHD 48V | 48 | 30 | ≥40A | 20 | 28 | 960 | 1344 | Yokuş/kargo: 28Ah daha iyi voltaj/ısı |
| BBS02B 52V | 52 | 25 | ≥30A | 17 | 24 | 884 | 1248 | 52V: daha canlı tepki/hız |
| BBSHD 52V | 52 | 30 | ≥40A | 20 | 28 | 1040 | 1456 | XT90-S + kalın kablo + güçlü sigorta |

> Pratik not: BMS sürekli akım yetersizse (ör. 20–25A), motor nominali yüksek olsa bile **ani güç düşüşleri** yaşanır.

---

## 3) Aynakol (Dişli) Seçimi: 36T ile başla

Aynakol dişlisi küçük oldukça:
- düşük hız tırmanışta motor daha verimli çalışır,
- akım ve ısı artışı daha kontrol edilebilir,
- zincir ve ruble üzerindeki yük azalır.

| Aynakol (T) | Kullanım | Artılar | Eksiler | Önerilen motor | Not |
|---:|---|---|---|---|---|
| **36T** | Dik yokuş / kargo / düşük hız | Tırmanış güçlü, ısı daha az | Düzde max hız düşer | BBS02B / BBSHD | **Başlangıç dişlisi önerisi** |
| 38T | Yokuş + şehir dengesi | Dengeli | 36T kadar tırmanış avantajı yok | BBS02B / BBSHD | Günlük için iyi denge |
| 40T | Şehir + hafif yokuş | Şehir hızları rahat | Ağır yükte ısınma artabilir | BBS02B | Düz ağırlıkta mantıklı |
| 42T | Genel kullanım | Bulunurluk yüksek | Uzun yokuşta akım yükselir | BBS02B / BBSHD | Yokuş varsa 36–38T daha iyi |
| 44T | Hız odaklı | Düzde daha hızlı | Yokuşta zorlar | BBSHD | Kargo/yokuş için önerilmez |
| 46T | Maks hız odaklı | Düzde en hızlı | Isı/akım artar | BBSHD | Fren/lastik/aktarma güçlü olmalı |

---

## 4) Sürekli Güç & Isı: Pratik Derating

| Koşul | Sürekli güç önerisi | Akım davranışı | Risk | Pratik önlem |
|---|---|---|---|---|
| Düz yol, 20–30 km/h | Nominalin %80–100’ü | Ortalama akım düşük | Düşük | Kadans 80–100 rpm, doğru vites |
| Uzun yokuş 6–10% | Nominalin %50–70’i | Akım uzun süre yüksek | Orta | **36–38T**, düşük vites, dur-kalk azalt |
| Çok dik yokuş >10%, <10 km/h | Nominalin %30–50’si | Akım maksimuma yakın | Yüksek | Mola/soğut, küçük dişli, gerekirse BBSHD |
| Kargo + yokuş | Nominalin %30–60’ı | Voltaj sarkması görülebilir | Yüksek | Yüksek BMS, kalın kablo, **36T**, güçlü fren |
| Sıcak hava + düşük hız | Nominalin %30–60’ı | Isı birikir | Yüksek | Aralıklı sürüş, gölgede soğut |

---

## 5) Elektrik & Güvenlik: Kablo, Konnektör, Sigorta

| Bileşen | BBS02B (25A) | BBSHD (30A) | Not |
|---|---|---|---|
| Besleme kablosu | **12 AWG (min)** | **10 AWG (öneri)** / 12 AWG (min) | Kısa tut; 52V/uzun kabloda kalınlaştır |
| Konnektör | XT60 (min) | XT90 / **XT90-S (öneri)** | XT90-S kıvılcımı azaltır |
| Sigorta | 35A | 45A | Bataryaya yakın konumlandır |
| Anahtar/kontaktör | 48–52V 40A sınıfı | 48–52V 60A sınıfı | Servis/kargo için pratik |
| BMS sürekli akım | ≥30A (35A rahat) | ≥40A (45A rahat) | “Sürekli” akım kritik |
| Şarj | 3–5A | 5–8A | Hızlı şarjda ısı kontrolü |

---

## 6) Senaryo Bazlı Öneriler

| Senaryo | Motor | Voltaj | Aynakol başlangıç | Batarya örneği | Kritik not |
|---|---|---|---|---|---|
| Şehir, düz ağırlıklı | BBS02B | 48V | 38–42T *(min 36T)* | 48V 20–24Ah, BMS ≥30–35A | Uzun yokuş varsa 36–38T |
| Şehir + düzenli yokuş | BBS02B / BBSHD | 48V | **36–38T** | 48V 24–28Ah, BMS ≥35–45A | Isı için küçük dişli + vites |
| Dağ / çok dik yokuş | BBSHD | 48/52V | **36T** | 52V 24–28Ah, BMS ≥45A | Düşük hızda ısınma → mola |
| Kargo + yokuş | BBSHD | 48V | **36T** | 48V 28Ah+, BMS ≥45A | Fren/aktarma güçlendir |
| Banliyö, hız odaklı | BBSHD | 52V | 40–46T *(min 36T)* | 52V 24–28Ah, BMS ≥45A | Fren/lastik kritik |

---

## 7) Menzil Hesabı Şablonu

### 7.1 Basit yaklaşım
- **Wh = V × Ah**
- **Menzil (km) = Wh / (Wh/km)**

### 7.2 Tipik tüketim bantları (yaklaşık)
- Düz / ekonomik: **8–12 Wh/km**
- Karma: **12–18 Wh/km**
- Yokuş / kargo: **18–28 Wh/km**

### 7.3 Örnekler
| Senaryo | Örnek batarya | Wh/km | Tahmini menzil |
|---|---:|---:|---:|
| Şehir düz | 48V 20Ah (960Wh) | 10 | ≈96 km |
| Şehir karma | 48V 24Ah (1152Wh) | 15 | ≈77 km |
| Yokuş/kargo | 48V 28Ah (1344Wh) | 22 | ≈61 km |
| Hız odaklı | 52V 24Ah (1248Wh) | 18 | ≈69 km |

---

## 8) BOM: Parça Listesi (Motor/Batarya/Aksesuar)

> Blogger içinde script/input sorunları olabildiği için BOM burada **statik** tutulmuştur.  
> Excel/Sheets tarafında “Toplam = Adet × Birim fiyat” ile kolayca hesaplanabilir.

### 8.1 Motor
| Parça | Spec | Adet | Not |
|---|---|---:|---|
| Motor (BBS02B / BBSHD) | Seçtiğin modele göre | 1 | Motor + kontrolcü gövde |

### 8.2 Batarya
| Parça | Spec | Adet | Not |
|---|---|---:|---|
| Batarya paketi | 48/52V, 20–28Ah+ / BMS 30–45A | 1 | Sürekli akım kritik |
| Şarj cihazı | 48/52V uyumlu, 3–5A (ops. 8A) | 1 | Hızlı şarjda ısı takibi |

### 8.3 Aksesuar (öneri seti)
| Parça | Spec | Adet | Not |
|---|---|---:|---|
| **Aynakol dişli** | **36T başlangıç** | 1 | Yokuş/kargo için ideal |
| Konnektör | XT60 (min) / XT90-S (öneri) | 2 | Anti-spark önerilir |
| Kablo | 12 AWG (min) / 10 AWG (öneri) | 1 | Kısa tut |
| Sigorta + yuva | 35A (BBS02B) / 45A (BBSHD) | 1 | Bataryaya yakın |
| Vites sensörü | Shift sensor (opsiyonel) | 1 | Aktarmayı korur |
| Fren upgrade | Hidrolik + 180–203mm rotor | 1 | Güvenlik için kritik |
| Makaron/izolasyon | Yapışkanlı heat-shrink | 1 | Su/titreşim |

---

## 9) Toplam Özet Şablonu

Bu repo için önerilen basit maliyet kırılımı:

- **Motor toplamı** = Motor satırları
- **Batarya toplamı** = Batarya + şarj satırları
- **Aksesuar toplamı** = diğer tüm parçalar

| Grup | Toplam |
|---|---:|
| Motor | ____ |
| Batarya | ____ |
| Aksesuar | ____ |
| **Genel toplam** | ____ |

---

## 10) Ek Notlar ve Varsayımlar

- Bu dokümandaki “tepe güç” değerleri, yaygın sahada kullanılan **V×A** yaklaşımıyla “tepe elektriksel giriş gücü” olarak değerlendirilmiştir.
- BMS değerleri “anlık tepe” değil, **sürekli akım** kapasitesine göre seçilmelidir.
- Düşük hız + yüksek tork (özellikle dik yokuş/kargo) koşullarında ısı hızla birikebilir: **36T** başlangıç yaklaşımı bu yüzden önerilir.
- Fren/lastik/aktarma organları, güç arttıkça güvenlik ve dayanım açısından kritik hale gelir.

---
