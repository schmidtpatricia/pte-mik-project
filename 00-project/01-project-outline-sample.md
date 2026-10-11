---
name: Schmidt Patrícia
neptun: VO0FT2
id: 2026-LA-02
github: https://github.com/schmidtpatricia/pte-mik-project/tree/main
---
# League of Legends mérkőzés-adattárház

A projekt egy League of Legends mérkőzésekre épülő adattárházi háttérrendszer és a hozzá kapcsolódó statisztikai webalkalmazás megvalósítása. A központi kérdés az, hogy a Riot Games API-ból származó hatalmas mennyiségű nyers adathalmaz hogyan gyűjthető megbízhatóan, és hogyan transzformálható egy elemzésre optimalizált dimenzionális sémába. A megoldás egy verziókezelt rendszer: a backend végzi az aszinkron adatgyűjtést és a rate-limit kezelést, egy SQL-alapú ETL vagy ELT folyamat felel az adatok tisztításáért és inkrementális betöltéséért egy relációs adatbázisba, míg a statisztikai elemzéseket és diagramokat egy webes felület jeleníti meg. A projekt végére a rendszer több százezer meccs adatait képes historikusan tárolni, felgyorsított lekérdezésekkel elemezni és vizualizálni.

## Célok

- **Elsődleges cél:** Egy valós e-sport adatokon alapuló, jól strukturált dimenzionális adattárház, egy megbízható adatbetöltő folyamat és egy ezeket bemutató vizualizációs webalkalmazás elkészítése.
- **Célfelhasználók / érintettek:** Statisztikák iránt érdeklődő LoL játékosok.
- **Mérhető sikerkritériumok:** A rendszer letölti és eltárolja a mérkőzésadatokat; az optimalizált elemző SQL lekérdezések sikeresen lefutnak az adattárházon; a kinyert statisztikák a webalapú dashboardon megjelennek.
- **Korlátok:** Az adatgyűjtő kliens architektúrálisan elkülönül az adatbázistól; az adattárház egy relációs adatbázis-kezelő rendszerben készül; a külső kommunikáció a Riot API-val történik, ahol a 429-es (Too Many Requests) hibákat szigorúan kezelni kell; a forráskód GitHubon van; hitelesítő adatok és API kulcsok nem kerülhetnek a repóba.

## Hatókör

### Benne van a hatókörben

- Riot Games API integráció és aszinkron adatgyűjtő worker készítése.
- Több százezer mérkőzés nyers adatainak nyomon követhető tárolása a Staging rétegben.
- A dimenzionális adatmodell (csillag- vagy hópehelyséma) fizikai és logikai megtervezése, a kettő összehasonlító elemzése.
- A dimenziótáblák (játékos, hős, szerepkör, idő, patch) feltöltése, kiegészítve a hősök lore szerinti régióival (Ionia, Noxus stb.).
- A lassan változó dimenziók (SCD) historizálási problémájának kezelése.
- SQL-alapú ETL vagy ELT folyamat írása az adatok tisztítására és az új meccsek betöltésére.
- Komplex analitikai SQL lekérdezések megírása a meccsadatok elemzéséhez.
- A lekérdezések teljesítményének optimalizálása (indexelés, végrehajtási tervek vizsgálata) és a mérési eredmények dokumentálása.
- Egy statisztikai webalkalmazás (vagy interaktív dashboard) lefejlesztése, amely grafikonokon keresztül vizualizálja az adattárház adatait.

### Nincs benne a hatókörben

- Élő meccsek valós idejű, streaming alapú feldolgozása.
- Meccsek kimenetelét prediktáló gépi tanulási modellek.
- Felhasználókezelés és beléptetés a weboldalon, mivel a felület célja pusztán a kinyert statisztikák vizualizációja.
- Különálló asztali (desktop) alkalmazás.
- Más Riot játékok adatainak integrálása.

## Jegyzetek

Az első fázis az adatmodell logikai megtervezésére és a Riot API-hoz kapcsolódó adatgyűjtő elkészítésére összpontosít. Ezt követi a Staging és a dimenzionális rétegek megvalósítása a relációs adatbázisban, majd az ETL vagy ELT folyamatok lefejlesztése. A hatókör legvégén szereplő webes vizualizációs felület csak akkor kerül kidolgozásra, ha a háttérrendszer, az adatbetöltés és az optimalizált lekérdezések már megbízhatóan és gyorsan működnek.