---
layout: "default"
description: ""
id: "muutosloki"
---
# Muutosloki
{:.no_toc}

## Versio 1.0.0

-  Ensimmäinen julkaisuversio.

## 23.1.2023

- Lisätty johdanto- ja README-sivujen sisällöt.
- Lisätty assosiaatio RakennuskohteenSijaintitiedot.hallinnollinenAlue, poistettu RakennuskohteenSijaintitiedot.kuntanumero. Muutettu kuntanumeroa koskeva laatusääntö vastaavasti.
- Valmistelua 1.0-version julkaisua varten. 

## 20.1.2023

-  Päivitetty UML-malliin Yhteiset tietokomponentit -kirjaston pre-1.0 -versio (commit f70db7122fa6113965dabcdde365a12d8b99beb3). Ei muutoksia tämän tietomallin sisältöön.

## 19.1.2023

- Korjattu kirjoitusvirhe koodiston RakennuksenKäyttötarkoitusluokkaEnergiatehokkuudenArvionnissa nimessä.
- Lisätty laatusääntö kuntanumerolle, fixes #72
- Lisätty laatusääntö huoneistoala- ja huoneiston käyttöala -attribuuteille, fixes #73
- Lisätty laatusääntö huoneiston huoneiden lukumäärälle, fixes #74
- Lisätty laatusääntö kerrosalalle, fixes #75
- Lisätty laatusääntö kerrosluvulle, fixes #76
- Lisätty laatusääntö tilavuudelle, fixes #77
- Lisätty laatusääntö kellarialalle, fixes #78
- Lisätty laatusääntö väestösuojen henkilömäärälle, fixes #79
- Lisätty laatusääntö rakennuskohteen kokonaisalalle, fixes #80
- Lisätty laatusääntö huoneiston muutoksen huonemäärän muutokselle, fixes #81
- Lisätty laatusääntö asuinrakennuksen kerrosalan vähimmäismäärälle, fixes #82
- Lisätty laatusääntö sähkölämmityksen ja sähköliittymän suhteesta, fixes #83
- Lisätty elinkaarisääntö huoneiston muutostietojen antamisesesta, fixes #84
- Lisätty laatusääntö huoneiston muutoksen pakollisista huoneisto-attribuuteista, fixes #85
- Lisätty elinkaarisääntö olemassaolevasta huoneistotunnuksesta huoneiston lisäyksessä, fixes #86
- Lisätty laatusääntö huonesalan vähimmäismäärästä, fixes #87
- Lisätty laatusääntö sähkölämmityslähteen ja sähkölämmitysenergian lähteen yhteydestä, fixes #88
- Lisätty kaksi laatusääntöä koskien laajentamistoimenpiteen muutostietoja ja laajennusosaa, fixes #90
- Lisätty laatusääntö lämmitystavan ja lämmmitysenergian lähteen yhteydelle, fixes #91
- Lisäty laatusääntö asuinrakennuksen äänestysaluenumerolle, fixes #92
- Lisätty laaatusääntö rakennuksen pakollisesta tilavuudesta, fixes #93
- Lisätty laaatusääntö rakennuksen pakollisesta kerrosalasta, fixes #94
- Lisätty laaatusääntö rakennuksen pakollisesta kokonaisalasta, fixes #95
- Lisätty laaatusääntö rakennuksen pakollisesta kerroluvusta, fixes #96

## 18.1.2023

