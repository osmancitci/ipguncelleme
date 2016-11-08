# ipguncelleme
İp guncelleme

Evimizde - çalışma yerimizde, internete bağlı olan tek kart pc ( RaspberryPi, OrangePi vb ) veya bilgisayarımıza erişmek ve çeşitli işlemler yaptırmak isteriz.

Kullandığınız internet bağlantısının ip adresi sürekli değişiyor olabilir. İp adresinizi sürekli güncel olarak takip etmek için, dynamicDns veya benzeri bir hizmet kullanmalısınız.

Peki, kendinize ait bir hosting ( veya sunucu ) üzerinden sürekli değişen ip adresinizi takip etseniz daha iyi olmaz mı ?

Peki, nasıl olacak ? Genel olarak bu uygulamacık (script) ile şu şekilde gerçekleştirmiş olacağız;



Açık olan mini pc veya açık bilgisayarımızdan crontab-curl aracılığı ile hostinginizin bulunduğu makineye istek göndermek.
Hosting-Sunucunuz üzerinden, bu isteği karşılayıp, dinamik ip adresimizi txt dosyaya yazacak bir php dosyası oluşturmak !
Bu işlemlere başlamadan önce Raspberry Pi cihazınızı kullanıma hazır hale getirdiğinizi varsayıyoruz;

Hazırlık

pc ile cihazınıza ssh ile bağlandıktan sonra

cd /home/pi
"Ipguncelleme" repomuzu indirmek için git clone komutunu kullanıyoruz

git clone https://github.com/osmancitci/ipguncelleme.git

ipguncelleme isimli dizine giriyoruz.

cd ipguncelleme
scriptimize çalıştırma izni veriyoruz

chmod +x ip_guncelleme.sh

Kurulum

artık çalıştırabiliriz scriptimizi

sudo ./ip_guncelleme.sh
İlk soru site adresinizdir. İlla isim olmasına gerek yok ( http://178.187.871.718 ip de verebilirsiniz ) Site isminizi yazarken sonunda "/" karakteri olmasın. örn --> http://sitemiz.com

http://sitenizinadi.com
Raspberrypi den çıkacak olan istekleri karşılaması için bir php dosyası oluşturulacak. Bu php dosyasına tahmin edilemeyecek bir isim vermeniz çok önemli !

___ip_guncelleme.php
Son soruda, ip adresiniz kaç dakikada bir güncellensin. Yani, sahip olduğunu internetin dinamik ip bilgisi, ne kadar da bir kaydedilsin ? 30 dkk idealdir. Ama yapacağınız işin önemine binaen 5 dkk bile verebilirsiniz.

30

Kontrol ve Dosya upload

Raspberrypi de işlem doğru şekilde gerçeleşmiş mi kontrol !

sudo crontab -l
Eğer şu şekide bir çıktı var ise doğru demektir -->

"*/30 * * * * curl http://sitenizinadi.com/___ip_guncelleme.php >/dev/null 2>&1" Artık oluşturulan __ip_guncelleme.php dosyamızı, sunucumuza veya hosting alanımıza upload edebiliriz !

İşlemler bitti. Peki güncel ip adresimizi nasıl takip edeceğiz ?

  http://sitenizinadi.com/___ip_guncelleme.txt
Oluşturduğumuz php dosyası, aynı isimde yeni bir txt dosyası açar ve ip bilginizi bu txt dosyasına yazar. Sizde tarayıcınız vasıtası ile her yerden ( ister telefon isterseniz bilgisayarınız ) erişebilirsiniz !
