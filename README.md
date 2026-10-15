# Feladatlista Ellenőrző

Egyetlen HTML-fájlból álló, **általános névlista-egyeztető** segédprogram pedagógusoknak. Egy eredeti névsort legfeljebb három másik névlistával hasonlít össze, és az eredményt táblázatban, CSV-ben vagy Excel-fájlban adja vissza. A Seterra-eredmények beolvasása ennek egyik külön támogatott módja.

Az útmutató kizárólag semleges névhelyettesítőket használ.

> ## 🔒 Adatvédelem és GDPR
>
> A beírt névsorok és feladatlisták feldolgozása **helyben, a megnyitott böngészőben** történik. A program a neveket és az eredményeket **nem tölti fel, nem küldi el külső szolgáltatásnak**, és nem tárolja szerveren.
>
> Ez a megoldás különösen kedvező adatvédelmi szempontból: nincs külső adatfeldolgozó, ahová a tanulói nevek átkerülnének. A helyi feldolgozás a GDPR szerinti *beépített és alapértelmezett adatvédelem* elvével összhangban áll ([GDPR, 25. cikk](https://eur-lex.europa.eu/legal-content/HU/TXT/?uri=CELEX:32016R0679)).
>
> A teljes intézményi GDPR-megfelelésért ugyanakkor mindig az adatkezelő intézmény felel: például a célhoz kötött használatért, a szükséges hozzáférési és megőrzési szabályokért ([EDPB útmutató](https://www.edpb.europa.eu/sme/be-compliant/be-compliant_en)).

## Mire használható?

Kétféle bemenet közül lehet választani.

| Mód | Mit kell bemásolni? | Mire jó? |
| --- | --- | --- |
| **Csak nevek** | Soronként egy nevet | Bármely feladat, jelenléti lista, leadási lista vagy online gyakorlófelület névlistájának ellenőrzésére. |
| **Seterra-eredménylista** | A Seterra-ból kimásolt eredménysorokat | A program a sorszám–név–százalék formátum alapján kiolvassa és párosítja a neveket. Az időeredmény maradhat a sorban. |

Mindkét módban megadható az eredeti névsor és legfeljebb három lista. Az egyes listák címe opcionálisan átírható; ha üresen marad, az eredményben **1. feladatlista**, **2. feladatlista**, illetve **3. feladatlista** jelenik meg.

## Használat

1. Töltsd le az `index.html` fájlt a számítógépedre.
2. Nyisd meg bármely modern böngészőben (Chrome, Edge, Firefox vagy Safari). Nem kell telepíteni semmit.
3. Másold be az eredeti névsort; minden név külön sorba kerüljön.
4. Válaszd ki a feladatlisták típusát.
5. Másold be az első, szükség esetén a második és harmadik listát is.
6. Ha szeretnéd, add meg a listák saját címét, például „Vaktérkép” vagy „Jelenlét”.
7. Kattints a **„Táblázat készítése”** gombra.
8. Ellenőrzés után töltsd le az eredményt CSV- vagy XLSX-formátumban.

A jobb felső **„ℹ️ Hogyan működik?”** gomb rövid beépített útmutatót is ad.

## Saját gépen, internet nélkül

A programot a letöltött HTML-fájl közvetlen megnyitásával, saját gépen lehet használni.

- A névfeldolgozás, a párosítás, a táblázatkészítés és a **CSV-export internet nélkül is működik**.
- Az **Excel (XLSX) exporthoz** a SheetJS könyvtárra van szükség, amelyet a program külső címről tölt be. Ha nincs kapcsolat – vagy a böngésző nem őrizte meg gyorsítótárban –, az XLSX-export nem érhető el, de a CSV-export változatlanul használható.
- A könyvtár letöltésekor sem kerülnek elküldésre a bemásolt nevek vagy eredmények; a böngésző csak magát a programkönyvtárat kéri le.

## Névfelismerés

A program a következő gyakori alakokat kezeli:

- ékezet nélküli és kisbetűs beírás;
- egybeírt név, például `vezeteknevkeresztnev`;
- CamelCase alak, például `VezetéknévKeresztnév`;
- ponttal vagy szóközzel tagolt alak, például `Vezetéknév.Keresztnév`;
- fordított sorrendű, egybeírt név, például `KeresztnévVezetéknév`;
- a fordított alak végén rövid számos azonosító is megengedett.

Az algoritmus szándékosan óvatos: a csendben hibás párosítás kockázatát csökkenti.

- Azonos vezetéknevű, de eltérő keresztnevű személyeket nem párosít össze pusztán a vezetéknév alapján.
- Egy bemeneti név egy listán belül csak egyszer használható fel.
- A vesszővel elválasztott, több személyre utaló beírásokat nem párosítja automatikusan.
- Egyes egyértelmű, rövidített keresztnevek sárga **⚠️ ellenőrizendő** jelöléssel kaphatnak párosítást. Ezeket érdemes ránézéssel ellenőrizni.
- A nem párosított nevek a táblázat alján jelennek meg, így Excelben néhány mozdulattal javíthatók.

## Csak nevek mód – általános használat

Ebben a módban minden nem üres sor egy név; nincs szükség sorszámra, százalékra vagy időeredményre.

```text
VezetéknévKeresztnév
Másik Vezetéknév
KeresztnévVezetéknév
```

Használható például egy feladatot leadók, egy jelenléti lista vagy egy online gyakorlófelület névlistájának összevetésére.

## Seterra-eredménylista mód – külön támogatott formátum

A Seterra nem enged szóközt a névben, ezért a tanulók többféleképpen írhatják be azt. A program a névsorhoz próbálja igazítani ezeket az alakokat.

```text
1.vezeteknevkeresztnev100%00:15
2.VezetéknévKeresztnév95%00:18
3.Vezetéknév.Keresztnév90%00:22
```

A program a sorszám és a százalék közötti névrészt használja a párosításhoz. Ha egy bemásolt lista nem ilyen eredménysorokat tartalmaz, válts **„Csak nevek”** módra.

## Eredmény és export

A táblázat első oszlopa az eredeti névsor. A további oszlopok a megadott feladatlisták. A címsorok a megadott saját címeket, vagy azok hiányában az alapértelmezett feladatlistasorszámot mutatják.

| Jelölés | Jelentés |
| --- | --- |
| Zöld név | automatikus párosítás |
| Sárga `⚠️` | enyhébb szabállyal párosított, ellenőrizendő név |
| Piros rész a táblázat alján | párosítatlan bemeneti név |
| `📝` | vesszővel elválasztott, több személyre utaló beírás |
| `2x`, `3x` | ugyanaz a név többször szerepel a bemeneti listában |

### CSV

- internet nélkül is elkészül;
- Excelben és más táblázatkezelőkben megnyitható;
- kezeli a magyar ékezeteket.

### Excel (XLSX)

- valódi `.xlsx` fájlt készít;
- az üres cellákat üresen hagyja;
- az ellenőrizendő párosításokat az exportban is jelöli;
- internetkapcsolat vagy meglévő böngésző-gyorsítótár szükséges hozzá.

## Technikai tudnivalók

- Egyetlen HTML-fájl, tiszta HTML, CSS és JavaScript.
- Nincs saját szerver, felhasználói fiók vagy adatbázis.
- A névegyeztetés Levenshtein-távolságon alapuló, szabályokkal kiegészített hasonlóságvizsgálat.
- Az XLSX-export a SheetJS könyvtárat használja.

## Közreműködés

Hibajelzés vagy fejlesztési javaslat a GitHub Issues felületén rögzíthető.

---

**Verzió:** 11
**Utolsó frissítés:** 2026. október