- Yhdistetty koodistoluokat EnergiaJaIlmastoselvityksenLaji, OhjeasiakirjanLaji ja RakentamisenSuunnitelmanLaji uudeksi yleisemmäksi koodistoksi LuvanvaraisenRakentamisenAsiakirjanLaji. Y-alustan koodisto puuttuu edelleen.
- Uudelleennimetty ViemäröintitavanLaji -> JätevesienKäsittelynLaji, ja kytketty Y-alustan koodistoon http://uri.suomi.fi/codelist/rytj/jatevesienkasittely
- Lisätty uusi attribuutti Huoneisto.käymälätyyppi ja sille uusi koodistoluokka Käymälätyyppi.
- Lisätty uudet attribuutit Rakennuspaikka.hulevedenKäsittelytapa ja Talotekniikkatiedot.hulevedenKäsittelytapa ja niille uusi yhteinen koodistoluokka HulevedenKäsittelynLaji.
- Poistettu RakennuskohteenToimenpide-luokan attribuutti toimenpidealueenLämmitettyNettoala ja lisätty attribuutti RakennuskohdekohtaisetVähähiilisyystiedot.kohteenToimenpidealueenLämmitettyNettoala.
- Lisätty attribuutti Materiaaliseloste.toimenpidealueenLämmitettyNettoala.
- Lisätty attribuutti Materiaaliseloste.rakennuksenKäyttötarkoitus.
- Päivitetty laatusäännöt vastaamaan muutettua ilmastoselvityksen luokkarakennetta.
- Päivitetty dokumentaatio-sivun otsikot vastaamaan muutettua ilmastoselvityksen luokkarakennetta ja lisätty koodistoluokkien otsikot ja Y-alustaviittaukset.
- Lisätty laatusääntöihin materiaaliselosteen sisältöä koskevat vaatimukset.

## 10.1.2023

- Siirretty ```Ilmastoselvitys```-luokan attribuutti ```rakennuksenTavoitteellinenKäyttöikä``` ```RakennuksenKäyttötiedot```-luokan ```tavoitteellinenKäyttöikä```-attribuutiksi.
- Siirretty ```Ilmastoselvitys```-luokan attribuutti ```rakennuksenSuunniteltuKäyttäjämäärä``` ```RakennuksenKäyttötiedot```-luokan ```suunniteltuKäyttäjämäärä```-attribuutiksi.
- Siirretty ```RakennuskohteenVähähiilisyystiedot``` attribuutti ```toimenpidealueenLämmitettyNettoala``` luokkaan ```RakennuskohteenToimenpide```.
- Muutettu ```Hiilijalanjälkitiedot```-luokan stereotyyppi FeatureType->DataType ja poistettu perintä luokasta ```Tietoryhmä```. Lisätty attribuutit ```rajaArvostaPoikkeamisenPeruste```ja ```osatekijä``` ja muokattu rajoitteita. Nyt rajoitteissa mukana vaadittujen osatekijöiden suureiden tunnukset, suureiden arvojen tyypit ja mittayksiköt.  
- Muutettu ```Hiilikädenjälkitiedot```-luokan stereotyyppi FeatureType->DataType ja poistettu perintä luokasta ```Tietoryhmä```. Lisätty attribuutit ```rajaArvostaPoikkeamisenPeruste```ja ```osatekijä``` ja muokattu rajoitteita. Nyt rajoitteissa mukana vaadittujen osatekijöiden suureiden tunnukset, suureiden arvojen tyypit ja mittayksiköt.  
- Muokattu luokasta ```RakennuskohteenVähähiilisyystiedot``` (FeatureType) uusi luokka ```RakennuskohdekohtaisetVähähiilisyystiedot```, joka ei enää periydy luokasta ```Tietoyksikkö```. Poistettu attribuutit ```rajaArvostaPoikkeamisenPeruste``` ja ```toimenpidealueenLämmitettyNettoala```, ja lisätty attribuutit ```hiilijalanjälki```ja ```hiilikädenjälki``` sekä assosiaatio ```kohde:RakennusTaiSenOsa```. Muokattu rajoitteita.
- Muokattu luokasta ```RakennuspaikanVähähiilisyystiedot``` (FeatureType) uusi luokka ```RakennuspaikkakohtaisetVähähiilisyystiedot```, joka ei enää periydy luokasta ```Tietoyksikkö```. Poistettu attribuutti ```rajaArvostaPoikkeamisenPeruste``` , ja lisätty attribuutit ```hiilijalanjälki```ja ```hiilikädenjälki``` sekä assosiaatio ```paikka:Rakennuspaikka```.
- Lisätty luokkaan ```Ilmastoselvitys``` attribuutit ```kohteenVähähiilisyys``` ja ```paikanVähähiilisyys``` sekä rajoitteet koskien pysyvää rakennustunnusta, laskennallista energiankulutusta, rakennuksen suunniteltua käyttäjämäärää, rakennuksen tavoitteellista käyttöikää, rakennuspaikan pinta-alaa ja toimenpidealueen lämmitetylle nettoalaa.
- Lisätty luokkaan ```Materiaaliseloste``` attribuutit ```otsikko```, ```kuvaus```, ```laatimispäivä```, ```rakennuksenOsienMateriaalit```, ```rakennuspaikanMateriaalit```, ```materiaalilajinMäärä```, ```vaarallistenAineidenMäärä```, ```uusituvanMateriaalinMäärä```, ```uusiutumattomanMateriaaliMäärä```, ```kierrätetynMateriaalinMäärä```, ```uudelleenkäytetynMateriaalinMäärä```.
- Lisätty luokkaan ```Materiaaliseloste``` rajoitteet vaadituille materiaalilajien määrille, pysyvälle rakennustunukselle, tavoitteelliselle käytöiälle, rakennuspaikan pinta-alalle ja toimenpidealueen lämmitetylle nettoalalle.
- Lisätty luokat ```RakennuskohdekohtaisetMateriaalimäärät``` ja ```RakennuspaikkakohtaisetMateriaalimäärät```.
- Korjattu koodiston Verkostoliittymän laji viittaus, fixes #70
- Muutettu koodiston EnergianLähde nimi ja koodistoviittaus, fixes #69
- Muutettu koodiston PolttoaineTaiLämmönLähde nimi ja koodistoviittaus, fixes #68
- Korjattu kantavien rakenteiden rakennusaine -koodiston viittaus, fixes #67
- Korjattu julkisivumateriaali-koodiston viittaus ja nimi, fixes #66
- Korjattu ilmanvaihtotavan laji -koodiston viite, fixes #65
- Lisätty koodiston TalousvedenLaji koodistoviittaus, fixes #56
- Lisätty koodiston SähköenergianLähteenLaji koodistoviittaus, fixes #52
- Lisätty koodiston JäähdytystavanLaji koodistoviittaus, fixes #51
- Lisätty koodiston HissinLaji koodistoviittaus, fixes #49
- Lisätty koodiston SisäänkäynninTyyppi koodistoviittaus, fixes #48
- Värjätty Y-alustalta puuttuvat koodistot punaisella.


