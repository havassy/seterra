# Seterra Eredmény Ellenőrző
Az alábbi leírást MI generálta, fejlesztő ellenőrizte és javította.

## 📋 Miről szól ez a program?

Ez egy **offline, webes alkalmazás** pedagógusok számára, amely automatikusan párosítja az osztálynévsor neveit a Seterra földrajzi vetélkedő eredményeivel.

## 🎯 Mi a célja?

A Seterra játékban a diákok gyakran nem teljes nevüket írják be (pl. csak keresztnevet, becenevet, vagy egybeírva). Ez a program **intelligens algoritmussal** automatikusan megtalálja, hogy ki kicsoda, és átlátható táblázatba rendezi az eredményeket.

## ⚙️ Hogyan működik?

1. **Bemenet**: Bemásolod az osztálynévsort és a Seterra eredménylistát
2. **Feldolgozás**: A program intelligens név-párosítással összepárosítja őket
3. **Kimenet**: Táblázat formában látod az eredményeket, amit letölthetsz Excel-kompatibilis CSV formátumban

### Intelligens párosítás
- **Vezetéknév ellenőrzés**: Ha van vezetéknév, szigorúan ellenőrzi
- **Rugalmas keresztnév párosítás**: Ha csak keresztnevet írtak be, megkeresi a megfelelő nevet
- **Egyszer-használat**: Egy diák neve csak egyszer jelenik meg a táblázatban
- **Párosítatlan nevek jelzése**: Ha egy nevet nem tud párosítani, külön jelzi a táblázat alján

## 🔒 Adatvédelem

- ✅ **100% offline működés** - Nincs internet szükséges (első megnyitás után)
- ✅ **Nincs adatküldés** - Az adatok NEM hagyják el a gépet
- ✅ **Teljes adatbiztonság** - Minden a böngésződben fut lokálisan
- ✅ **GDPR-kompatibilis** - Személyes adatok teljes kontrollja

## 🚀 Használat

1. Töltsd le az index.html` fájlt
2. Nyisd meg bármely modern böngészőben (Chrome, Firefox, Edge, Safari)
3. Másold be az eredeti osztálynévsort (minden név külön sorba)
4. Másold be a Seterra eredményeket
5. Kattints a "Táblázat készítése" gombra
6. Letöltheted az eredményt CSV formátumban

## 📊 Kimenet

A program egy táblázatot generál:
- **Első oszlop**: Eredeti osztálynévsor
- **További oszlopok**: 1-3 feladatlista eredményei
- **Párosítatlan nevek**: A táblázat alján, piros háttérrel jelezve

## 💡 Tippek

- Ha egy név nem párosul automatikusan (< 90% egyezés), a táblázat alján megjelenik
- A duplikált nevek "2x", "3x" jelöléssel vannak ellátva
- A CSV fájl megnyitható Excel-ben és Google Sheets-ben is

## 🛠️ Technikai részletek

- Tiszta HTML + JavaScript (vanilla JS)
- Nincs külső függőség
- Fájlméret: ~36 KB
- Kompatibilis: Minden modern böngésző

## 📄 Licence

MIT License - Szabadon használható oktatási célokra.

## 🤝 Közreműködés

Ha hibát találsz vagy új funkciót javasolnál, írj e-mailt: havassy@budai-rfg.hu.

---

**Készítette**: Havassy András (földrajz tanár)  
**Verzió**: 1.0  
**Utolsó frissítés**: 2025. december
