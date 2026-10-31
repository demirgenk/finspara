[README.md](https://github.com/user-attachments/files/34227178/README.md)
# Finans Takip

Telefondan kullanılan, tek sayfalık kişisel finans takip uygulaması. Mevduat, kredi kartı, nakit, döviz ve altın varlıklarını tek yerde izler. Sunucu, hesap veya üyelik gerektirmez; tüm veriler yalnızca kullanıcının kendi telefonunda saklanır.

## Özellikler

**Hesap türleri**
- **Mevduat:** Faiz, vergi, vade ve başlangıç tarihine göre günlük/vade sonu net kazanç hesabı. Vadesi yaklaşan hesaplar renkle öne çıkar. Yenileme, kapatma ve başka bankaya taşıma desteklenir; kapanan mevduatların kazancı geçmişte saklanır.
- **Kredi kartı:** Hesap kesim ve son ödeme tarihleri, kalan gün rozetleri, "Ödendi" ile sonraki aya geçen döngülü kartlar ve taksit takibi.
- **Nakit:** Birikim hesabı (günlük net faiz) ve cüzdan.
- **Döviz ve altın:** Alış/satış kuru, orta kur üzerinden TL karşılığı, isteğe bağlı alış maliyeti ile kâr/zarar. Kurlar internetten otomatik çekilebilir veya elle girilebilir.

**Genel görünüm**
- Çok kişili kullanım (kişi bazlı süzme ve özet).
- Genel sekmesi üç görünüme ayrılır: Yaklaşan işlemler, Toplam para, Kişi özeti.
- Toplam kartının rengi 7 seçenekten seçilebilir.
- Gizlilik modu: tek dokunuşla tüm tutarlar gizlenir.
- Açık ve koyu tema uyumu.

**Kontrol sekmesi**
- Günlük otomatik kayıtlarla 7/15/30 gün karşılaştırması.
- Aylık özet: faiz geliri, kart ödemeleri, varlık değişimi.

**Güvenlik ve yedek**
- PIN ile ekran kilidi (4-6 hane, güvenlik sorusuyla sıfırlama).
- JSON yedek alma ve geri yükleme, isteğe bağlı şifreli yedek (AES-256).
- Yedeği WhatsApp, Drive gibi uygulamalara paylaşma ve yedek hatırlatması.

## Kurulum (GitHub Pages)

1. Bu depodaki dosyaları herkese açık bir GitHub deposuna yükleyin.
2. **Settings > Pages** bölümünde **Deploy from a branch** seçin, branch olarak `main` ve `/ (root)` belirleyin.
3. Birkaç dakika sonra uygulama `https://KULLANICI_ADI.github.io/DEPO_ADI/` adresinde yayında olur.
4. Telefonda Chrome (Android) ile adresi açın, menüden **Uygulamayı yükle** veya **Ana ekrana ekle** deyin.

Uygulama bir kez açıldıktan sonra internetsiz de çalışır.

## Güncelleme

1. Yeni `index.html` ve `sw.js` dosyalarını depoya yükleyin (**Add file > Upload files**) ve **Commit changes** deyin.
2. Telefonda uygulamayı kapatıp iki kez açın. Başlığın altında görünen sürüm numarası yeni sürümü doğrular.

Uygulama dosyasını değiştirdiğinizde `sw.js` içindeki `CACHE` sürüm numarasını artırın; telefonlar eski önbelleği bu sayede bırakır.

## Dosyalar

| Dosya | Açıklama |
| --- | --- |
| `index.html` | Uygulamanın tamamı (arayüz, hesaplamalar, veri saklama) |
| `sw.js` | Service worker: uygulamayı önbelleğe alır, internetsiz açılışı sağlar |
| `manifest.json` | Ana ekrana kurulum bilgileri (ad, renk, simgeler) |
| `icon-192.png`, `icon-512.png`, `icon-512-maskable.png` | Uygulama simgeleri |

## Gizlilik

- Veriler yalnızca cihazın tarayıcı deposunda (`localStorage`) tutulur. Hiçbir sunucuya gönderilmez.
- Depoda yalnızca uygulama kodu bulunur; kişisel veriler depoya yüklenmez.
- Kur güncellemesi dışında uygulama ağ isteği yapmaz.
- PIN yalnızca ekranı kilitler, tarayıcı verisini şifrelemez. Yedek dosyasını korumak için yedek alırken şifre kullanın.

## Önemli notlar

- **Yedek alın.** Tarayıcı verisi (site verileri/çerezler) temizlenirse veya uygulama kaldırılırsa kayıtlar silinebilir. Önemli değişikliklerden sonra şifreli yedeği kendinize gönderin. Uygulama 3 günden eski yedekte hatırlatma gösterir.
- **Adres bazlı veri.** Tarayıcı verisi adres bazlı saklanır. Uygulamayı yeni bir adrese taşırsanız yedekle aktarmanız gerekir.
- **Uygulama kapalıyken bildirim yoktur.** Uyarılar (yaklaşan vade, son ödeme) uygulama açıldığında gösterilir.
- **Faiz ve kazanç hesapları bilgilendirme amaçlıdır.** Hesaplar girilen oran, vergi ve tarihlere göre yapılır; bankanın fiilen yatırdığı tutardan küçük farklar olabilir.
- Finansal veya yatırım tavsiyesi değildir.

## Teknik özet

Tek dosyalık HTML, CSS ve JavaScript; harici kütüphane veya derleme adımı yoktur. Veri `localStorage` içinde, yedek şifreleme Web Crypto API (PBKDF2 + AES-GCM) ile yapılır. Kurulabilir web uygulaması (PWA) olarak çalışır.
