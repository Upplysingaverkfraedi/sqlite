# Gagnavinnsla með SQLite3

## Leiðbeiningar

- **Öll svör verða að vera rökstudd með skýrri röksemdafærslu.** Ekki verður veitt stig fyrir
  svör án rökstuðnings.
- **Tryggið skýrleika og skipulag í uppsetningu.** Hlaðið svo upp PDF útgáfu af lausninni ykkar.
- Þetta er hópverkefni, sem fer fram hér. **Notið PR til að fara yfir lausnir hvers annars.**
  Mikilvægt er að allir séu virkir þátttakendur í sérhverju undirverkefni.
    - Tveir teymismeðlimir þurfa að samþykkja breytingar frá öðrum áður en þær eru samþykktar.
    - Ekki samþykkja án þess að skilja innihald breytinganna, ef um er að ræða kóða þarf að tékka
      kóðann út og prófa keyra kóðann sjálf/ur.
    - Verið óhrædd að óska eftir frekari útskýringum ef eitthvað er óskýrt.
- **Óskýr uppsetning hefur áhrif á stigagjöf verkefnisins.**
- Gangi ykkur vel!

> Munið að uppfæra README skrána til að endurspegla innihald verkefnisins ykkar. Takið fram öll
> forrit sem þarf að hlaða niður og uppsetningu þeirra. Útskýrið möppustrúktur og hvernig
> verkefnið er unnið.
> Takið fram allar skipanalínur sem þarf að keyra til að keyra lausnina ykkar og notið
> viðeigandi markdown merkingar til að greina þær frá kóða (þ.e. nota \`\`\`bash skipanalína
> \`\`\` eða \`\`\`sql SELECT * FROM tbl;\`\`\`.).

## 1. Tíðni nafna á Íslandi

Verkefnið felur í sér að sameina tíðnigögn úr tveimur CSV skrám,

- [first_names_freq.csv](data/first_names_freq.csv)
- [middle_names_freq.csv](data/middle_names_freq.csv)

í SQLite gagnagrunn [names_freq.db](data/names_freq.db).
Nemendur munu búa til eina töflu í gagnagrunninum til að geyma og vinna úr þessum gögnum.

1. Búið til töflu sem inni heldur gögn um eiginnöfn og millinöfn ásamt tíðni þeirra.
    - Töflunafn: `names`
    - Dálkar: `name`, `year`, `frequency`, `type`
        - `name`: Eiginnafn eða millinafn
        - `year`: Ár sem tíðnin er fyrir
        - `count`: Tíðni nafnsins
        - `type`: Tegund nafns, segir til hvort nafnið sé eiginnafn eða millinafn
    - Þið þurfið að skilgreina hvaða dálkur (eða dálkar) eru aðallykill töflunnar.
    - Notið dálkagerð sem hentar best fyrir gögnin (reynið að nota minnsta mögulega gagnategund).
2. **Greining**: Greinið tíðni nafna **allra** hópmeðlima teymsins út frá þessum gögnum. Notið
   _eina_
   SQL fyrirspurn til að svara hverju af eftirfarandi spurningum:
    - Hvaða hópmeðlimur á algengasta eiginnafnið?
    - Hvenær voru öll nöfnin vinsælust?
    - Hvenær komu þau fyrst fram?
3. Skilið skipanaskrá `names.sql` sem a) býr til töfluna, b) les gögnin inn í töfluna og c) svarar
   spurningunum í lið 2.

## 2. Saga Ísfólksins

Verkefnið felur í sér að lesa inn SQLite gagnagrunninn [isfolkid.db](data/isfolkid.db) sem
inniheldur ýmis gögn um bókabálkinn _Söga Ísfólksins_ eftir norska rithöfundinn Margit Sandemo,
sem tröllreið íslenskt samfélag á 9. áratug 20. aldar.

1. Til að átta ykkur á grunninum, útbúið skipanaskrá sem sýnir hvernig gagnagrunninn er
   uppbyggður (ekki hafa gögnin sjálf með). Skilið henni sem `create_isfolkid.sql`.
2. Skilið skipanaskrá `isfolkid.sql` sem svarar eftirfarandi spurningum:
    - Hversu margar aðalpersónur eru í bókabálkinum?
    - Hversu margar persónur eru í hverri bók?
    - Hversu oft kemur Þengill fyrir í bókunum?
    - Hvað eru margir af Paladín ættinni?
    - Hversu algengur er illi arfurinn af þeim sem eru útvalin?
    - Hver er fæðingartíðni kvenna í bókabálkinum?
    - Hvað er Ísfólkið margar blaðsíður samanlagt?
    - Hvað er meðallengd hvers þáttar af _Ískisum_?

## 3. Gagnagrunnur fyrir tímataka.net

Nú skal vinna áfram með tímatöku-liðinn sem var kynntur í
[síðasta hópverkefni](https://github.com/Upplysingaverkfraedi/regex/?tab=readme-ov-file#4-gagna%C3%BArvinnsla).

Sérhver hópur fær ákveðið tímabil og skal taka saman öll hlaup úr þeim mánuði og skila sem
SQLite gagnagrunn:

1. Baratheon - ágúst 2024
2. Greyjoy - ágúst 2023
3. Lannister - ágúst 2022
4. Martell - ágúst 2021
5. Stark - ágúst 2020
6. Targaryen - ágúst 2019
7. Tyrell - ágúst 2018

### SQLite3 gagnagrunnur

Gagnagrunnurinn skal hafa eftirfarandi töflur:

1. Taflan `hlaup` sem tekur saman helstu upplýsingar um sérhvert hlaup, t.d.:
    - `id`: Auðkenni
    - `upphaf`: Tímasetning hlaups (dagsetning og tími dags)
    - `endir`: Áætluð lok hlaups (dagsetning og tími dags)
    - `nafn`: Nafn hlaups
    - `fjoldi`: Fjöldi þátttakenda
    - og fleiri eftir þörfum.
2. Taflan `timataka` sem tekur saman upplýsingar um hvern þátttakanda í hlaupinu, þar ætti að koma
   fram:
    - `id`: Auðkenni
    - `hlaup_id`: Auðkenni hlaups (ytri lykill)
    - `nafn`: Nafn keppanda
    - `timi`: Tími sem keppandi lauk hlaupinu á
    - `kyn`: Kyn keppanda (ef uppgefið)
    - `aldur`: Aldur keppanda (ef uppgefið)
    - og fleiri eftir þörfum.

Sannreynið með samsöfnun og hópun hvort fjöldi keppanda í `hlaup` töflunni sé réttur út frá
fjölda lína í `timataka` töflunni.

Skilið skipanaskrá `timataka.sql` sem býr til gagnagrunninn, les gögnin inn og sannreynir fjölda.

> Þið viljið ekki tvítaka gögn, t.d. í tilfelli Flensborgarhlaupið 2024 þá er ýmist gefið upp  
> [heildar](https://timataka.net/flensborgarhlaup2024/urslit/?race=2&cat=overall) niðurstöður,
> og líka niðurbrotið á [karla](https://timataka.net/flensborgarhlaup2024/urslit/?race=2&cat=m) og
> [kvenna](https://timataka.net/flensborgarhlaup2024/urslit/?race=2&cat=f) sér. Grunnurinn skal
> passa að það verða ekki leyfðar tvítekningar. Passið samt að þið missið ekki upplýsingar
> einsog kyn og aldur.

### RegEx útvíkkun

1. Útvíkkið Python kóðann ykkar `code/timataka.py` þannig að hann getur tekið lesið og unnið
   fleiri hlaup. Kóðinn skal vera **almennur**, ekki bundinn við ákveðin tímabil eða tegund
   hlaups. Passið að þið harðkóðið ekki nöfn hlaupa eða keppenda í kóðanum.
2. **Ábending**, hér gæti verið gott að brjóta upp reglulegu segðina frá því síðast í tvær
   reglulegar segðir:
    1. Eina til að finna viðeigandi línu (`thead` fyrir dálkaheiti og `tr` fyrir tímatöku gögn).
    2. Svo þegar við erum búin að finna viðeigandi línu, notið aðra reglulega segð
       til að finna gildin úr öllum dálkum (`td`).
3. Bætið við reglulega segð til að sækja öll viðbótarupplýsingar sem á almennt við hlaupið.

### Samvinna

Mælt er með að tveir nemendur vinni saman að þessum liði. Annar nemandi einbeitir sér að því að
parsa gögnin með uppfærðu RegEx í Python, meðan hinn býr til gagnagrunninn og innlestur gagna.

Þið þurfið ekki að bíða eftir RegEx hlutnum til að hefja vinnu með SQLite gagnagrunninn, þar sem
niðurstöður frá síðasta verkefni eru til staðar.

Ekki er mælt með að þið vinni í sama branchi.

Nauðsynlegt er að vinna náið saman svo hægt sé að uppfæra SQLite gagnagrunninn með nýjustu gögnunum.
Hugsanlega væri gott að búa til branch fyrir RegEx hlutann sem er tengdur við SQLite, og gera PR í
SQLite branchið til að tryggja að það sé alltaf uppfært. Þaðan má svo gera PR í main branchið.
