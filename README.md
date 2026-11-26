# Langflow Çalışma Projeleri

Langflow’u öğrenirken geliştirdiğim dört uygulama. Temel bir sohbet akışıyla başladım. Sonraki çalışmalarda şirket raporlarını özetleyen bir ajan kurdum, bir SQLite veritabanına doğal dille soru sordum ve yanıtları Telegram’a gönderdim. Son projede ise PDF’den ilgili metin parçalarını bulup bunlara dayanarak cevap veren bir RAG akışı oluşturdum.

## Akışlar

| Proje | Ne yapıyor? |
| --- | --- |
| [Chat Deneme](flows/Chat%20Deneme.json) | Kullanıcının mesajını bir prompt şablonuyla dil modeline iletir ve cevabı Playground’da gösterir. |
| [Şirket Raporu Özetleyici](flows/%C5%9Eirket%20Raporu%20%C3%96zetleyici.json) | Şirket raporundaki satış, kâr ve EBITDA gibi bilgileri tek paragrafta özetler. |
| [SQL ve Telegram](flows/Mini%20RAG-%20telegram.json) | Doğal dildeki soruyu SQL sorgusuna çevirir, sonucu anlaşılır bir dille yazar ve özel bir bileşenle Telegram’a gönderir. |
| [PDF RAG](flows/RAG%20Flow.json) | PDF’yi parçalara ayırıp FAISS’te indeksler. Soru geldiğinde ilgili parçaları bulur ve cevap üretmesi için modele verir. |

## Langflow’da deneme

1. Denemek istediğin JSON dosyasını indir ve Langflow’a içe aktar.
2. Akışta kullanacağın modeli ve API anahtarını kendi Langflow ortamında seç.
3. Projeye göre aşağıdaki ayarları tamamla ve **Playground**’da bir mesaj gönder.

### SQL ve Telegram

**SQL Database** bileşeninin bağlantı adresine kendi örnek SQLite veritabanını gir. Dersteki örnek, `products` tablosundaki `id` sütununu `orders` tablosundaki `product_id` ile eşleştiriyor. Bağlantıyı `SELECT * FROM orders;` ile kontrol edebilirsin.

**Telegram Sender** bileşenine bot tokenını ve sohbet kimliğini gir. Örnek soru olarak **“Hangi ürün hiç sipariş edilmemiş?”** yaz.

### PDF RAG

**Read File** bileşenine bir PDF yükle. Langflow’un Python ortamında `faiss-cpu` kurulu olmalı. İki FAISS bileşeninde aynı **Index Name** ve **Persist Directory** değerlerini kullan. Önce belgeyi indeksleyen FAISS bileşenini çalıştır, ardından Playground’da PDF’de cevabını bildiğin bir soru sor. FAISS indeks okuma iznini yalnızca kendi oluşturduğun ve kontrol ettiğin indeks için kullan.
