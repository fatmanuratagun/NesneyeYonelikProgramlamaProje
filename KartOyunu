using System;
using System.Collections.Generic;
using System.Linq;
using System.Media;
using System.Text;
using System.Threading;
using System.Threading.Tasks;

namespace KartOyunu
{
    internal class Program
    {

        public interface IOyun
        {
            void Baslat();
            void KartDagit(int kullaniciKart = 5, int bilgisayarKart = 5); 
        }

        public class Kart
        {
            public int Deger { get; private set; }

            public Kart(int deger)
            {
                Deger = deger;
            }

            public override string ToString()
            {
                return Deger.ToString();
            }
        }

        class Oyuncu
        {
            public string Isim { get; private set; }
            public List<Kart> El { get; private set; }
            public int KazanilanRaund { get; private set; }

            public Oyuncu(string isim)
            {
                Isim = isim;
                El = new List<Kart>();
                KazanilanRaund = 0;
            }

            public void KartEkle(Kart kart)
            {
                El.Add(kart);
            }

            public void KartCikar(Kart kart)
            {
                El.Remove(kart);
            }

            public void RaundKazan()
            {
                KazanilanRaund++;
            }

            public override string ToString()
            {
                return $"{Isim} - Kazanılan Raundlar: {KazanilanRaund}";
            }
        }

        public abstract class Oyun : IOyun
        {
            public static int ToplamOyunSayisi = 0;
            public static int ToplamKullaniciKazanim = 0;
            public static int ToplamBilgisayarKazanim = 0;
            public static int ToplamBeraberlik = 0;
            private Oyuncu kullanici;
            private Oyuncu bilgisayar;
            protected List<Kart> deste;
            protected Random rastgele;

            public Oyun()
            {
                rastgele = new Random();
                kullanici = new Oyuncu("Kullanıcı");
                bilgisayar = new Oyuncu("Bilgisayar");
                deste = new List<Kart>();

                // 20 kartlık deste oluştur
                for (int i = 1; i <= 10; i++)
                {
                    deste.Add(new Kart(i));
                    deste.Add(new Kart(i));
                }

                // Karıştır
                deste = deste.OrderBy(x => rastgele.Next()).ToList();
            }


            public abstract void Baslat();

            public virtual void KartDagit(int kullaniciKart = 5, int bilgisayarKart = 5)
            {
                for (int i = 0; i < kullaniciKart; i++)
                {
                    kullanici.KartEkle(deste[0]);
                    deste.RemoveAt(0);
                }

                for (int i = 0; i < bilgisayarKart; i++)
                {
                    bilgisayar.KartEkle(deste[0]);
                    deste.RemoveAt(0);
                }
            }

            public class KartliOyun : Oyun
            {
                public KartliOyun() : base() { }

                public override void Baslat()
                {
                    // Her yeni oyun başladığında toplam oyun sayısını artırıyoruz
                    ToplamOyunSayisi++;
                    BaslikYaz("KART OYUNUNA HOŞ GELDİNİZ!");
                    YavasYaz("Kartlar dağıtılıyor...\n");
                    Thread.Sleep(1000);

                    // Kart dağıtımı
                    KartDagit();

                    // Raundlar
                    for (int raund = 1; raund <= 5; raund++)
                    {
                        Console.WriteLine($"\n=== {raund}. RAUND ===");
                        RaundOyna();
                    }

                    // Sonuç
                    SonuclariGoster();
                }
            }

            private void RaundOyna()
            {
                Console.WriteLine("\nSizin Kartlarınız:");
                foreach (var kart in kullanici.El)
                {
                    KartCiz(kart.Deger);
                }

                // Kullanıcı kart seçimi
                Console.WriteLine("\nHangi kartı oynamak istersiniz? (1 - " + kullanici.El.Count + ")");
                int secim;
                while (!int.TryParse(Console.ReadLine(), out secim) || secim < 1 || secim > kullanici.El.Count)
                {
                    Console.WriteLine($"Geçerli bir kart seçiniz (1-{kullanici.El.Count}):");
                }

                Kart kullaniciKart = kullanici.El[secim - 1];
                kullanici.KartCikar(kullaniciKart);

                // Bilgisayar kart seçimi
                Kart bilgisayarKart = bilgisayar.El[rastgele.Next(0, bilgisayar.El.Count)];
                bilgisayar.KartCikar(bilgisayarKart);

                Console.WriteLine("\nSizin Kartınız:");
                KartCiz(kullaniciKart.Deger);
                Console.WriteLine("Bilgisayarın Kartı:");
                KartCiz(bilgisayarKart.Deger);

                // Karşılaştırma
                if (kullaniciKart.Deger > bilgisayarKart.Deger)
                {
                    Console.ForegroundColor = ConsoleColor.Green;
                    Console.WriteLine("Bu raundu kazandınız!");
                    Console.ResetColor();
                    kullanici.RaundKazan();
                }
                else if (bilgisayarKart.Deger > kullaniciKart.Deger)
                {
                    Console.ForegroundColor = ConsoleColor.Red;
                    Console.WriteLine("Bu raundu bilgisayar kazandı!");
                    Console.ResetColor();
                    bilgisayar.RaundKazan();
                }
                else
                {
                    Console.ForegroundColor = ConsoleColor.Yellow;
                    Console.WriteLine("Bu raund berabere!");
                    Console.ResetColor();
                }
            }