## 3.1.2023

- Päivitetty uusin ry-yhteiset dev.
- Uudelleennimetty koodistoluokka SisäänkäynninTaiHissinElinkaarenVaihe -> RakennuksenToiminnallisenOsanElinkaarenVaihe.
- Lisätty Y-alustan koodistoihin viittaavat vocabulary-tagien arvot koodistoluokille RakennuksenToiminnallisenOsanElinkaarenVaihe, RakennuskohteenTiedonLaji, RakennuksenOsittelunLaji, HuoneistonElinkaarenVaihe, fixes #47, #50, #58
- Korjattu puuttunut Talotekniikka-luokan attribuutin verkostoliittymä tyyppi, fixes #55
- Korjattu elinkaarisääntöä ```elinkaari/vaat-huoneisto-elinkaaren-vaiheen-sallitut-muutokset``` ottamaan huomioon lisätty koodi ```2 - Rakenteilla```
- Korjattu elinkaarisääntöä ```elinkaari/vaat-hissi-sisaankaynti-elinkaaren-vaiheen-sallitut-muutokset``` ottamaan huomioon lisätty koodi ```2 - Rakenteilla```
- Korjattu elinkaarisääntöä ```elinkaari/vaat-hissin-sisaankaynnin-ja-rakennuksen-elinkaaret``` ottamaan huomioon koodiston RakennuksenToiminnallisenOsanElinkaarenVaihe uudelleennumerointi.
- Lisätty seuraavat laatusäännöt:
   - ```laatu/vaat-rakennuksen-ensisijainen-sisaankaynti```
   - ```laatu/suos-rakennuksen-osan-tilat```
   - ```laatu/suos-rakennuksen-osan-huoneistot```
   - ```laatu/suos-tilan-yhteys-rakennuksen-osaan```
   - ```laatu/vaat-huoneiston-tunnus```
   - ```laatu/suos-huoneiston-yhteys-rakennuksen-osaan```
   - ```laatu/vaat-ensisijainen-kant-rak-rakennusaine```
   - ```laatu/vaat-ensisijainen-julkisivumateriaali```
   - ```laatu/vaat-rakennuksen-ensisijainen-kayttotarkoitus```
   - ```laatu/vaat-ensisijainen-lammitystapa```
   - ```laatu/vaat-ensisijainen-lammitysenergian-lahde```
   - ```laatu/vaat-ensisijainen-jaahdytystapa```
   - ```laatu/vaat-ensisijainen-jaahdytysenergian-lahde```
   - ```laatu/vaat-ensisijainen-sahkoenergian-lahde```
   - ```laatu/vaat-ensisijainen-ilmanvaihtotapa```
   - ```laatu/vaat-sisaankaynnin-geometria```
   - ```laatu/vaat-hissin-geometria```
   - ```laatu/vaat-ilmastoselvitys-rakennuspaikan-pinta-ala```


