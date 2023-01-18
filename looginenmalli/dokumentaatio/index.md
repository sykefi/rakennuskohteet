---
layout: "default"
description: ""
id: "dokumentaatio"
status: "Keskeneräinen"
---
# Loogisen tason rakennuskohteiden ja huoneistojen tietomalli
{:.no_toc}

1. 
{:toc}

## Yleistä
Loogisen tason Rakennuskohteiden ja huoneistojen tietomalli määrittelee yhteiset tietorakenteet, joita käytetään rakennusten, rakennelmien ja muiden rakennuskohteiden, sekä rakennusten sisältämien rakennettujen tilojen ja huoneistojen tietojen kuvaamiseen koneluettavassa rakenteisessa paikkatietomuodossa. Tietomallin luokkia tulee käyttää tietomallin [elinkaari](../elinkaarisaannot.html)- ja [laatusääntöjen](../laatusaannot.html) mukaisesti. Looginen tietomalli pyrkii olemaan mahdollisimman riippumaton tietystä toteutusteknologiasta tai tiedon fyysisestä esitystavasta (esim. relaatiotietokanta, tietyn ohjelmointikielen tietorakenteet, XML, JSON).

## Normatiiviset viittaukset
Seuraavat dokumentit ovat välttämättömiä tämän dokumentin täysipainoisessa soveltamisessa:

* [ISO 639-2:1998 Codes for the representation of names of languages — Part 2: Alpha-3 code][ISO-639-2]
* [ISO 8601-1:2019 Date and time — Representations for information interchange — Part 1: Basic rules][ISO-8601-1]
* [ISO 19103:2015 Geographic information — Conceptual schema language][ISO-19103]
* [ISO 19107:2019 Geographic information — Spatial schema][ISO-19107]
* [ISO 19108:2002 Geographic information — Temporal schema][ISO-19108]
* [ISO 19109:2015 Geographic information — Rules for application schema][ISO-19109]
* [ISO 19505-2:ISO/IEC 19505-2:2012, Information technology — Object Management Group Unified Modeling Language (OMG UML) — Part 2: Superstructure][ISO-19505-2]