            private void SonuclariGoster()
            {
                Console.WriteLine("\n=== OYUN SONUCU ===");
                Console.WriteLine(kullanici);
                Console.WriteLine(bilgisayar);

                if (kullanici.KazanilanRaund > bilgisayar.KazanilanRaund)
                {
                    Console.ForegroundColor = ConsoleColor.Green;
                    Console.WriteLine("Tebrikler, oyunu kazandınız!");
                    // Alkış sesi
                    string alkisDosyasi = @"C:\\Users\\atagu\\Downloads\\applause-236785.wav";
                    SoundPlayer player = new SoundPlayer(@"C:\\Users\\atagu\\Downloads\\applause-236785.wav");
                    player.PlaySync();  // Alkış sesi çalıyor
                    ToplamKullaniciKazanim++;
                }
                else if (bilgisayar.KazanilanRaund > kullanici.KazanilanRaund)
                {
                    Console.ForegroundColor = ConsoleColor.Red;
                    Console.WriteLine("Maalesef, bilgisayar oyunu kazandı.");
                    //Kaybetme sesi
                    string KaybetmeDosyasi = @"C:\\Users\\atagu\\Downloads\\Aaa - Üzülme Ses Efekti.wav";
                    SoundPlayer player = new SoundPlayer(@"C:\\Users\\atagu\\Downloads\\Aaa - Üzülme Ses Efekti.wav");
                    player.PlaySync();  // Kaybetme sesi çalıyor
                    ToplamBilgisayarKazanim++;
                }
                else
                {
                    Console.ForegroundColor = ConsoleColor.Yellow;
                    Console.WriteLine("Oyun berabere!");
                    ToplamBeraberlik++;
                }
                Console.ResetColor();

                Console.WriteLine();
                Console.WriteLine("Yeni bir oyun başlatmak ister misiniz? (Evet - 'e' veya Hayır - 'h')");

                while (true)
                {
                    string cevap = Console.ReadLine().ToLower();

                    if (cevap == "evet" || cevap == "e")
                    {
                        Console.Clear();
                        Oyun yeniOyun = new KartliOyun();
                        yeniOyun.Baslat();
                        break;
                    }
                    else if (cevap == "hayır" || cevap == "h")
                    {
                        Console.WriteLine("Oyun sonlandırılıyor...");
                        Thread.Sleep(1000);
                        ToplamSonuclariGoster();
                        Console.ReadKey();
                        Environment.Exit(0);
                    }
                    else
                    {
                        Console.WriteLine("Geçersiz bir cevap girdiniz. Lütfen 'e' veya 'h' yazınız.");
                    }
                }
            }

            private static void ToplamSonuclariGoster()
            {
                Console.WriteLine("\n=== TOPLAM SONUÇLAR ===");
                Console.WriteLine($"Toplam Oyun Sayısı: {ToplamOyunSayisi}");
                Console.WriteLine($"Kullanıcı Kazandı: {ToplamKullaniciKazanim}");
                Console.WriteLine($"Bilgisayar Kazandı: {ToplamBilgisayarKazanim}");
                Console.WriteLine($"Beraberlik Sayısı: {ToplamBeraberlik}");
            }

            private void KartCiz(int deger)
            {
                Console.ForegroundColor = ConsoleColor.DarkRed;
                Console.WriteLine("┌───────┐");
                Console.WriteLine("|       |");
                Console.WriteLine("|       |");
                Console.WriteLine($"|  {deger.ToString().PadLeft(2, ' ')}   |");
                Console.WriteLine("|       |");
                Console.WriteLine("|       |");
                Console.WriteLine("└───────┘");
                Console.ResetColor();
            }

            private void BaslikYaz(string baslik)
            {
                Console.ForegroundColor = ConsoleColor.Black;
                Console.WriteLine(new string('=', baslik.Length + 4));
                Console.WriteLine($"| {baslik} |");
                Console.WriteLine(new string('=', baslik.Length + 4));
                Console.ResetColor();
            }

            private void YavasYaz(string mesaj, int gecikmeMs = 50)
            {
                foreach (char c in mesaj)
                {
                    Console.Write(c);
                    Thread.Sleep(gecikmeMs);
                }
                Console.WriteLine();
            }

            static void Main(string[] args)
            {
                Console.BackgroundColor = ConsoleColor.DarkGray;
                Console.ForegroundColor = ConsoleColor.White;

                Oyun oyun = new KartliOyun();
                oyun.Baslat();

                Console.ReadKey();
            }
        }
    }
}
