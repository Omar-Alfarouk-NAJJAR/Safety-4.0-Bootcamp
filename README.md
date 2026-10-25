[README.md](https://github.com/user-attachments/files/33938511/README.md)
# Safety 4.0 Bootcamp — Laboratuvar Cevapları (LAB 1–4)

**Makine:** Denge Bagaj Taşıma Sistemi (besleme konveyörü + bagaj carousel'i)
**Eğitim:** INSPECCO × KRIPTARIUM · Safety 4.0 Bootcamp
**Durum:** Eğitim çıktısı. Resmî denetim, uygunluk değerlendirmesi veya belgelendirme değildir; CE/mevzuat uygunluğu garantisi vermez.

---

## 1. Bu repo ne içeriyor?

Bootcamp'te iki föy seti verildi: **Şişeleme Hattı (Genel Sürüm)** ve **PaketPro 3000 (Paketleme Makinesi)**. Her sette 7 laboratuvar var. Bu repoda her iki setin **ilk 4 laboratuvarı** (LAB 1–4), kendi seçtiğimiz makineye göre Türkçe olarak cevaplandı.

Her laboratuvar ayrı bir Word belgesi olarak ait olduğu klasörde yer almaktadır.

## 2. Makine seçimi: neden bagaj taşıma sistemi?

Denge Havacılık (DENGE Airport Equipment, İstanbul / İkitelli OSB) 1982'den beri havalimanı ekipmanı üretiyor ve ürünlerini 100'den fazla ülkede pazarlıyor. Sitelerindeki ürün grupları:

1. Yer Hizmetleri Ekipmanları (GSE), ör. yolcu merdiveni
2. **Bagaj Taşıma Sistemleri** (konveyör, carousel)
3. Kargo Transfer Sistemleri
4. ULD Depolama Sistemleri
5. Askerî Ekipman (ör. kamyon üstü makaslı kule)

Bunlardan **bagaj taşıma sistemi** seçildi, çünkü:

- Yapısı sade ve kolay anlatılıyor: sensör → PLC → motor sürücüleri → bant.
- Föylerdeki mimariyle birebir örtüşüyor: normal kontrol yolu ile ayrı bir safety yolu (acil durdurma / çekme halatı / kapak kilidi → Safety PLC → STO).
- Tehlike somut: bant ağızlarında ve carousel plakalarında sıkışma, ezilme, makaslama; en kötü senaryo bakım sırasında bandın beklenmedik çalışması.
- Denge'nin 7/24 destek hizmeti vermesi, uzak servis erişimi senaryosunu (LAB 2 ve LAB 4) anlamlı kılıyor.

## 3. Varsayımlar (önemli)

Firmanın ürün tasarımına dair kamuya açık teknik ayrıntı yok. Bu yüzden cevaplar **eğitim amaçlı varsayımlara** dayanır: normal PLC, bant sürücüleri, HMI, ayrı Safety PLC ve üretici desteği için uzak servis erişimi. Bu repo, Denge'nin gerçek mimarisini yansıttığını iddia etmez.

PaketPro föyünde senaryo verileri (internete açık uzak bakım modülü, `admin/admin`, port 80 HMI, kartonda Wi-Fi parolası, kilitsiz USB, bulut telemetri) **kendi makinemize uyarlanmış senaryo koşulları** olarak kullanıldı. PaketPro'nun çene/bıçak tehlikesinin bizdeki karşılığı bant sıkışma ve ezilme noktalarıdır.

## 4. Laboratuvarlar ve çıktılar

| Lab | Konu | Çıktı | Evidence Pack |
|---|---|---|---|
| 1 | Safety Architecture | Safety Function Map | EP 03 |
| 2 | IEC 62443 Mini Workshop | Zone / Conduit Diagram | EP 05 |
| 3 | Threat & Risk + Risk Matrix | Risk Register | EP 04 |
| 4 | Secure Remote Access | Secure Architecture | EP 02 + EP 06 |

### Öne çıkan sonuçlar

- **Emniyet fonksiyonları:** acil durdurma (STO) ve bakım/erişim kapağı kilidi. Hedef güvenilirlik PLr d (varsayım).
- **Dijital kesişim noktası:** uzak servis erişimi → ağ → Safety PLC konfigürasyon yolu. Asıl zayıf halka burası.
- **Bölgeler (zone):** Emniyet, Kontrol, Operasyon, Mühendislik, Uzak erişim (DMZ), Kurumsal. Safety PLC kendi bölgesinde.
- **En yüksek risk (skor 18, Kritik):** zayıf korunan uzak erişim → emniyet konfigürasyonu → bakım sırasında bant çalışır → el/kol sıkışması.
- **S=3 kuralı:** skoru düşük kalan ama ağır sonuçlu senaryo (Safety PLC yapılandırmasının değiştirilmesi) bayrakla öne alındı.
- **Uzak erişim kararı:** jump server, VPN, MFA, kişisel hesap, tam oturum kaydı, varsayılan kapalı.
- **Emniyet bağımsızlığı:** uzak erişim ele geçirilse bile emniyet fonksiyonu devre dışı kalmamalı. Cevaplar çözüm değil **gereksinim** olarak yazıldı (föyün tarafsızlık notuna uygun).

## 5. Önerilen repo yapısı

```
Safety_4.0_Bootcamp/
├── README.md
├── Siseleme_Hatti/
│   ├── LAB1_Safety_Architecture.docx
│   ├── LAB2_IEC_62443_Mini_Workshop.docx
│   ├── LAB3_Threat_and_Risk.docx
│   └── LAB4_Secure_Remote_Access.docx
└── PaketPro_3000/
    ├── LAB1_Safety_Architecture.docx
    ├── LAB2_IEC_62443_Mini_Workshop.docx
    ├── LAB3_Threat_and_Risk.docx
    └── LAB4_Secure_Remote_Access.docx
```

## 6. Sıradaki adımlar

- LAB 5–7 (SBOM/CVE/Patch, CRA Incident Simulation, AI Safety Challenge) cevaplanacak.
- Tüm föyler tamamlanınca **Machine Starter Pack** oluşturulacak.