## Standardienmukaisuus
Kuvattu tietomalli perustuu [ISO 19109][ISO-19109]-standardin yleinen kohdetietomalliin (General Feature Model, GFM), joka määrittelee rakennuspalikat paikkatiedon ISO-standardiperheen mukaisten sovellusskeemojen määrittelyyn. GFM kuvaa muun muassa metaluokat ```FeatureType```, ```AttributeType``` ja ```FeatureAssociationType```. Kaavatietomallissa kaikki tietokohteet, joilla on tunnus ja jota voivat esiintyä erillään toisista kohteista on määritelty kohdetyypeinä (stereotyyppi ```FeatureType```. Sellaiset tietokohteet, joilla ei ole omaa tunnusta ja jotka voivat esiintyä vain kohdetyyppien attribuuttien arvoina on määritelty [ISO 19103][ISO-19103]-standardin ```DataType```-stereotyypin avulla.

[ISO 19109][ISO-19109] -standardin lisäksi tietomalli perustuu muihin paikkatiedon ISO-standardeihin, joista keskeisimpiä ovat [ISO 19103][ISO-19103] (UML-kielen käyttö paikkatietojen mallinnuksessa), [ISO 19107][ISO-19107] (sijaintitiedon mallintaminen) ja [ISO 19108][ISO-19108] (aikaan sidotun tiedon mallintaminen).

### Muulla määritellyt luokat ja tietotyypit

#### CharacterString

Kuvaa yleisen merkkijonon, joka koostuu 0..* merkistä, merkkijonon pituudesta, merkistökoodista ja maksimipituudesta. Määritelty rajapinta-tyyppisenä [ISO 19103][ISO-19103]-standardissa.

#### LanguageString

Kuvaa kielikohtaisen merkkijonon. Laajentaa [CharacterString](#characterstring)-rajapintaa lisäämällä siihen ```language```-attribuutin, jonka arvo on ```LanguageCode```-koodiston arvo. Kielikoodi voi [ISO 19103][ISO-19103]-standardin määritelmän mukaan olla mikä tahansa ISO 639 -standardin osa.

#### Number

Kuvaa yleisen numeroarvon, joka voi olla kokonaisluku, desimaaliluku tai liukuluku. Määritelty rajapintana [ISO 19103][ISO-19103]-standardissa.

#### Integer

Laajentaa [Number](#number)-rajapintaa kuvaamaan numeron, joka on kokonaisluku ilman murto- tai desimaaliosaa. Määritelty rajapintana [ISO 19103][ISO-19103]-standardissa.

#### Decimal

Laajentaa [Number](#number)-rajapintaa kuvaamaan numeron, joka on desimaaliluku. Decimal-rajapinnan toteuttava numero voidaan ilmaista virheettä yhden kymmenysosan tarkkuudella. Määritelty rajapintana [ISO 19103][ISO-19103]-standardissa. Decimal-numeroita käytetään, kun desimaalien käsittelyn tulee olla tarkkaa, esim. rahaan liityvissä tehtävissä.

#### Real

Laajentaa [Number](#number)-rajapintaa kuvaamaan numeron, joka on tarkkudeltaan rajoitettu liukuluku. Real-rajapinnan numero voi ilmaista tarkasti vain luvut, jotka ovat 1/2:n (puolen) potensseja. Määritelty rajapintana [ISO 19103][ISO-19103]-standardissa. Käytännössä esitystarkkuus riippuu numeron tallentamiseen varattujen bittien määrästä, esim. ```float (32-bittinen)``` (tarkkuus 7 desimaalia) ja ```double (64-bittinen)``` (tarkkuus 15 desimaalia).

#### Measure

Mittattavan, numeerisen tiedon ja sen antamiseen käytetyn mittayksikön kuvaamiseen käytettävä yleiskäyttöinen tietorakenne. Määritelty [ISO 19103][ISO-19103]-standardissa. 

#### TM_Object

Aikamääreiden yhteinen yläluokka, käytetään, mikäli arvo voi olla joko yksittäinen ajanhetki tai aikaväli. Määritelty luokkana [ISO 19108][ISO-19108]-standardissa. 

#### TM_Instant

Kuvaa yksittäisen ajanhetken 0-ulotteisena ajan geometriana, joka vastaa pistettä avaruudessa. Määritelty luokkana [ISO 19108][ISO-19108]-standardissa. Aikapisteen arvo on määritelty ```TM_Position```-luokalla yhdistelmänä [ISO 8601][ISO-8601-1]-standin mukaisia päivämäärä- tai kellonaika-kenttiä tai näiden yhdistelmää, tai muuta ```TM_TemporalPosition```-luokan avulla kuvattua aikapistettä. Viimeksi mainitun luokan attribuutti ```indeterminatePosition``` mahdollistaa ei-täsmällisen ajanhetken ilmaisemisen liittämällä mahdolliseen arvoon luokittelun tuntematon, nyt, ennen, jälkeen tai nimi.

#### TM_Period

Kuvaa aikavälin [TM_Instant](#tm_instant)-tyyppisten ```begin```- ja ```end```-attribuuttien avulla. Molemmat attribuutit ovat pakollisia, mutta voivat sisältää tuntemattoman arvon  ```indeterminatePosition = unknown``` -attribuutin arvon avulla annettuna. Määritelty luokkana [ISO 19108][ISO-19108]-standardissa.

#### URI

Määrittää merkkijonomuotoisen Uniform Resource Identifier (URI) -tunnuksen [ISO 19103][ISO-19103]-standardissa. URIa voi käyttää joko pelkkänä tunnuksena tai resurssin paikantimena (Uniform Resource Locator, URL).

#### Geometry

Kaikkien geometria-tyyppien yhteinen rajapinta [ISO 19107][ISO-19107]-standardissa. Tyypillisimpiä [ISO 19107][ISO-19107]-standardin Geometry-rajapintaa laajentavia rajapintoja ovat ```Point```, ```Curve```, ```Surface``` ja ```Solid``` sekä ```Collection```, jota käyttämällä voidaan kuvata geometriakokoelmia (multipoint, multicurve, multisurface, multisolid).

#### Point
Täsmälleen yhdestä pisteestä koostuva geometriatyyppi. Määritelty rajapintana [ISO 19107][ISO-19107]-standardissa.

## Tietomallin yleispiirteet

## Rakennuskohteet

### Rakennuskohde

### RakennusTaiSenOsa

### Rakennus

### RakennuksenOsa

### ErityistäToimintaaVartenRakennettavaAlue

### RakennelmaTaiSenOsa

### Rakennelma

### RakennelmanOsa

### Rakennustietomalli

### Rakennussuunnitelma

### Erityissuunnitelma

### Rakennuspaikka

### RakennuksenOmistaja

### Hissi

### Sisäänkäynti

### RakennuskohteenToimenpide

### RakennuskohteenMuutos

### TunnuksettomanOmistajanTiedot

### RakennuksenOsittelu

### RakennuskohteenSijaintitiedot

### RakennuksenSisäänkäynti

### RakennuksenVaruste

### Materiaalitiedot

#### KantavienRakenteidenRakennusaine

#### Julkisivumateriaali

### RakennuksenKäyttötiedot

#### RakennuksenKäyttötarkoitus

### Energiatiedot

#### Lämmitystapa

#### Jäähdytystapa

#### SähköenergianLähde

#### EnergianKulutus

#### JäähdytysenergianLähde

#### LämmitysenergianLähde

### Talotekniikkatiedot

#### Ilmanvaihtotapa

#### Verkostoliittymä

### UlkokuorenTiedot

### SisätilojenTiedot

## Tilat ja huoneistot

### RakennettuTila

### Huoneisto

### Huone

### OsoiterakenteenMukainenHuoneistoTunnus

### HuoneistonVaruste

## Ilmastoselvitys

### Ilmastoselvitys

### Hiilijalanjälkitiedot

### Hiilikädenjälkitiedot

### RakennuskohdekohtaisetVähähiilisyystiedot

### RakennuspaikkakohtaisetVähähiilisyystiedot

### PoikkeamisenPeruste

## Materiaaliseloste

### Materiaaliseloste

### RakennuspaikkakohtaisetMateriaalimäärät

### RakennuskohdekohtaisetMateriaalimäärät

## Koodistot

### RakennuksenElinkaarenVaihe

{% include common/codelistref.html registry="rakrek" id="rakelinvaih" name="Rakennuksen elinkaaren vaihe" %}

### Rakennusluokitus2018

{% include common/codelistref.html registry="jhs" id="rakennus_1_20180712" name="Rakennusluokitus 2018" %}

### RakennelmanKäyttötarkoitus

{% include common/codelistref.html registry="rytj" id="RakennelmanKayttotarkoitus" name="Rakennelman käyttötarkoitus" %}

### RakentamistoimenpiteenLaji

{% include common/codelistref.html registry="rytj" id="Rakentamistoimenpide" name="Rakentamistoimenpide" %}

### RakennuksenVarusteenLaji

{% include common/codelistref.html registry="rytj" id="RakennusVaruste" name="Rakennuksen varusteet" %}

### Rakennustietomallinlaji

{% include common/codelistref.html registry="rytj" id="rakennuksentietomallinlaji" name="Rakennuksen tietomallin laji" %}

### RakennuskohteenTiedonLaji

{% include common/codelistref.html registry="rytj" id="rakkohteen-tiedon-laji" name="Rakennuskohteen tiedon laji" %}

### RakennuskohteenTiedonLähteenLaji

{% include common/codelistref.html registry="rytj" id="RakennuskohteenTiedonlahde" name="Rakennuskohteen tiedon lähde" %}

### Suojelutapa

{% include common/codelistref.html registry="rytj" id="suojtapa" name="Suojelutapa" %}

### RakennuksenOsittelunLaji

{% include common/codelistref.html registry="rytj" id="rak-osittelun-laji" name="Rakennuksen osittelun laji" %}

### ErityistäToimintaaVartenRakennettavanAlueenTyyppi

{% include common/codelistref.html registry="rakrek" id="erityistatoimintaavartenrakennettavanalueentyyppi" name="Erityistä toimintaa varten rakennettavan alueen tyyppi" %}

### SuhdeMaanpintaan

{% include common/codelistref.html registry="rytj" id="Suhde_pintaan" name="Suhde maan pintaan" %}

### Omistajalaji

{% include common/codelistref.html registry="rytj" id="Omistajalaji" name="Omistajalaji" %}

### OmistuksenLaji

{% include common/codelistref.html registry="rytj" id="Omistuksenlaji" name="Omistuksen laji" %}

### KulttuurihistoriallinenMerkittävyys

{% include common/codelistref.html registry="rakrek" id="kulthistmer" name="Kulttuurihistoriallinen merkittävyys" %}

### LuvanvaraisenRakentamisenAsiakirjanLaji

Laajentaa luokkaa AbstraktiAsiakirjanLaji

Y-alustan koodisto puuttuu toistaiseksi

### KantavienRakenteidenRakennusaineenLaji

{% include common/codelistref.html registry="rytj" id="kantavanrakenteenrakennusaine" name="Kantavan rakenteen rakennusaine" %}

### Rakentamistapa

{% include common/codelistref.html registry="vtj" id="Rake_runkotapa" name="Rakentamistapa" %}

### IlmastoselvityksenHiilijalanjälkisuure

{% include common/codelistref.html registry="rytj" id="is-hiilijalanjalkisuure" name="Ilmastoselvityksen hiilijalanjälkisuure" %}

### IlmastoselvityksenHiilikädenjälkisuure

{% include common/codelistref.html registry="rytj" id="is-hiilikadenjalkisuure" name="Ilmastoselvityksen hiilikädenjälkisuure" %}

### JulkisivunRakennusaineenLaji

{% include common/codelistref.html registry="rytj" id="julkisivunrakennusaine" name="Julkisivun rakennusaineen laji" %}

### Paloluokka

{% include common/codelistref.html registry="rytj" id="Paloluokka" name="Paloluokka" %}

### RakennusosanMateriaalinMäärä

{% include common/codelistref.html registry="rytj" id="ms-rakennusosan-materiaalimaara" name="Rakennuksen rakennusosan materiaalin määrä" %}

### RakentamisessaKäytettävänMaterialilajinMäärä

{% include common/codelistref.html registry="rytj" id="ms-materiaalilajin-maara" name="Rakentamisessa käytettävän materiaalin määrä" %}

### IlmastoselvityksenRajaArvoistaPoikkeamisenPerusteenLaji

{% include common/codelistref.html registry="rytj" id="is-raja-arvoista-poikkeamisen-laji" name="Ilmastoselvityksen raja-arvoista poikkeamisen perusteen laji" %}

### RakennuksenKäyttötarkoitusluokkaEnergiatehokkuudenArvioinnissa

{% include common/codelistref.html registry="rytj" id="rak-kt-luokka-energiatehokkuus" name="Rakennuksen käyttötarkoitusluokka energiatehokkuuden arvionnissa" %}

### Energialuokka

{% include common/codelistref.html registry="rytj" id="Energialuokka" name="Energialuokka" %}

### LämmitystavanLaji

{% include common/codelistref.html registry="rytj" id="lammitystapa" name="Lämmitystavan laji" %}

### JäähdytystavanLaji

{% include common/codelistref.html registry="rytj" id="jaahdytystapa" name="Jäähdytystavan laji" %}

### SähköenergianLähteenLaji

{% include common/codelistref.html registry="rytj" id="sahkoenergianlahde" name="Sähköenergianlähteen laji" %}

### HulevedenKäsittelynLaji

{% include common/codelistref.html registry="rytj" id="hulevedenkasittely" name="Huleveden käsittelyn laji" %}

### JäähdytysenergianLähteenLaji

Y-alustan koodisto puuttuu toistaiseksi

### LämmitysenergianLähteenLaji

{% include common/codelistref.html registry="rytj" id="lammitysenergianlahde" name="Lämmitysenergianlähteen laji" %}

### OstoenergianLaji

{% include common/codelistref.html registry="rytj" id="ostoenergia" name="Ostoenergian laji" %}

### JätevesienKäsittelynLaji

{% include common/codelistref.html registry="rytj" id="jatevesienkasittely" name="Jätevesien käsittelyn laji" %}

### IlmanvaihtotavanLaji

{% include common/codelistref.html registry="rytj" id="ilmanvaihto" name="Ilmanvaihtotavan laji" %}

### VerkostoliittymänLaji

{% include common/codelistref.html registry="rytj" id="verkliit" name="Verkostoliittymän laji" %}

### TalousvedenLaji

{% include common/codelistref.html registry="rytj" id="talousvesi" name="Talousveden laji" %}

### SisäänkäynninTyyppi

{% include common/codelistref.html registry="rytj" id="sisaankaynti" name="Sisäänkäynnin tyyppi" %}

### HissinLaji

{% include common/codelistref.html registry="rytj" id="hissi" name="Hissin laji" %}

### RakennuksenToiminnallisenOsanElinkaarenVaihe

{% include common/codelistref.html registry="rytj" id="rakennuksen-toim-osan-elinkaaren-vaihe" name="Rakennuksen toiminnallisen osan elinkaaren vaihe" %}

### HuoneenTaiMuunTilanKäyttötarkoitus

Y-alustan koodisto puuttuu toistaiseksi

### HuoneenTaiMuunTilanLaji

{% include common/codelistref.html registry="jhs" id="huonelaji" name="Huoneiden ja muiden tilojen lajit" %}

### Huoneistotyyppi

{% include common/codelistref.html registry="rytj" id="Huoneistotyyppi" name="Huoneistotyyppi" %}

### HuoneistonVarusteenLaji

{% include common/codelistref.html registry="rytj" id="HuoneistoVaruste" name="Huoneiston varusteet" %}

### HuoneistonElinkaarenVaihe

{% include common/codelistref.html registry="rytj" id="huon-elinkaaren-vaihe" name="Huoneiston elinkaaren vaihe" %}

### Keittiötyyppi

{% include common/codelistref.html registry="rytj" id="Keittiotyyppi" name="Keittiötyyppi" %}

### HuoneistonMuutoksenLaji

{% include common/codelistref.html registry="rytj" id="huoneistonmuutoksenlaji" name="Huoneiston muutoksen laji" %}

### Käymälätyyppi

{% include common/codelistref.html registry="rytj" id="kaymalatyyppi" name="Käymälätyyppi" %}


[ISO-8601-1]: https://www.iso.org/standard/70907.html "ISO 8601-1:2019 Date and time — Representations for information interchange — Part 1: Basic rules"
[ISO-639-2]: https://www.iso.org/standard/4767.html "ISO 639-2:1998 Codes for the representation of names of languages — Part 2: Alpha-3 code"
[ISO-19103]: https://www.iso.org/standard/56734.html "ISO 19103:2015 Geographic information — Conceptual schema language"
[ISO-19107]: https://www.iso.org/standard/66175.html "ISO 19107:2019 Geographic information — Spatial schema"
[ISO-19108]: https://www.iso.org/standard/26013.html "ISO 19108:2002 Geographic information — Temporal schema"
[ISO-19109]: https://www.iso.org/standard/59193.html "ISO 19109:2015 Geographic information — Rules for application schema"
[ISO-19505-2]: https://www.iso.org/standard/52854.html "ISO/IEC 19505-2:2012, Information technology — Object Management Group Unified Modeling Language (OMG UML) — Part 2: Superstructure"

