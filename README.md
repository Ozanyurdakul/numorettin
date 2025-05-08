def pisagor_tablosu():
    return {
        'A':1, 'B':2, 'C':3, 'Ç':3, 'D':4, 'E':5, 'F':8,
        'G':3, 'Ğ':3, 'H':5, 'I':1, 'İ':1, 'J':1, 'K':2,
        'L':3, 'M':4, 'N':5, 'O':7, 'Ö':7, 'P':8, 'R':9,
        'S':1, 'Ş':1, 'T':2, 'U':3, 'Ü':3, 'V':4, 'Y':7, 'Z':8
    }

def sayiya_cevir(metin):
    tablo = pisagor_tablosu()
    return [tablo[harf] for harf in metin.upper() if harf in tablo]

def basamaklara_ayir(sayi):
    while sayi > 9 and sayi not in [11, 22, 33]:
        sayi = sum(int(d) for d in str(sayi))
    return sayi

def isim_sayisi(isim_tam):
    sayilar = sayiya_cevir(isim_tam.replace(" ", ""))
    return basamaklara_ayir(sum(sayilar))

def ruh_sayisi(isim_tam):
    unlu_harfler = 'AEIİOÖUÜ'
    sayilar = sayiya_cevir(''.join(h for h in isim_tam.upper() if h in unlu_harfler))
    return basamaklara_ayir(sum(sayilar))

def kisilik_sayisi(isim_tam):
    sessiz_harfler = 'BCÇDFGĞHJKLMNPRSŞTVYZ'
    sayilar = sayiya_cevir(''.join(h for h in isim_tam.upper() if h in sessiz_harfler))
    return basamaklara_ayir(sum(sayilar))

def kader_sayisi(dogum_tarihi):
    sayilar = [int(c) for c in dogum_tarihi if c.isdigit()]
    return basamaklara_ayir(sum(sayilar))

def cakra_detay(cakra_no):
    cakralar = {
        1: {
            "ad": "1. Kök Çakra (Muladhara)",
            "renk": "Kırmızı",
            "duygu": "Kabul, güven, aidiyet",
            "element": "Toprak",
            "organlar": "Omurga, bacaklar, ayaklar, kalın bağırsak",
            "sorunlar": "Korku, güvensizlik, kabızlık, öfke, şiddet",
            "ifade": "İstiyorum"
        },
        2: {
            "ad": "2. Sakral Çakra (Svadhisthana)",
            "renk": "Turuncu",
            "duygu": "Yaratıcılık, zevk, değişim",
            "element": "Su",
            "organlar": "Üreme organları, böbrekler, mesane",
            "sorunlar": "Utanç, suçluluk, bastırılmış cinsellik",
            "ifade": "Arzuluyorum"
        },
        3: {
            "ad": "3. Solar Pleksus Çakrası (Manipura)",
            "renk": "Sarı",
            "duygu": "Özgüven, irade, kişisel güç",
            "element": "Ateş",
            "organlar": "Mide, karaciğer, pankreas",
            "sorunlar": "Öfke, değersizlik hissi, kontrol saplantısı",
            "ifade": "Hareket etmek istiyorum"
        },
        4: {
            "ad": "4. Kalp Çakrası (Anahata)",
            "renk": "Yeşil",
            "duygu": "Sevgi, empati, bağışlama",
            "element": "Hava",
            "organlar": "Kalp, akciğer, göğüs",
            "sorunlar": "Kıskançlık, yalnızlık, kalp rahatsızlıkları",
            "ifade": "Sevmek ve sevilmek istiyorum"
        },
        5: {
            "ad": "5. Boğaz Çakrası (Vishuddha)",
            "renk": "Mavi",
            "duygu": "İfade, dürüstlük, iletişim",
            "element": "Eter",
            "organlar": "Boğaz, tiroit, ses telleri",
            "sorunlar": "İfade edememe, boğaz rahatsızlıkları",
            "ifade": "Özgürce konuşmak istiyorum"
        },
        6: {
            "ad": "6. Üçüncü Göz Çakrası (Ajna)",
            "renk": "İndigo",
            "duygu": "Sezgi, içgörü, bilgelik",
            "element": "Işık",
            "organlar": "Gözler, alın, beyin",
            "sorunlar": "Kafa karışıklığı, baş ağrısı, hayal kuramama",
            "ifade": "Görmek istiyorum"
        },
        7: {
            "ad": "7. Taç Çakra (Sahasrara)",
            "renk": "Mor",
            "duygu": "Spiritüellik, birlik bilinci",
            "element": "Kozmik Enerji",
            "organlar": "Beyin, sinir sistemi",
            "sorunlar": "Anlam eksikliği, bağlantısızlık, depresyon",
            "ifade": "Olmak istiyorum"
        }
    }
    return cakralar.get(cakra_no, {})

def cakra_analizi_detayli(isim_sayi, ruh_sayi, kader_sayi):
    cakra_kod = (isim_sayi + ruh_sayi + kader_sayi) % 7
    cakra_kod = 7 if cakra_kod == 0 else cakra_kod
    return cakra_detay(cakra_kod)

def analiz_et():
    isim = input("İsim (varsa ikinci isim dahil): ")
    soyisim = input("Soyisim: ")
    dogum_tarihi = input("Doğum tarihi (GG.AA.YYYY): ")

    tam_ad = f"{isim} {soyisim}"
    i_sayi = isim_sayisi(tam_ad)
    r_sayi = ruh_sayisi(tam_ad)
    k_sayi = kisilik_sayisi(tam_ad)
    kader = kader_sayisi(dogum_tarihi)

    cakra = cakra_analizi_detayli(i_sayi, r_sayi, kader)

    print("\n--- NUMEROLOJİ ANALİZİ ---")
    print(f"İsim Sayısı: {i_sayi}")
    print(f"Ruh Sayısı: {r_sayi}")
    print(f"Kişilik Sayısı: {k_sayi}")
    print(f"Kader Sayısı: {kader}")

    print("\n🌀 ÇAKRA ANALİZİ 🌀")
    for k, v in cakra.items():
        print(f"{k}: {v}")

if __name__ == "__main__":
    analiz_et()
