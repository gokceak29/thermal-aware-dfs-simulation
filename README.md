# thermal-aware-dfs-simulation
# Isı Geri Beslemeli Dinamik Frekans Ölçekleme (Temperature-Aware DFS)

İşlemci sıcaklığını gerçek zamanlı takip edip frekansı otomatik olarak ayarlayan,
Java ile yazılmış bir **termal farkındalıklı DFS simülasyonu**.
> Bilgisayar Mimarisi dersi kapsamında geliştirilmiştir.

## Proje Hakkında

Modern işlemciler aşırı ısındığında performans düşer (thermal throttling), enerji
tüketimi artar ve donanım zarar görebilir. Bu proje, sıcaklık sensöründen gelen
veriyi **geri besleme (feedback loop)** olarak kullanan bir **kapalı döngü kontrol
algoritması** ile bu sorunu çözmeyi amaçlar.

## Nasıl Çalışır?

Sistem üç modülden oluşur:

| Modül | Rolü | Açıklama |
|-------|------|----------|
| Termal İzleme | Sensör | Anlık sıcaklığı hesaplar (ısınma − soğuma) |
| DFS Kontrol Ünitesi | Karar birimi | Sıcaklığı eşik değerlerle karşılaştırır |
| Frekans Yönetimi | Eyleyici | Frekansı 3000 MHz ↔ 1500 MHz arasında değiştirir |

```
Sıcaklık Sensörü → Karar Birimi (Algoritma) → Frekans Kontrolcüsü → CPU
        ↑                                                            |
        └──────────────── Sıcaklık geri beslemesi ───────────────────┘
```

**Algoritma mantığı:**
- Sıcaklık **85 °C** (kritik eşik) üzerine çıkarsa → frekans **1500 MHz**'e düşer
- Sıcaklık **60 °C** (güvenli eşik) altına inerse → frekans tekrar **3000 MHz**'e çıkar
- İki eşiğin farklı olması **histerezis** sağlar; sistem sürekli aç-kapa yapmaz

**Termal model:** Isınma çalışma frekansıyla doğru orantılıdır, soğuma Newton'un
Soğuma Yasası'na göre ortam sıcaklığı farkına bağlıdır.

## Sonuçlar

- Simülasyon süresi: 60 saniye
- Başlangıç: 47.7 °C, 3000 MHz
- 50. saniyede sıcaklık kritik eşiğe (85.5 °C) ulaştı, algoritma frekansı 1500 MHz'e çekti
- İşlemci tehlikeli sıcaklık bölgesine (90 °C) çıkmadı

<img width="244" height="319" alt="Resim1 1" src="https://github.com/user-attachments/assets/e6ae3595-49d9-4c40-8e8d-0321dadc9dcd" />
<img width="389" height="729" alt="Resim2 2" src="https://github.com/user-attachments/assets/0e726206-afad-4e01-9808-789523151d5c" />

![Sıcaklık Değişimi]
<img width="1656" height="899" alt="Resim3 3" src="https://github.com/user-attachments/assets/f8177cd0-67e5-4bcd-98f2-3d3b7b4ef695" />

## Kullanılan Teknolojiler

- Java
- Eclipse IDE
- Microsoft Excel (veri analizi ve grafik)

## Gelecek Çalışmalar

- Ani frekans düşüşü yerine **kademeli frekans ayarı** ile performans kaybını azaltmak
- Daha gelişmiş termal modeller (ör. HotSpot tarzı)
- PID kontrolcü ile karşılaştırma

## 📚 Kaynaklar

- Hennessy & Patterson (2017). *Computer Architecture: A Quantitative Approach*
- Brooks & Martonosi (2001). Dynamic thermal management
- Skadron et al. (2003). HotSpot thermal modeling

## Geliştirici

**Gökçenur Aksakal** – Bilgisayar Mühendisliği
[GitHub](https://github.com/gokceak29) 
