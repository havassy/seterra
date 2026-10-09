# Seterra Eredmény Ellenőrző
Az útmutató kizárólag semleges névhelyettesítőket használ.

## 📋 Miről szól ez a program?

Ez egy **offline, webes alkalmazás** pedagógusok számára, amely automatikusan párosítja az osztálynévsor neveit a Seterra földrajzi vetélkedő eredményeivel.

## 🎯 Mi a célja?

A Seterra játékban a diákok gyakran nem teljes nevüket írják be, mert **a Seterra nem enged szóközt**! Így kreatívan kell beírniuk:
- **Egybeírva:** `vezeteknevkeresztnev`, `masikvezeteknevmasikkeresztnev`
- **CamelCase:** `VezetéknévKeresztnév`, `VezetéknévKeresztnévMásodiknév`
- **Pont:** `Vezetéknév.Keresztnév`, `MásikVezetéknév.MásikKeresztnév`

Ez a program **intelligens algoritmussal** automatikusan megtalálja, hogy ki kicsoda, és átlátható táblázatba rendezi az eredményeket.

## ⚙️ Hogyan működik?

1. **Bemenet**: Bemásolod az osztálynévsort és a Seterra eredménylistát (1-3 lista)
2. **Feldolgozás**: A program intelligens név-párosítással összepárosítja őket
3. **Kimenet**: Táblázat formában látod az eredményeket
4. **Export**: Letöltheted Excel (XLSX) vagy CSV formátumban

### Intelligens párosítás
- **Teljes név egyezés (85%)**: Egybeírt, kisbetűs nevek felismerése
- **Vezetéknév ellenőrzés (88%)**: Ha van vezetéknév, szigorúan ellenőrzi
- **Keresztnév párosítás (90%)**: Ha csak keresztnevet írtak be, megkeresi a megfelelő nevet
- **CamelCase felismerés**: `VezetéknévKeresztnév`, `Vezetéknév-KeresztnévMásodiknév` automatikus szétbontása
- **Egyszer-használat**: Egy diák neve csak egyszer jelenik meg a táblázatban (greedy matching)
- **Párosítatlan nevek jelzése**: Ha egy nevet nem tud párosítani, külön jelzi a táblázat alján
- **Vesszős nevek detektálása**: Ha valaki két nevet írt be vesszővel (`név1,név2`), külön jelzi 📝

## 🔒 Adatvédelem

- ✅ **100% offline működés** - Első megnyitás után internet NEM szükséges (SheetJS cache-elődik)
- ✅ **Nincs adatküldés** - Az adatok NEM hagyják el a gépet
- ✅ **Teljes adatbiztonság** - Minden a böngésződben fut lokálisan
- ✅ **GDPR-kompatibilis** - Személyes adatok teljes kontrollja

## 🚀 Használat

### Első használat (internettel):
1. Töltsd le a `seterra-ellenorzo.html` fájlt
2. Nyisd meg **internetkapcsolattal** először (SheetJS könyvtár betöltődik)
3. A böngésző cache-eli → **utána offline is használható**!

### További használat (offline is működik):
1. Nyisd meg bármely modern böngészőben (Chrome, Firefox, Edge, Safari)
2. Másold be az eredeti osztálynévsort (minden név külön sorba)
3. Másold be a Seterra eredményeket (1-3 feladatlista)
4. Kattints a "Táblázat készítése" gombra
5. Letöltheted az eredményt XLSX vagy CSV formátumban

## 📥 Export opciók

### Excel (XLSX) - Ajánlott! ⭐
- ✅ Valódi Excel fájl (.xlsx)
- ✅ **Minden külön sorban** → húzható az Excel-ben!
- ✅ Üres cellák helyesen kezelve (nincs "lecseréli éket?" figyelmeztetés)
- ✅ Formázás megmarad
- ⚠️ **Első használathoz internetkapcsolat szükséges** (SheetJS betöltése)

**Használat Excel-ben:**
1. Megnyitod a letöltött .xlsx fájlt
2. Párosítatlan név megfogása
3. Húzod a megfelelő eredeti név mellé
4. Kész! Nincs felesleges figyelmeztetés!

