Kart Oyunu - Konsol Uygulaması
Bu proje, konsol tabanlı bir kart oyunu uygulamasıdır. Oyuncu, bilgisayara karşı 5 raund boyunca kart seçerek yarışır ve sonuçlara göre oyun kazananı belirlenir.

Özellikler
  •	Oyuncu ve bilgisayar arasında rastgele kart dağıtımı.
  •	Kart seçimi sırasında kullanıcı etkileşimi.
  •	Her raundun kazananını belirlemek için kart değerlerinin karşılaştırılması.
  •	Oyun sonunda genel sonuçları ve toplam istatistikleri görüntüleme.
  •	Kullanıcıdan yeni bir oyun başlatma veya çıkış yapma seçeneği.

Oyun Akışı
  1. Oyun Başlangıcı:
    •	Başlangıç: Oyun başlar.
    •	Başlatma Mesajı: "KART OYUNUNA HOŞ GELDİNİZ!" başlık mesajı ekranda gösterilir.
    •	Kart Dağıtımı: Oyunun başında her iki oyuncuya (kullanıcı ve bilgisayar) 5'er kart dağıtılır.
  2. Raundlar:
    •	Raund Başlangıcı: 5 raund boyunca oyun devam eder. Her raund için aşağıdaki işlemler sırasıyla gerçekleştirilir.
    1.	Kullanıcı ve Bilgisayar Kart Seçimi:
       •	Kullanıcı Kartı Seçer: Kullanıcı, elindeki kartlar arasından bir kart seçer.
       •	Bilgisayar Kartı Seçer: Bilgisayar rastgele bir kart seçer.
    2.	Kartların Karşılaştırılması:
      •	Kart Değerleri Karşılaştırılır: Seçilen kartlar arasında değerler karşılaştırılır.
      •	Sonuç Durumu:
          •	Kullanıcı Kazanır: Kullanıcının kartı daha yüksekse, kullanıcı o raundu kazanır.
          •	Bilgisayar Kazanır: Bilgisayarın kartı daha yüksekse, bilgisayar o raundu kazanır.
          •	Beraberlik: Kartlar eşitse, o raund berabere olur.
    3.	Raund Sonucu:
      •	Kazanan belirlenir ve ekranda kullanıcıya bildirilir.
      •	Kazanan oyuncunun puanı (raund kazançları) bir artırılır.
    3. Oyun Sonu:
      •	Oyun Bitişi: 5 raund tamamlandıktan sonra oyun sona erer.
      •	Oyun Sonucu Gösterimi: Her iki oyuncunun (kullanıcı ve bilgisayar) kazandığı raundlar gösterilir.
      •	Kazananın Belirlenmesi:
          •	Kullanıcı Kazandıysa: Alkış sesi çalınır ve kullanıcı tebrik edilir.
          •	Bilgisayar Kazandıysa: Üzüntü sesi çalınır ve bilgisayarın kazandığı bildirilir.
          •	Beraberlik Durumu: Her iki oyuncu eşit sayıda raund kazandıysa oyun berabere biter.
    4. Tekrar Oyun Başlatma:
      •	Yeni Oyun İsteği: Kullanıcıya yeni bir oyun başlatmak isteyip istemediği sorulur.
          •	Evet (e): Yeni bir oyun başlatılır.
          •	Hayır (h): Oyun sonlandırılır ve toplam oyun sonuçları gösterilir.
    5. Toplam Sonuçlar:
      •	Sonuçların Gösterilmesi: Oyun sonunda toplamda kaç oyun oynandığı, kullanıcı ve bilgisayarın kazandığı oyun sayıları, beraberlik sayısı ekranda gösterilir.
