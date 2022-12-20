---
layout: "default"
description: ""
id: "muutosloki"
---
# Muutosloki

## 20.12.2022

- Muutettu Rakennuskohde-luokka abstraktiksi, fixes #42
- Poistettu luokat Rakentamistoimenpide ja Purkamistoimenpide, muutettu RakennuskohteenToimenpide-luokka konkreettiseksi ja lisätty siihen attribuutit purkamisenSyy, perusparannus ja korjausaste, fixes #41  

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