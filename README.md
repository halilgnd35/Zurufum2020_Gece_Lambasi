# Zurufum2020_Gece_Lambasi
Kart çizimi dahil olmak üzere her şeyi el emeğim olan gece lambasının ruhu olan kodlar.Youtube kanalımdan izleyebilirsiniz.
Youtube kanalım-> https://www.youtube.com/channel/UCrHQlXOK2GSIDMV41BJtEaQ
```javascript
------------------------------Kodlar------------------------------
//Zürüfüm2020-Gece lambası kodları
//Author:Halil
#include<IRremote.h>
#include<math.h> //parti modunu yazarken kullanılan sin fonksiyonu için lazım
#define pin0 0xFF9867//uzaktan kumanda üzerindeki tuşların tanımlanması
#define pin1 0xFFA25D
#define pin2 0xFF629D
#define pin3 0xFFE21D
#define pin4 0xFF22DD
#define pin5 0xFF02FD
#define pin6 0xFFC23D
#define pin7 0xFFE01F
#define pin8 0xFFA857
#define pin9 0xFF906F
#define pinasterix 0xFF6897// * tuşu
#define pinhash 0xFFB04F// # tuşu
#define pinok 0xFF38C7//orta tuş
#define pinup 0xFF18E7//yukarı
#define pind 0xFF4AB5//aşağı
#define pinr 0xFF5AA5//sağ
#define pinl 0xFF10EF//sol
#define pintkr 0xFFFFFF//herhangi bi tuşa basılı tutulunca bu kod gönderiliyo
#define irpin 7//kızıl ötesi alıcının bağlandığı pini tanımlama
#define r_com 5//köşedeki rgb ledler
#define g_com 6
#define b_com 9
#define r_tek 2//ortadaki rgb led
#define g_tek 3
#define b_tek 4
#define tek 1//ilerde bir kodda kullanılması için yazıldı yeri gelince açıklanacak
#define cift 2
short int renk_tek;//ilerde bir kodda kullanılması için yazıldı yeri gelince açıklanacak
short int renk_com;
IRrecv irrecv(irpin);
//aşağıda set_renginbaşharfi(x) şeklinde fonskiyonlar var x eğer 1 olursa ortadaki rgb ledi 
//eğer 2 olursa köşedeki rgb ledleri istenen renge ayarlar
// void loop kısmında fonksiyon kullanılırken 1 ve 2 kullanmak yerine yukarda tanımlanan tek ve cift değişkenlerini kullandım
//karışıklık olmasın diye yaptım ama gerek yoktu
void set_k(int x)//koddanda anlaşılacağı gibi istenen rgb ledi kırmızıya çevirir
{
  if (x == 1)
  {
    digitalWrite(g_tek, LOW);
    digitalWrite(b_tek, LOW);
    digitalWrite(r_tek, HIGH);
    renk_tek = 1;
    //tüm set_renk(x) fonksiyonlarında renk_tek ve renk_çift tanımlamalarını 0 dan 7ye kadar görüceksin
    //bunlar ilerde arduinonun hangi rgbnin hangi renkte yandığını anlaması için kullanıldı
    //ilerdeki başka fonksiyonlarda kullanılıcak
  }
  else if (x == 2)
  {
    digitalWrite(g_com, LOW);
    digitalWrite(b_com, LOW);
    digitalWrite(r_com, HIGH);
    renk_com = 1;
  }
}
void set_y(int x)//istenen rgb yi yeşile çevirir
{
  if (x == 1)
  {
    digitalWrite(g_tek, HIGH);
    digitalWrite(b_tek, LOW);
    digitalWrite(r_tek, LOW);
    renk_tek = 2;
  }
  else if (x == 2)
  {
    digitalWrite(g_com, HIGH);
    digitalWrite(b_com, LOW);
    digitalWrite(r_com, LOW);
    renk_com = 2;
  }
}
void set_ma(int x)//istenen rgbyi maviye çevirir
{
  if (x == 1)
  {
    digitalWrite(g_tek, LOW);
    digitalWrite(b_tek, HIGH);
    digitalWrite(r_tek, LOW);
    renk_tek = 3;
  }
  else if (x == 2)
  {
    digitalWrite(g_com, LOW);
    digitalWrite(b_com, HIGH);
    digitalWrite(r_com, LOW);
    renk_com = 3;
  }
}
void set_s(int x)//istenen rgbyi sarıya çevirir
{
  if (x == 1)
  {
    digitalWrite(g_tek, HIGH);
    digitalWrite(b_tek, LOW);
    digitalWrite(r_tek, HIGH);
    renk_tek = 4;
  }
  else if (x == 2)
  {
    digitalWrite(g_com, HIGH);
    digitalWrite(b_com, LOW);
    digitalWrite(r_com, HIGH);
    renk_com = 4;
  }
}
void set_mo(int x)//istenen rgbyi mora çevirir
{
  if (x == 1)
  {
    digitalWrite(g_tek, LOW);
    digitalWrite(b_tek, HIGH);
    digitalWrite(r_tek, HIGH);
    renk_tek = 6;
  }
  else if (x == 2)
  {
    digitalWrite(g_com, LOW);
    digitalWrite(b_com, HIGH);
    digitalWrite(r_com, HIGH);
    renk_com = 6;
  }
}
void set_t(int x)//istenen rgbyi turuncuya çevirir
{
  if (x == 1)
  {
    digitalWrite(g_tek, HIGH);
    digitalWrite(b_tek, HIGH);
    digitalWrite(r_tek, LOW);
    renk_tek = 5;
  }
  else if (x == 2)
  {
    digitalWrite(g_com, HIGH);
    digitalWrite(b_com, HIGH);
    digitalWrite(r_com, LOW);
    renk_com = 5;
  }
}
void set_b(int x)//istenen rgbyi beyaza çevirir
{
  if (x == 1)
  {
    digitalWrite(g_tek, HIGH);
    digitalWrite(b_tek, HIGH);
    digitalWrite(r_tek, HIGH);
    renk_tek = 0;
  }
  else if (x == 2)
  {
    digitalWrite(g_com, HIGH);
    digitalWrite(b_com, HIGH);
    digitalWrite(r_com, HIGH);
    renk_com = 0;
  }
}
void set_off(int x)//istenen rgbyi söndürür
{
  if (x == 1)
  {
    digitalWrite(g_tek, LOW);
    digitalWrite(b_tek, LOW);
    digitalWrite(r_tek, LOW);
    renk_tek = 7;
  }
  else if (x == 2)
  {
    digitalWrite(g_com, LOW);
    digitalWrite(b_com, LOW);
    digitalWrite(r_com, LOW);
    renk_com = 7;
  }
}
//aşağıda kumandanın yukarı aşağı tuşlarını kullanarak ortadaki tek rgb ledin 0dan 7ye kadar tanımladığımız renkleri arasında geçiş yapıcak fonskiyonlar
void Ch_tekclr_plus(void)//yukarı tuş için fonksiyon
{
  if (renk_tek == 7)//eğer 7. moddaysa 8. mod olmadığı ve bir arttırıldığında modun 0 olmasını istediğim için
    renk_tek = 0;// eğer 7. moddaysa bir arttırılınca 0 olmasını ayarladım
  else
    renk_tek += 1;// 0 dan 7ye kadar yukarı tuşa basılınca modu bir arttırma komudu
}
void Ch_tekclr_minus(void)//aşağı tuş için fonksiyon
{
  if (renk_tek == 0)//aynı şeylerin tam tersi burası için geçerli
    renk_tek = 7;
  else
    renk_tek -= 1;
}
//yukarıdaki ortadaki led içindi bu da kenardaki ledler için aynısı kopyala yapıştır yaptım :D
void Ch_comclr_plus(void)
{
  if (renk_com == 7)
    renk_com = 0;
  else
    renk_com += 1;
}
void Ch_comclr_minus(void)
{
  if (renk_com == 0)
    renk_com = 7;
  else
    renk_com -= 1;
}
//yukarıdaki fonksiyonlarda renk_tek ve renk_cift değişkenlerini değiştirip modlar arasında geçiş yaptık ama hiçbişeyin rengini değiştirmedik
//şimdi aşağıda yukarda değişen modlara göre renkler değişicek
void Ch_clr_tek(void)
{
  if (renk_tek == 0)
    set_b(tek);
  else if (renk_tek == 1)
    set_k(tek);
  else if (renk_tek == 2)
    set_y(tek);
  else if (renk_tek == 3)
    set_ma(tek);
  else if (renk_tek == 4)
    set_s(tek);
  else if (renk_tek == 5)
    set_t(tek);
  else if (renk_tek == 6)
    set_mo(tek);
  else if (renk_tek == 7)
    set_off(tek);
}
void Ch_clr_com(void)
{
  if (renk_com == 0)
    set_b(cift);
  else if (renk_com == 1)
    set_k(cift);
  else if (renk_com == 2)
    set_y(cift);
  else if (renk_com == 3)
    set_ma(cift);
  else if (renk_com == 4)
    set_s(cift);
  else if (renk_com == 5)
    set_t(cift);
  else if (renk_com == 6)
    set_mo(cift);
  else if (renk_com == 7)
    set_off(cift);
}
decode_results results;
void setup() {
  irrecv.enableIRIn();
  pinMode(r_tek, OUTPUT);
  pinMode(g_tek, OUTPUT);
  pinMode(b_tek, OUTPUT);
  pinMode(r_com, OUTPUT);
  pinMode(g_com, OUTPUT);
  pinMode(b_com, OUTPUT);
}

void loop() {
  if (irrecv.decode(&results))//eğer bir kod alındıysa
  {
    //alınan kodun ne olduğuna göre belli işlemler yapıcak
    irrecv.resume();//yeni bir kod almak için hafızada yer aç(klasik ır led fonksiyonları)
    if (results.value == pin1)//kumandadaki 0dan 9a kadar olan tuşlara isteğime göre bazı hazır led pozisyonları atadım
    {
      set_k(tek);
      set_b(cift);
    }
    else if (results.value == pin2)
    {
      set_s(tek);
      set_k(cift);
    }
    else if (results.value == pin3)
    {
      set_k(tek);
      set_s(cift);
    }
    else if (results.value == pin4)
    {
      set_k(tek);
      set_k(cift);
    }
    else if (results.value == pin5)
    {
      set_y(tek);
      set_y(cift);
    }
    else if (results.value == pin6)
    {
      set_ma(tek);
      set_ma(cift);
    }
    else if (results.value == pin7)
    {
      set_t(tek);
      set_t(cift);
    }
    else if (results.value == pin8)
    {
      set_mo(tek);
      set_mo(cift);
    }
    else if (results.value == pin9)
    {
      set_s(tek);
      set_s(cift);
    }
    else if (results.value == pin0)
    {
      set_b(tek);
      set_b(cift);
    }
    else if (results.value == pinup)//eğer yukarı tuşa basılmışsa ortadaki rgb ledi değiştirmek için gerekli fonksiyonları çağırır
    {
      Ch_tekclr_plus();//bu fonksiyon açıklandığı gibi sadece modu değiştirir
      Ch_clr_tek();//bu da değişen moda uygun şekilde renkleri değiştirir
    }
    else if (results.value == pind)//aşağı tuş için
    {
      Ch_tekclr_minus();
      Ch_clr_tek();
    }
    else if (results.value == pinr)//sağ tuş
    {
      Ch_comclr_plus();
      Ch_clr_com();
    }
    else if (results.value == pinl)//sol tuş
    {
      Ch_comclr_minus();
      Ch_clr_com();
    }
    else if (results.value == pinasterix)//eğer * tuşuna basılırsa tüm rgbler sönsün komutu
    {
      set_off(cift);
      set_off(tek);
    }
    else if (results.value == pinok)//burası biraz karmaşık eğer ortadaki tuşa basılırsa ortadaki rgb ledin rengi sabitlenir
    //kenardaki dans etmeye başlar
    {
      set_off(cift);//öncelikle kenardaki ledler yanıyosa söndürülür
      bool volume;//gerektiğinde açıklanıcak
      bool main = true;//gerektiğinde açıklanıcak
      long double i = 0;//burada i j ve k 3 farklı değişkeni ifade ediyo bunların amacı sin() fonksiyonunun içine girip
      long double j = (2 * PI) / 3;//hatırlamadığım bir derste gördüğümüz aralarında 2pi/3 kadar faz farkı olan sinüs dalgalarını oluşturucak
      long double k = (4 * PI) / 3;//buda kırmızı yeşil ve mavi arasında ara renkleri kullanarak tatlı bir geçiş sağlıyıcak
      long int sindegeri;//sinüs fonksiyonun giren i j k nın sayısal olarak değeri mesela i=pi değerindeyken sin(i)=0 olacak
      long int sindegerj;//sin fonskiyonundan dolayı sayılar -1le 1 arasında olucak ama arduinonun içinde 8bitlik adc olduğu için
      long int sindegerk;//arduinoya bu değerleri vermeden 0 ile  255 arasına çekmek gerekir bu aralğa çekilen değerleri bu değişkenler tutar
      short int del = 10;//renkler arasındaki geçişin hızını tutan değişken ya da yavaşlığını mı demeliyim işte
      while (1)
      {
        if (irrecv.decode(&results))
        {
          delay(1);
          irrecv.resume();
          if (results.value == pinhash)//main değişkeninin içinde true değeri varken ledler kırmızı yeşil mavi arasında geçiş yapar
            main = !main;//eğer # tuşuna basılırsa main değişkeni false olur ve geçiş artık turquaz mor ve sarı arasında yapılır
          else if (results.value == pinasterix)//eğer * tuşuna basılırsa ledlerin hepsi kapanır ve döngü kırılıp parti modundan çıkılır
          {
            set_off(cift);
            set_off(tek);
            break;
          }
          else if (results.value == pinl)//televizyonlardaki ses kısıp mantığına benzer bir şekilde renk geçiş hızını ayarlar
          {
            if (del < 100)
            {
              del += 1;
              volume = false;//bu değişken sesin kısılıyomu yoksa açılıyomu olduğunu anlamak için kullanıldı
            }
          }
          else if (results.value == pinr)
          {
            if (del >= 2)
              del -= 1;
            volume = true;
          }
          if (results.value == pintkr)
          {
            if (volume == true)//eğer ses kısılıyosa ve ya açılıyosa tuşa tekrar tekrar basmak yerine basılı tutarak kullanılması için yazıldı
            //ama nedense iş yapmıyor
            {
              if (del > 1)
                del -= 1;
            }
            else if (volume == false)
            {
              if (del < 100)
                del += 1;
            }
          }
        }
        i = i + PI / 500;//eğer bir tuşa baılmamışsa parti modu devam ediyodur ve her seferinde değişkenler kendilerini pi/500 değeri kadar artırır
        j = j + PI / 500;//bu değer tamamen deneyseldir oturup işlem yapmadım denedim ve güzel oldu
        k = k + PI / 500;
        sindegeri = 255 * (sin(i));//burada map komutu da kullanılabilirdi ama o an aklıma gelmedi sinüsün -1le 1 arasındaki değerini
        sindegerj = 255 * (sin(j));//-255 ile 255 arasına çekildi
        sindegerk = 255 * (sin(k));
        if (main == true)//burada kırmızı-yeşil mavi mi yoksa turquaz-mor-sarı arasında  ı geçiş yapılacağı kontrol ediliyo
        {
          if (sindegeri >= 0)//burada halili araman şiddetle tavsiye edilir ama yinede açıklamaya çalışayım
            analogWrite(r_com, sindegeri);
          if (sindegerj >= 0)//120 derece faz farklı 3lü sinüs dalgasının sadece pozitif kısmını istiyoruz bunu çizerek görmeye çalışabilirsim
            analogWrite(g_com, sindegerj);
          if (sindegerk >= 0)//bunları yaparken kağıt üzerine çizip baya kafa patlatmıştım
            analogWrite(b_com, sindegerk);
        }
        else if (main == false)//aynı şekilde turquaz mor sarı için
        {
          if (sindegeri >= 0)
            analogWrite(r_com, 255 - sindegeri);
          if (sindegerj >= 0)
            analogWrite(g_com, 255 - sindegerj);
          if (sindegerk >= 0)
            analogWrite(b_com, 255 - sindegerk);
        }
        delay(del);//renkler arasındaki geçiş hızını ayarlar
      }
    }
    delay(20);//bir probleme yol açmamak arduinoya dinlenme süresi
  }
}
```
