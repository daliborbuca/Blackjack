# Blackjack

import random

def deli_kartu():
  """Vraća nasumičnu kartu iz špila."""
  karte = [11, 2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10]
  karta = random.choice(karte)
  return karta

def izracunaj_rezultat(karte):
  """Uzima listu karata i vraća rezultat izračunat iz karata"""

  if sum(karte) == 21 and len(karte) == 2:
    return 0
  if 11 in karte and sum(karte) > 21:
    karte.remove(11)
    karte.append(1)
  return sum(karte)

def uporedi(rezultat_korisnika, rezultat_kompjutera):
  if rezultat_korisnika > 21 and rezultat_kompjutera > 21:
    return "Prešli ste. Izgubili ste 😤"

  if rezultat_korisnika == rezultat_kompjutera:
    return "Nerešeno 🙃"
  elif rezultat_kompjutera == 0:
    return "Izgubili ste, protivnik ima Blackjack 😱"
  elif rezultat_korisnika == 0:
    return "Pobedili ste sa Blackjack-om 😎"
  elif rezultat_korisnika > 21:
    return "Prešli ste. Izgubili ste 😭"
  elif rezultat_kompjutera > 21:
    return "Protivnik je prešao. Pobedili ste 😁"
  elif rezultat_korisnika > rezultat_kompjutera:
    return "Pobedili ste 😃"
  else:
    return "Izgubili ste 😤"

def igraj_igru():
  # Ovde bi išao ASCII art logo umesto komentara
  # print(logo)

  korisnicke_karte = []
  kompjuterske_karte = []
  igra_je_gotova = False

  for _ in range(2):
    korisnicke_karte.append(deli_kartu())
    kompjuterske_karte.append(deli_kartu())

  while not igra_je_gotova:
    rezultat_korisnika = izracunaj_rezultat(korisnicke_karte)
    rezultat_kompjutera = izracunaj_rezultat(kompjuterske_karte)
    print(f"   Vaše karte: {korisnicke_karte}, trenutni rezultat: {rezultat_korisnika}")
    print(f"   Prva karta kompjutera: {kompjuterske_karte[0]}")

    if rezultat_korisnika == 0 or rezultat_kompjutera == 0 or rezultat_korisnika > 21:
      igra_je_gotova = True
    else:
      korisnik_zeli_kartu = input("Ukucajte 'd' da dobijete još jednu kartu, 'n' da preskočite: ")
      if korisnik_zeli_kartu == "d":
        korisnicke_karte.append(deli_kartu())
      else:
        igra_je_gotova = True

  while rezultat_kompjutera != 0 and rezultat_kompjutera < 17:
    kompjuterske_karte.append(deli_kartu())
    rezultat_kompjutera = izracunaj_rezultat(kompjuterske_karte)

  print(f"   Vaš finalni skup karata: {korisnicke_karte}, finalni rezultat: {rezultat_korisnika}")
  print(f"   Finalni skup karata kompjutera: {kompjuterske_karte}, finalni rezultat: {rezultat_kompjutera}")
  print(uporedi(rezultat_korisnika, rezultat_kompjutera))

# Umesto replit.clear() možete koristiti print("\n"*100) kao jednostavnu alternativu za "čišćenje" konzole
while input("Želite li da igrate igru Blackjack? Ukucajte 'd' za da, 'n' za ne: ") == "d":
  # clear()
  print("\n"*100)  # Alternativa za clear() funkciju
  igraj_igru()
