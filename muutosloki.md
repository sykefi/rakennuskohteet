---
layout: "default"
description: ""
id: "muutosloki"
---
# Muutosloki


## 7.12.2022

- Siirretty rakentamis- ja purkamistoimenpiteet ja ilmastoselvitys kokonaisuudessaan Rakentamisen lupapäätökset -tietomallista osaksi Rakennuskohteet ja huoneistot -tietomallia. Peruste: Rakennuskohteiden elinkaareen olennaisesti liittyvät rakentamis- ja purkamistoimenpiteet ovat nyt osa rakennuskohteiden tietomallia riippumatta siitä vaativatko ne rakentamislupaa vai eivät. Ilmastoselvityksen tiedot liittyvät rakennuskohteeseen ja rakentamistoimenpiteeseen, jotka molemmat nyt rakennuskohteiden tietomallissa. Mahdollistaa ilmastoselvityksen tuottamisen myös toimenpiteiden yhteydessä, joissa rakentamislupaa ei tarvita. Seuraavat luokat tuotu sellaisenaan lupapäätösten tietomallista: RakennuskohteenToimenpide, Rakentamistoimenpide, Purkamistoimenpide,  RakentamistoimenpiteenLaji, PurkamistoimenpiteenLaji, Ilmastoselvitys, Hiilijalanjälkitiedot, Hiilikädenjälkitiedot, Energiankulutus, RakennuskohteenVähähiilisyystiedot, RakennuspaikanVähähiilisyystiedot, PoikkeamisenPeruste, Energialähde, RakennuksenKäyttötarkoitusluokkaEnergiatehokkuudenArvioinnissa, IlmastoselvityksenrajaArvoistapoikkeamisenPerusteenLaji, IlmastoselvityksenHiilijalanjälkisuure, IlmastoselvityksenHiilikädenjälkisuure.
- Poistettu RakennuskohteenToimenpide-luokasta suora assosiaatio ```asia``` RakentamislupaAsia-luokkaan, korvattu assosiaatiolla ```liittyväAsia``` luokkaan AlueidenkäyttöJaRakentamisasia. Peruste: Ei haluta, että Rakennuskohteiden tietomalli riippuu RakentamisLupapäätökset -tietomallista, vaan ainoastaan toisinpäin.
- Lisätty uusi suora assosiaatio Rakennuskohde- ja Rakennuspaikka-luokkien välille (```kohde``` - ```paikka```). Rakennuskohteella on aina tasan yksi Rakennuspaikka.
- Poistettu Ilmastoselvitys-luokan suora assosiaatio ```rakennuspaikka:Rakennuspaikka```: Ilmastoselvityksen Rakennuskohteen kautta saadaan aina myös Rakennuspaikka.
- Uudelleennimetty Huoneisto-Huone -luokkien välisen assosiaation roolit kuuluu -> huoneisto ja koostuu -> huone. Peruste: mallissa ei käytetä verbejä assosiaatioroolien niminä muualla.
- Poistettu käyttämättömät koodistot HuoneistonVaruste ja RakennuksenVaruste.

## 5.12.2022

- Luurangot laatu- ja elinkaarisäännöistä lisätty
- Siirretty RakennuskohteenMuutos-, HuoneistonMuutos- ja HuoneistonMuutoksenLaji-luokat Rakentamisen lupapäätökset -tietomallista Rakennukohteiden tietomalliin. Peruste: näin saadaan lupapäätösprosessista riippumaton rakennuskohteiden ja huoneistojen muutosten elinkaari kuvattua Rakennuskohteiden tietomallissa ilman riippuvuutta Rakentamissen lupapäätösten tietomalliin. 