## 23.12.2022

- Korjattu Rakennelma-luokan attribuutin ```väliaikainenTunnus```-attribuutin kardinaliteetti 1 -> 0..1
- Lisätty Hissi-luokkaan attribuutti elinkaarenVaihe, ja koodistoluokka SisäänkäynninTaiHissinElinkaarenVaihe, fixes #45,
- Lisätty Sisäänkäynti-luokkaan attribuutti elinkaarenVaihe, fixes #44 

## 22.12.2022

- Lisätty RakennuksenOsittelu-luokkaan kuvaus-attribuutti. Hyödyllinen, mikäli perusteen lajiksi valitaan "muu ositteluperuste".
- Lisätty Huoneisto-luokkaan attribuutti elinkaarenVaihe ja sille koodistoluokka HuoneistonElinkaarenVaihe. Poistettu attribuutit muuttokiellossa ja muuttovalmis, jotka ilmenevät elinkaarenVaihe-attribuutin arvoina, fixes #43
- Muutettu RakennuskohteenMuutos-luokan assosiaation ```paikka:Rakennuspaikka``` kardinaliteetti 1..* -> 1. Kunkin rakennuskohteen muutoksen on koskettava täsmälleen yhtä rakennuspaikkaa.

## 21.12.2022

- Lisätty otsikkotason rakenne dokumentaatiosivulle.
- Korjattu Rakennuskohteet-luokkakaavion asettelua.
- Korjattu RakennuskohteenMuutos-luokan attribuutin ```varustemuutos``` tyypiksi RakennuksenVaruste.
- Poistettu HuoneistonMuutos-luokasta väärä usage-suhde luokkaan RakennuksenVaruste.
- Päivitetty elinkaarisääntöjä (edelleen keskeneräinen).

## 20.12.2022

- Muutettu Rakennuskohde-luokka abstraktiksi, fixes #42
- Poistettu luokat Rakentamistoimenpide ja Purkamistoimenpide, muutettu RakennuskohteenToimenpide-luokka konkreettiseksi ja lisätty siihen attribuutit purkamisenSyy, perusparannus ja korjausaste, fixes #41  
- Päivitetty uusin ry-yhteiset -riippuvuus, ei muutoksia rakennuskohteiden tietomallin luokkiin.

