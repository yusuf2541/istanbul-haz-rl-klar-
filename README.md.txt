"""
İstanbul'un Fethi Simülatörü
Hazırlayan: (İsmini Yaz)
Açıklama:
Bu program, İstanbul'un fethiyle ilgili tarihî olayları, taktikleri, orduları,
stratejileri ve önemli gelişmeleri simüle eden uzun ve detaylı bir Python örneğidir.
Kod bolca yorum ve açıklama içerir.
"""

import time
import random

class Ordu:
    def __init__(self, isim, asker_sayisi, moral, teknoloji_seviyesi):
        self.isim = isim
        self.asker_sayisi = asker_sayisi
        self.moral = moral
        self.teknoloji = teknoloji_seviyesi

    def durum(self):
        print(f"\n[{self.isim} Durumu]")
        print(f"Asker Sayısı: {self.asker_sayisi}")
        print(f"Moral: {self.moral}")
        print(f"Teknoloji Seviyesi: {self.teknoloji}")

    def saldiri_gucu(self):
        return int(self.asker_sayisi * (self.moral / 100) * self.teknoloji)

class Surlar:
    def __init__(self, guc):
        self.guc = guc

    def durum(self):
        print(f"Surların Dayanıklılığı: {self.guc}")

    def zarar_al(self, miktar):
        self.guc -= miktar
        if self.guc < 0:
            self.guc = 0

class FetihSimulator:
    def __init__(self):
        self.osmanli = Ordu("Osmanlı Ordusu", 120000, 95, 1.3)
        self.bizans = Ordu("Bizans Ordusu", 7000, 85, 1.0)
        self.surlar = Surlar(100000)

    def bilgi_mesaji(self, mesaj):
        print("\n" + mesaj)
        time.sleep(0.8)

    def toplarla_saldiri(self):
        self.bilgi_mesaji("🔥 Şahi topları ateşleniyor!")
        zarar = random.randint(2000, 5000)
        self.surlar.zarar_al(zarar)
        print(f"Surlara {zarar} hasar verildi.")

    def gemileri_karadan_yurut(self):
        self.bilgi_mesaji("🚢 Gemiler karadan yürütülüyor... Haliç'e indiriliyor!")
        self.osmanli.moral += 10
        print("Osmanlı ordusunun morali arttı!")

    def genel_hucum(self):
        self.bilgi_mesaji("⚔️ Genel hücum başlıyor!")
        osmanli_gucu = self.osmanli.saldiri_gucu()
        bizans_gucu = self.bizans.saldiri_gucu()

        print(f"Osmanlı saldırı gücü: {osmanli_gucu}")
        print(f"Bizans savunma gücü: {bizans_gucu}")

        if osmanli_gucu > bizans_gucu:
            self.bilgi_mesaji("🏰 Osmanlı birlikleri surları aşıyor!")
            return True
        else:
            self.bilgi_mesaji("Bizans direnmeye devam ediyor... Saldırı başarısız.")
            return False

    def calistir(self):
        self.bilgi_mesaji("=== İstanbul'un Fethi Simülasyonu Başlıyor ===")

        # 1. Top atışları
        for _ in range(8):
            self.toplarla_saldiri()
            self.surlar.durum()

        # 2. Gemiler karadan yürütülüyor
        self.gemileri_karadan_yurut()

        # 3. Surlar zayıflayınca genel hücum
        if self.surlar.guc < 40000:
            kazandi = self.genel_hucum()

            if kazandi:
                self.bilgi_mesaji("🎉 İstanbul fethedildi!")
            else:
                self.bilgi_mesaji("Surlar aşılamadı, simülasyon başarısız.")
        else:
            self.bilgi_mesaji("Surlar hâlâ çok güçlü, hücum başarısız.")

if __name__ == "__main__":
    simulator = FetihSimulator()
    simulator.calistir()
