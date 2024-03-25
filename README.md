from datetime import datetime

class Lastik:
    def __init__(self, adet, olcu, mevsim, teslim_alma_tarihi, teslim_etme_tarihi, arac_bilgisi, raf_numarasi):
        self.adet = adet
        self.olcu = olcu
        self.mevsim = mevsim
        self.teslim_alma_tarihi = teslim_alma_tarihi
        self.teslim_etme_tarihi = teslim_etme_tarihi
        self.arac_bilgisi = arac_bilgisi
        self.raf_numarasi = raf_numarasi
        self.islem_tarihi = datetime.now().strftime("%Y-%m-%d %H:%M:%S")

class LastikDepo:
    def __init__(self):
        self.raf_sayisi = 2000
        self.raflar = {i: None for i in range(1, self.raf_sayisi + 1)}
        self.islem_gecmisi = []

    def lastik_ekle(self, lastik):
        if lastik.raf_numarasi in self.raflar.keys() and self.raflar[lastik.raf_numarasi] is None:
            self.raflar[lastik.raf_numarasi] = lastik
            self.islem_gecmisi.append(f"{lastik.adet} adet lastik, raf numarası {lastik.raf_numarasi}'de depoya eklendi. İşlem tarihi: {lastik.islem_tarihi}")
            print("Lastik başarıyla eklendi.")
        else:
            print("Belirtilen raf numarası uygun değil veya dolu.")

    def lastik_sil(self, raf_numarasi):
        if raf_numarasi in self.raflar.keys() and self.raflar[raf_numarasi] is not None:
            lastik = self.raflar[raf_numarasi]
            self.raflar[raf_numarasi] = None
            self.islem_gecmisi.append(f"{lastik.adet} adet lastik, raf numarası {lastik.raf_numarasi}'den silindi. İşlem tarihi: {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}")
            print("Lastik başarıyla silindi.")
        else:
            print("Belirtilen raf numarası uygun değil veya boş.")

    def lastikleri_listele(self):
        for raf_numarasi, lastik in self.raflar.items():
            if lastik is not None:
                print(f"\nRaf Numarası: {raf_numarasi}")
                print(f"Adet: {lastik.adet}")
                print(f"Ölçü: {lastik.olcu}")
                print(f"Mevsim: {lastik.mevsim}")
                print(f"Teslim Alma Tarihi: {lastik.teslim_alma_tarihi}")
                print(f"Teslim Etme Tarihi: {lastik.teslim_etme_tarihi}")
                print(f"Araç Bilgisi: {lastik.arac_bilgisi}")
                print(f"İşlem Tarihi: {lastik.islem_tarihi}")

    def gecmisi_goruntule(self):
        print("\nİşlem Geçmişi:")
        for islem in self.islem_gecmisi:
            print(islem)

def main():
    depo = LastikDepo()

    while True:
        print("\n1. Yeni Lastik Ekle")
        print("2. Lastikleri Listele")
        print("3. Lastik Sil")
        print("4. İşlem Geçmişini Görüntüle")
        print("5. Çıkış")
        secim = input("Seçiminizi yapınız: ")

        if secim == "1":
            adet = int(input("Adet: "))
            olcu = input("Ölçü: ")
            mevsim = input("Mevsim: ")
            teslim_alma_tarihi = input("Teslim Alma Tarihi: ")
            teslim_etme_tarihi = input("Teslim Etme Tarihi: ")
            arac_bilgisi = input("Araç Bilgisi: ")
            raf_numarasi = int(input(f"Raf numarası (1 - {depo.raf_sayisi}): "))

            lastik = Lastik(adet, olcu, mevsim, teslim_alma_tarihi, teslim_etme_tarihi, arac_bilgisi, raf_numarasi)
            depo.lastik_ekle(lastik)

        elif secim == "2":
            depo.lastikleri_listele()

        elif secim == "3":
            raf_numarasi = int(input(f"Silmek istediğiniz lastiğin raf numarası (1 - {depo.raf_sayisi}): "))
            depo.lastik_sil(raf_numarasi)

        elif secim == "4":
            depo.gecmisi_goruntule()

        elif secim == "5":
            print("Programdan çıkılıyor...")
            break

        else:
            print("Geçersiz seçim. Lütfen tekrar deneyin.")

if __name__ == "__main__":
    main()