## 19.12.2022
- Lisätty ja uudelleenryhmitelty tietotyyppejä Materiaalitiedot, RakennuksenKäyttötiedot ja Energiatiedot. Poistettu Statustiedot ja viety sen attribuutit suoraan rakennuskohde-luokkiin, fixes #9, #12, #22 
- Poistettu RakennuskohteenToimenpide-luokasta suora assosiaatio asia RakentamislupaAsia-luokkaan, korvataan assosiaatiolla liittyväAsia luokkaan AlueidenkäyttöJaRakentamisasia, fixes #6
- Lisätty seuraavat koodistoluokat ja päivitetty attribuuttiviittaukset niihin: RakenuskohteenTiedonLaji, RakennuskohteenTiedonlähde, RakennuksenElinkaarenVaihe, Suojelutapa, KulttuurihistoriallinenMerkittävyys, RakennuksenVarusteenLaji, HuoneistonVarusteenLaji, RakennuksenTietomallinLaji, Omistajalaji, OmistuksenLaji, ErityistäToimintaaVartenRakennettavanAlueenTyyppi, RakennuksenOsittelunLaji, SisäänkäynninTyyppi, HissinLaji, 
Rakentamistapa, Paloluokka, KantavienRakenteidenRakennusaine, JulkisivumateriaalinLaji, Energialuokka, LämmitystavanLaji, JäähdytystavanLaji, SähköenergianlähteenLaji, PolttoaineTaiLammönlahde, JäähdytysenergianLähteenLaji, ViemäröintitavanLaji, TalousvedenLaji, IlmanvaihtotavanLaji, VerkostoliittymänLaji, SuhdeMaanpintaan, Huoneistotyyppi, Keittiötyyppi, RakennelmanKäyttötarkoitus, HuoneenTaiMuunTilanLaji, HuoneenTaiMuunTilanKäyttötarkoitus, EnergiaJaIlmastoselvityksenLaji, RakentamisenSuunnitelmanLaji, OhjeasiakirjanLaji, fixes #10
- Lisätty Hissi-luokka, fixes #11
- Poistettu Huone-luokan attribuutti ```huonelaji```. RakennettuTila-luokkan ```laji```-attribuutti viittaa nyt HuoneenTaiMuutTilanLaji-koodistoon, lisäksi lisätty uusi attribuutti ```käyttötarkoitus```, jolla toistaiseksi puuttuva Y-alustan koodisto, fixes #13, #14.
- Lisätty RakennettuTila-luokkaan attribuutit pysyväTilaTunnus, tilaryhmä, kokoontumistilanHenkilömäärä, tilavuus ja pohjapintaAla. Lisätty Huone-luokkaan attribuutit asuinhuone ja huoneala, fixes #15
- Puretttu Varuste-luokka kahdeksi luokaksi RakennuksenVaruste ja HuoneistonVaruste ja päivitetty niihin viittaavat attribuutit, fixes #16.
- Lisätty uusi tietoryhmittelyluokka Talotekniikkatiedot, fixes #17
- Lisätty uudet RakennuskohteenOmistaja- ja TunnuksettomanOmistajanTiedot-luokat, ja kytketty Rakennuskohde-luokkiin, fixes #18,#27
- Lisätty Rakennukohde-luokkaan uudet attribuutit tiedonLaji ja tiedonLähde, fixes #19
- Uudelleennimetty Erityisrakentamisalue -> ErityistäTarkoitustaVartenRakennettavaAlue, ja lisätty attribuutteja, fixes #20
- Lisätty assosiaatioluokka RakennuksenSisäänkäynti luokkien Rakennus ja Sisäänkäynti väliseen assosiaatioon. Sisältää attribuutin ensisijainen, ks. #21
- Lisätty Rakennustietomalli-luokkaan attribuutti ```jalanjälkiprojektionNurkkapiste```, fixes #23
- Lisätty seuraavat attribuutit luokkiin Rakennus, Rakennelma ja ErityistäToimintaaVartenRakennettavaAlue: väliaikainen:boolean ja purkamisenMääräaika:Date, fixes #24
- Lisätty RakennuskohteenSijaintitiedot-luokkaan attribuutti äänestysaluenumero, fixes #25
- Lisätty UlkokuorenTiedot-luokkaan attribuutti lentoeste:boolean, fixes #26
- Muutettu rakennelman käyttötarkoitus viittaamaan omaan koodistoonsa, fixes #28
- Siirretty kerrosala- ja rakennusoikeudellinenKerrosala-attribuutit luokasta SisätilojenTiedot luokkaan UlkokuorenTiedot, fixes #29
- Lisätty RakennelmataiSenOsa-luokkaan attribuutti kulttuurihistoriallinenMerkittävyys sekä energiatiedot, jonka alle edelleen jäähdytys- ja lämmitystapatiedot, ks. #30
- Lisätty Rakennusala-luokkaan ei-pakollinen attribuutti pintaAla, poistettu Ilmastoselvitys-luokasta attribuutti rakennuspaikanPintaAla, fixes #31
- Purettu luokka Statustiedot ja lisätty sen attribuutit suoraan luokkiin RakennusTaiSenOsa, Rakennus, RakennelmaTaiSenOsa, Rakennelta ja ErityistäTarkoitustaVarteRakennettavaAlue, fixes #32
- Poistettu Rakennuskohde-luokan attribuutti liittymäInfrastruktuuriin. LiittymäInfrastruktuuriin-luokka uudelleennimetty Verkostoliittymä-luokaksim jota käytetään Talotekniikkatiedot-luokassa. Lisätty myös ErityistäToimintaaVartenRakennettavaAlue-luokkaan attribuutit verkostoliittymä ja varuste, fixes #33
- Poistettu Huoneisto- ja RakennusTaiSenOsa-luokkien välinen assosiaatio ja korvattu se erillisillä assosiaatiolla Huoneisto- ja Rakennus-luokkien sekä Huoneisto- ja RakennuksenOsa-luokkien välillä, fixes #34
- Poistettu luokassa Statustiedot ollut redundantti valmistumisvuosi-attribuutti, valmistumispäivämäärä-attribuutti lisätty luokkiin RakennusTaiSenOsa, RakennelmaTaiSenOsa ja ErityistäToimintaaVartenRakennettavaAlue. Lisätty luokkaan RakennuskohteenToimenpide attribuutti arvioituValmistumisajankohta, fixes #36
- Erityissuunnitelma-luokan attribuutti laji, korvattu attribuutilla kuvaus, fixes #37
- Muutettu MateriaalinMäärä-luokan attribuuti laji tyypiksi Koodiarvo, fixes #38
- Uudelleennimetty luokan Energitiedot attribuutti energiatehokkuus -> laskennallinenEnergiatehokkuudenVertailuluku, ja muutettu tyyppi double:ksi, fixes #39
- Lisätty Huoneisto-luokalle käyttöAla-attribuutti [0..1], fixes #40
- Lisätty uudet luokkakaaviot Tilat ja huoneistot, Rakennuskohteen muutos, Materiaaliseloste.