### CSV - Mindig működik!
- ✅ Mindig működik (internetkapcsolat nélkül is)
- ✅ Excel-ben is megnyitható
- ✅ UTF-8 BOM támogatás (magyar ékezetek)
- ⚠️ Kézzel kell javítani az üres cellákat

## 📊 Kimenet

A program egy táblázatot generál:
- **Első oszlop**: Eredeti osztálynévsor
- **További oszlopok**: 1-3 feladatlista eredményei
- **Párosítatlan nevek**: A táblázat alján, piros háttérrel jelezve
  - 📝 **ikon**: Vesszős név (két diák együtt írta be)
  - Egyéb: Túl nagy eltérés, kézzel javítható

## 💡 Tippek

### Diákoknak:
A Seterra **nem enged szóközt** a nevekben! Használjátok:
- ✅ **CamelCase:** `VezetéknévKeresztnév` (ajánlott!)
- ✅ **Pont:** `Vezetéknév.Keresztnév`
- ✅ **Egybeírva:** `vezeteknevkeresztnev`
- ❌ **NE írjatok vesszővel több nevet!** Mindenki a saját nevét írja!

### Pedagógusoknak:
- Ha egy név nem párosul automatikusan (< 85% egyezés), a táblázat alján megjelenik
- A duplikált nevek "2x", "3x" jelöléssel vannak ellátva
- Az XLSX fájl megnyitható Excel-ben és Google Sheets-ben is
- Ha vesszős nevet látsz (📝), az azt jelenti, hogy két diák együtt írta be a nevét

## 🛠️ Technikai részletek

- Tiszta HTML + JavaScript (vanilla JS)
- SheetJS (XLSX könyvtár) - CDN-ről, defer attribútummal
- Fuzzy string matching (Levenshtein distance)
- Fájlméret: ~43 KB (+ ~700 KB SheetJS cache első használatkor)
- Kompatibilis: Minden modern böngésző

## 🔧 Párosítási algoritmus

```
1. Vesszős név? → PÁROSÍTATLAN (📝 jelzéssel)
   ↓
2. 100% normalizált egyezés? → PÁROSUL
   ↓
3. 85% teljes név hasonlóság? → PÁROSUL
   ↓
4. Van vezetéknév?
   ├─ IGEN: Vezetéknév 88% + keresztnév 85% → PÁROSUL
   └─ NEM: Csak keresztnév 90% → PÁROSUL
   ↓
5. Semmi nem egyezik → PÁROSÍTATLAN
```

## 📄 Példa használat

**Eredeti névsor:**
```
Vezetéknév Keresztnév
MásikVezetéknév Keresztnév Másodiknév
Vezetéknév-Keresztnév Másodiknév
```

**Seterra eredmények:**
```
1.vezeteknevkeresztnev100%00:15.23312/14/25
2.MásikVezetéknévKeresztnévMásodiknév100%00:18.45612/14/25
3.vezeteknevkeresztnev,masikvezeteknevmasikkeresztnev100%00:22.11112/14/25
```

**Eredmény táblázat:**
```
Névsor               | 1. lista
---------------------|-------------------------
Vezetéknév Keresztnév                    | vezeteknevkeresztnev
MásikVezetéknév Keresztnév Másodiknév    | MásikVezetéknévKeresztnévMásodiknév
Vezetéknév-Keresztnév Másodiknév         |
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ Párosítatlan nevek:
                                           | 📝 vezeteknevkeresztnev,masikvezeteknevmasikkeresztnev
```

**Magyarázat:**
- Az első névhelyettesítő ✅ párosult
- A második névhelyettesítő ✅ párosult
- A 3. sorban valaki két nevet írt be vesszővel → párosítatlan, manuális javítás szükséges

## 📄 Licence

MIT License - Szabadon használható oktatási célokra.

---

## 🤝 Közreműködés
Hibajelzést vagy fejlesztési javaslatot a GitHub Issues felületén lehet rögzíteni.

---

Verzió: 9
Utolsó frissítés: 2026. február
