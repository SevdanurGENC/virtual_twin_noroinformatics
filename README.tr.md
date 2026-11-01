[English](README.md) | **Türkçe**

# Açık Bağlantıom Verisinden Tüm-Beyin Sanal İkizleri

[![Colab'da Aç](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/USERNAME/REPOSITORY/blob/main/sanal_ikiz_noroinformatik.ipynb)
![Python](https://img.shields.io/badge/python-3.10%2B-blue)
![Lisans](https://img.shields.io/badge/lisans-MIT-green)

> **[KARAR]** Colab rozetindeki ve aşağıdaki bağlantılardaki `USERNAME/REPOSITORY` kısmını kendi GitHub yolunuzla değiştirin ve lisansı seçin (kod için MIT öneriliyor; bkz. [Lisans](#lisans)).

Bu depo, aşağıdaki makalenin arkasındaki analizin tamamını, tekrarlanabilir biçimde içerir:

**"Tüm-Beyin Sanal İkizleri Kişiye Özgü mü? Açık Bağlantıom Verisinden Kanıtlar ve Türkiye'yi Kapsayan Bibliyometrik Bir Derleme"**
*(Journal of Computational Bioengineering and Clinical Medicine, JCBCM dergisine gönderilmiştir)*

Verinin yüklenmesi, modelleme, istatistik, tüm şekil ve tablolar ve bibliyometrik derleme dahil her şey, Türkçe adım adım açıklamalar içeren **tek bir Jupyter notebook'ta** çalışır. Her şekil 300 dpi çözünürlükte **hem Türkçe hem İngilizce** üretilir.

## Çalışmanın soruları

Bir *dijital ikiz* **kişiselleştirilmiş**, **veriyle güncellenen** ve **öngörü yapabilen** bir model olmalıdır. Yedi sağlıklı yetişkin için kişiye özel tüm-beyin modelleri kurduk ve bu özellikleri doğrudan sınadık:

| # | Soru | Notebook bölümü |
|---|------|-----------------|
| S1 | Kişinin kendi difüzyon MR bağlantıomuyla kurulan ikiz, o kişinin dinlenim-hali beyin aktivitesini yeniden üretip öngörebiliyor mu? | 5–6 |
| S2 | İkiz o kişiye **özgü** mü, yani başka birinin bağlantıomuyla kurulan ikizden daha mı iyi? | 7 |
| S3 | 80 kortikal bölgenin her birinde yapılan **sanal lezyon** ağ kırılganlığı hakkında ne gösteriyor? | 8 |
| Derleme | Beyin/nöro dijital ikiz araştırmaları dünyada ve Türkiye'de ne büyüklükte? (OpenAlex) | 9 |

## Ana bulgular

| Ölçü | Sonuç |
|---|---|
| Doğrudan yapı–işlev korelasyonu (SC–FC) | r = 0,263 ± 0,042 |
| Sanal ikiz ile ampirik FC | **r = 0,471 ± 0,115** (7 katılımcının 7'sinde daha iyi, p = 0,016) |
| Kaydın görülmemiş yarısının öngörülmesi | r = 0,455 (test-tekrar tavanının %69'u) |
| Karıştırılmış bağlantıom ikizi (sıfır modeli) | r = 0,065 |
| Kendi ikizi ile başkalarının ikizleri | Δr = −0,007, permütasyon p = 0,78 → **kişiye özgü değil** |
| Grup ortalaması bağlantıom ikizi | r = 0,495 |
| Sanal lezyon haritaları: güvenilirlik / düğüm gücüyle ilişki | ρ = 0,85 / ρ = 0,79 |
| OpenAlex beyin/nöro dijital ikiz yayınları (2015–2026) | 1.164 (kesinlik %96); Türkiye 12 yayınla 19. sırada |

**Ana mesaj:** Mekanistik beyin ikizleri insan bağlantıomunun *ortak* mimarisini yakalar ve zaman içinde genellenir; ancak kişiselleştirme **varsayılmamalı, gösterilmelidir**. Bölüm 7'deki çapraz uyum testi, bunu herhangi bir ikiz iş akışında yapmanın basit bir yoludur.

## Veri

- **Birincil kohort:** WU-Minn **Human Connectome Project (HCP)** kapsamındaki 7 sağlıklı yetişkin. Difüzyon traktografisinden yapısal bağlantı ve lif uzunluğu ile dinlenim-hali BOLD verisi (1.200 hacim, TR = 0,72 s); 80 kortikal AAL2 bölgesine parsellenmiştir.
- **Tekrar kohortu:** 5 katılımcı (yalnızca ampirik yapı–işlev korelasyonu için).
- Her iki kohort da açık kaynak [`neurolib`](https://github.com/neurolib-dev/neurolib) kütüphanesiyle dağıtılır ve otomatik yüklenir; **bu depoda veri saklanmaz**.
- **Bibliyometri:** [OpenAlex](https://openalex.org) API'sinden canlı çekilir (bu depodaki sonuçlara 1 Kasım 2026'da erişilmiştir).

HCP verisi: *Data were provided by the Human Connectome Project, WU-Minn Consortium (Principal Investigators: David Van Essen and Kamil Ugurbil; 1U54MH091657), funded by the 16 NIH Institutes and Centers that support the NIH Blueprint for Neuroscience Research, and by the McDonnell Center for Systems Neuroscience at Washington University.* HCP verilerinin kullanımı HCP Açık Erişim Veri Kullanım Koşullarına tabidir (bkz. [humanconnectome.org](https://www.humanconnectome.org)).

## Yöntem (özet)

Her bölge, çatallanma noktasının hemen altında (*a* = −0,02) çalışan bir **Stuart–Landau (Hopf) osilatörüdür**; içsel frekansı katılımcının kendi BOLD sinyalinden ölçülür. Bölgeler katılımcının kendi yapısal bağlantıomu üzerinden bağlanır; tek bir global bağlaşım *G*, ampirik fonksiyonel bağlantıya (0,04–0,07 Hz) göre her katılımcı için ayrı kalibre edilir. Doğrulamada fonksiyonel bağlantı dinamiği (FCD), zamansal çapraz doğrulama, permütasyon istatistiğiyle çapraz uyum özgüllük testi, kontrol ikizleri (grup ortalaması, yalnız yapı, yalnız ritim, karıştırılmış ağ) ve sanal lezyonlar için bağımsız tohum setleriyle güvenilirlik analizi kullanılır.

## Hızlı başlangıç

**Google Colab (önerilen):** Yukarıdaki rozete tıklayın, ardından *Çalışma zamanı → Tümünü çalıştır* deyin. İlk hücre `neurolib`'i kurar. Standart Colab CPU'sunda tam çalıştırma yaklaşık **40–50 dakika** sürer.

**Yerel bilgisayarda**

```bash
git clone https://github.com/USERNAME/REPOSITORY.git
cd REPOSITORY
pip install -r requirements.txt
jupyter notebook sanal_ikiz_noroinformatik.ipynb
```

### OpenAlex API anahtarı (ücretsiz)

Bölüm 9 OpenAlex'i sorgular. Colab'ın paylaşımlı IP adresleri anahtarsız kotayı sıkça doldurduğu için (HTTP 429) **ücretsiz** bir API anahtarı önerilir:

1. [openalex.org](https://openalex.org) adresinde ücretsiz hesap açın ve anahtarınızı *Settings → API* sayfasından kopyalayın.
2. Colab'da 🔑 **Secrets** panelini açın, `OPENALEX_API_KEY` adıyla anahtarı ekleyin ve notebook erişimini açın.

Anahtar ücretsizdir; ödeme bilgisi istenmez.

## Depo yapısı

```
├── sanal_ikiz_noroinformatik.ipynb   # analizin tamamı (Türkçe açıklamalı)
├── requirements.txt
├── sekiller/
│   ├── en/                           # 16 şekil, İngilizce, 300 dpi JPEG
│   └── tr/                           # 16 şekil, Türkçe, 300 dpi JPEG
├── ciktilar/                         # sonuç tabloları (CSV) ve OpenAlex sorgu sonuçları
├── README.md                         # İngilizce
└── README.tr.md                      # bu dosya (Türkçe)
```

## Tekrarlanabilirlik

- Tüm stokastik adımlar sabit tohumla başlar; aynı ortamda tekrar çalıştırmak aynı sayıları verir.
- Farklı kütüphane sürümleri yalnızca son basamakları değiştirebilir; sonuçlar etkilenmez.
- Bibliyometrik sayılar erişim tarihine bağlıdır; sorgu ifadeleri ve erişim tarihi sonuçlarla birlikte kaydedilir.
- Diğer araştırmacılar için not: Olasılıksal traktografide bağlantıomlar **tam yoğundur**; bu yüzden derece-korumalı yeniden bağlama yapılamaz ve notebook bunun yerine ağırlık karıştırma kullanır. Ayrıca sorguya *neural* kelimesini eklemek, "neural network" makalelerini yakaladığı için nöro dijital ikiz sayılarını yaklaşık yedi kat şişirir.

## Atıf

> **[KARAR]** Makale yayımlandığında atıf bilgisini ekleyin.

```bibtex
@article{AUTHOR2026virtualtwins,
  title   = {Are Whole-Brain Virtual Twins Personal? Evidence from Open Connectome Data and a Bibliometric Review including T{\"u}rkiye},
  author  = {AUTHOR, A. and AUTHOR, B.},
  journal = {Journal of Computational Bioengineering and Clinical Medicine},
  year    = {2026},
  note    = {Submitted}
}
```

Lütfen kullanılan araç ve verilere de atıf yapın: neurolib (Cakan ve ark., 2023, *Cognitive Computation*), Human Connectome Project (Van Essen ve ark., 2013, *NeuroImage*) ve OpenAlex (Priem ve ark., 2022).

## Lisans

> **[KARAR]** Öneri: kod (notebook) için **MIT**, şekil ve tablolar için **CC BY-NC 4.0** (JCBCM'nin kullandığı lisans). HCP verileri burada yeniden dağıtılmaz ve HCP Veri Kullanım Koşullarına tabi kalır.

## Üretken yapay zekâ kullanımı

Kodun taslağının hazırlanması ve hatalarının ayıklanması, hesaplanan sonuçlardan şekil ve tablo üretilmesi ve metin taslağı için bir yapay zekâ asistanı (Claude, Anthropic) kullanılmıştır. Tüm kod, sonuçlar ve kaynaklar yazarlar tarafından incelenmiş ve doğrulanmıştır.

## İletişim

> **[KARAR]** Sorumlu yazarın adı, kurumu ve e-posta adresi.