## 14.12.2022

- Siirretty rakennuspaikan pinta-ala Ilmastoselvitys-luokasta Rakennuspaikka-luokkaan, fixes #31.
- Tehty Ilmastoselvitys- ja Rakennuskohde-luokkien välinen assosiaatio kahdensuuntaiseksi: Rakennuskohde-luokkaan voi liittyä nolla tai useampi Ilmastoselvitys. Siirretty Ilmastoselvitys luokan assosiaatio ```rakennuskohde``` viittaamaan RakennusTaiSenOsa-luokkaan Rakennuskohde-luokan sijasta: Ilmastoselvitys voi siis liittyä vain Rakennukseen tai RakennuksenOsaan.
- Lisätty Materiaaliseloste-luokka tyhjänä, assosiaatiot RakennusTaiSenOsa- ja Rakentamistoimenpide-luokkiin.
- Siirretty Ilmastoselvitys-luokan attribuutti ```rakennuksenLaskennallinenOstoenergianKulutus``` Energiatiedot-luokan ```laskennallinenOstoenergianKulutus```-attribuutiksi.

## 7.12.2022

- Siirretty rakentamis- ja purkamistoimenpiteet ja ilmastoselvitys kokonaisuudessaan Rakentamisen lupapäätökset -tietomallista osaksi Rakennuskohteet ja huoneistot -tietomallia. Peruste: Rakennuskohteiden elinkaareen olennaisesti liittyvät rakentamis- ja purkamistoimenpiteet ovat nyt osa rakennuskohteiden tietomallia riippumatta siitä vaativatko ne rakentamislupaa vai eivät. Ilmastoselvityksen tiedot liittyvät rakennuskohteeseen ja rakentamistoimenpiteeseen, jotka molemmat nyt rakennuskohteiden tietomallissa. Mahdollistaa ilmastoselvityksen tuottamisen myös toimenpiteiden yhteydessä, joissa rakentamislupaa ei tarvita. Seuraavat luokat tuotu sellaisenaan lupapäätösten tietomallista: RakennuskohteenToimenpide, Rakentamistoimenpide, Purkamistoimenpide,  RakentamistoimenpiteenLaji, PurkamistoimenpiteenLaji, Ilmastoselvitys, Hiilijalanjälkitiedot, Hiilikädenjälkitiedot, Energiankulutus, RakennuskohteenVähähiilisyystiedot, RakennuspaikanVähähiilisyystiedot, PoikkeamisenPeruste, Energialähde, RakennuksenKäyttötarkoitusluokkaEnergiatehokkuudenArvioinnissa, IlmastoselvityksenrajaArvoistapoikkeamisenPerusteenLaji, IlmastoselvityksenHiilijalanjälkisuure, IlmastoselvityksenHiilikädenjälkisuure, Rakennuspaikka. Fixes #1
- Poistettu RakennuskohteenToimenpide-luokasta suora assosiaatio ```asia``` RakentamislupaAsia-luokkaan, korvattu assosiaatiolla ```liittyväAsia``` luokkaan AlueidenkäyttöJaRakentamisasia. Peruste: Ei haluta, että Rakennuskohteiden tietomalli riippuu RakentamisLupapäätökset -tietomallista, vaan ainoastaan toisinpäin, fixes #6
- Lisätty uusi suora assosiaatio Rakennuskohde- ja Rakennuspaikka-luokkien välille (```kohde``` - ```paikka```). Rakennuskohteella on aina tasan yksi Rakennuspaikka, fixes #2
- Poistettu Ilmastoselvitys-luokan suora assosiaatio ```rakennuspaikka:Rakennuspaikka```: Ilmastoselvityksen Rakennuskohteen kautta saadaan aina myös Rakennuspaikka, fixes #3
- Uudelleennimetty Huoneisto-Huone -luokkien välisen assosiaation roolit kuuluu -> huoneisto ja koostuu -> huone. Peruste: mallissa ei käytetä verbejä assosiaatioroolien niminä muualla, fixes #4
- Poistettu käyttämättömät koodistot HuoneistonVaruste ja RakennuksenVaruste.
- Lisätty Kaavatiedot-tietomalli riippuvuudeksi ja palautettu Rakennuspaikka-luokan rakentamistaOhjaavaKaava- ja kaavyksikkö-assosiaatiot, fixes #5

## 5.12.2022

- Luurangot laatu- ja elinkaarisäännöistä lisätty
- Siirretty RakennuskohteenMuutos-, HuoneistonMuutos- ja HuoneistonMuutoksenLaji-luokat Rakentamisen lupapäätökset -tietomallista Rakennukohteiden tietomalliin. Peruste: näin saadaan lupapäätösprosessista riippumaton rakennuskohteiden ja huoneistojen muutosten elinkaari kuvattua Rakennuskohteiden tietomallissa ilman riippuvuutta Rakentamissen lupapäätösten tietomalliin. 