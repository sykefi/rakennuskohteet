---
layout: "default"
description: ""
id: "laatusaannot"
status: "Luonnos"
---
# Laatusäännöt
{:.no_toc}

1. 
{:toc}

## Johdanto

## Yhteiset laatusäännöt

### UML-mallin mukaisuus
{% include common/clause_start.html type="req" id="laatu/vaat-uml-mukaisuus" %}
Tietomallin loogisen tietomallin toteutusten tulee noudattaa tietomallin [UML-kielisen luokkakaavion](./uml/) määrityksiä luokkien attribuuttien ja assosiaatioiden kardinaliteetin ja tyypin suhteen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-uml-toteutus" %}
Kunkin fyysisen tietomallin kuvauksessa tulee määritellä minkälaista rakennetta ja tietotyyppiä kukin loogisen tietomallin luokka ja attribuutin tyyppi vastaa fyysisessä mallissa. Attribuutit ja assosiaatiot, joiden kardinaliteetti on loogisessa tietomallissa ```0..1``` tai ```0..*``` voivat puuttua fyysisen tietomallin mukaisista objekteista.
{% include common/clause_end.html %}

### Tunnisteet ja sisäisten viittausten eheys
{% include common/clause_start.html type="req" id="laatu/vaat-tunnukset-viittaukset" %}
Tietomallin versioitavilla tietokohteilla tulee olla yksilöivät tunnukset, joiden luomisessa ja käyttämisessä viittaamiseen toisiin tietokohteisiin tulee noudattaa elinkaarisääntöjen luvun [Tunnukset ja niiden hallinta](elinkaarisaannot.html#tunnukset-ja-niiden-hallinta) vaatimuksia.
{% include common/clause_end.html %}

### Elinkaarisääntöjen mukaisuus
{% include common/clause_start.html type="req" id="laatu/vaat-elinkaarisaannot" %}
Tietomallin mukaisten aineistojen tulee noudattaa [elinkaarisääntöjen](elinkaarisaannot.html) vaatimuksia, ja niiden on suositeltavaa noudattaa elinkaarisääntöjen suosituksia. Vaatimukset ja suositukset on erotettu selkeästi elinkaarisääntöjen muusta sisällöstä.
{% include common/clause_end.html %}

### Merkkijonojen käyttö
#### Merkistöt
{% include common/clause_start.html type="req" id="laatu/vaat-merkisto-utf8" %}
Kaikki tietomallin tekstimuotoiset sisällöt on tiedonsiirtoa varten koodattava käyttäen UTF-8 -merkistökoodausta.
{% include common/clause_end.html %}

#### Monikielinen sisältö ja kielikoodit
Kaikki tietomallin tekstimuotoinen sisältö ilmaistaan ISO 19103 -standardin määrittelemän [LanguageString](dokumentaatio/#languagestring)-luokan avulla.

{% include common/clause_start.html type="req" id="laatu/vaat-monikielisyys-kielikoodi" %}
Kunkin LanguageString-luokan objektin tulee toteuttaa ```language```-attribuutti, jonka arvona on ISO 639-2 -standardin mukainen terminologinen, kolmekirjaiminen kielikoodi code (ISO 639-2/T).
{% include common/clause_end.html %}

{% include common/note.html content="ISO 639-2/T koodilistan mukaiset koodit Suomen virallisille kielille ovat ```fin``` (suomi), ```swe``` (ruotsi), ```smn``` (inarinsaami), ```sms```(koltansaami) ja ```sme``` (pohjoissaami). Muita Suomessa paljon puhuttujen kielten ISO 639-2/T -koodeja: ```rus``` (venäjä), ```est``` (viro), ```ara```(arabia),  ```eng``` (englanti), ```som``` (somali), ```kur``` (kurdi)." %}

Tekstimuotoiset attribuutit on määritelty siten, että ne sisältävät nolla tai enemmän LanguageString-tyyppisiä arvoja.

{% include common/clause_start.html type="req" id="laatu/vaat-yksi-teksti-per-kieli" %}
Kunkin tekstimuotoista sisältöä kuvaavan attribuutin arvoina tulee olla enintään yksi LanguageString-tyyppinen arvo kutakin kielikoodia (```language```-attribuutti) kohti.
{% include common/clause_end.html %}

#### Enimmäispituudet
{% include common/clause_start.html type="req" id="laatu/vaat-merkijono-pituus" %}
Kunkin yhdellä kielellä annetun LanguageString-tyyppisen merkkijonon enimmäispituus on 2048 merkkiä.
{% include common/clause_end.html %}

{% include common/note.html content="Valittu 2048 merkin raja perustuu arvioon tietomallissa tarvittavien merkkijonojen tyypillisistä pituuksista. Merkkijonojen enimmäispituuden määrääminen loogisen tietomallin tasolla on jossain määrin kajoamista mallin tekniseen toteutukseen, mutta yhteentoimivuuden takaamisen näkökulmasta on tärkeää, että kaikkissa fyysisissä tietomalleissa varataan yhtä suuri maksimimäärä merkkejä tekstisisältöjen tallentamiseen. Muutoin on riskinä oikeusvaikuttteisen tiedon katoaminen tiedonsiirrossa tai -käsittelyproseseissa." %}

### Geometriat

#### Geometriatyypit
{% include common/clause_start.html type="req" id="laatu/vaat-geom-piste-maar" %}
Pistemäiset geometriat toteuttavat ISO 19107 -standardin määrittelemän ```Point```-rajapinnan.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-geom-2d-alue-maar" %}
Aluemaiset geometriat toteuttavat ISO 19107 -standardin määrittelemän ```Surface```-rajapinnan.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-geom-3d-kappale-maar" %}
3-ulotteiset kappalegeometriat toteuttavat joko ISO 19107 -standardin määrittelemän ```Solid```-rajapinnan.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-geom-kokoelmat-maar" %}
Geometriakokoelmat toteuttavat ISO 19107 -standardin määrittelemän ```Collection```-rajapinnan. Monipiste (multipoint) -geometriat rakentuvat ```Point```-rajapinnan, monialue (multisurface) -geometriat ```Surface```-rajapinnan ja monikappale (multisolid) -geometriat ```Solid```-rajapinnan toteuttavista osista (```element```-attribuutti).
{% include common/clause_end.html %}

{% include common/note.html content="Tietomalli ei vaadi kaikkien ISO 19107 -standardin mukaisten geometriatyyppien tukemista. Loogisen tietomallin mukaiset fyysiset tietomallit voivat rajoittaa mahdollisia geometriatyyppejä ja niiden ominaisuuksia." %}

#### Sallitut koordinaatistot ja koordinaattijärjestys

Rakennetun ympäristön tietojärjestelmä tukee seuraavia koordinaatistoja:

Tiedon luovutuksen koordinaatistot
* EPSG:4326, WGS84
  * Käytössä myös IFC-mallissa 
* EPSG:3857, Google Web Mercator
* Tiedon luovutusrajapinnan käyttäjä voi pyytää vastauksen haluamassaan tuetussa koordinaatistossa, jolloin tietojärjestelmä muuntaa tarvittaessa varannossa olevan tiedon haluttuun kohdekoordinaatistoon.

Tiedon luovutuksen ja vastaanoton koordinaatistot
* EPSG:3067, valtakunnallinen koordinaatisto.
* EPSG:3873-3885 koordinaatistot tiedon luovutuksessa / tiedon vastaanotossa
* Tiedon toimituksen yhteydessä tulee tallentaa tieto koordinaattijärjestelmästä ja korkeusjärjestelmästä (N2000), jossa tieto toimitettu.

{% include common/clause_start.html type="req" id="laatu/vaat-koord-jarjestys" %}
Geometrioiden ilmaisemisessa tulee noudattaa kunkin koordinaatiston määritelmässä annettua virallista koordinaattijärjestystä.
{% include common/clause_end.html %}

#### Geometrinen ja topologinen eheys

{% include common/clause_start.html type="req" id="laatu/vaat-suljetut-ringit" %}
Mikäli viiva on osa aluemaisen geometrian reunaviivaa, on sen oltava suljettu, eli sen alku- ja loppuppisteiden on oltava samat.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-alue-kielletyt-leikkaukset" %}
Aluemaisen geometrian ulkoreunan ja reikien reunaviivat eivät saa leikata itseään tai toisiaan. Kukin reunaviiva saa koskettaa alueen ulkoreunaa tai reiän reunaa, mukaanlukien se itse, vain yksittäisissä pisteissä.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-yhteneva-alue" %}
Aluemaisen geometrian sisäosan on oltava yhtenevä, eli minkä tahansa kahden alueen sisäpisteen välillä on voitava muodostaa yhtenäinen käyrä, joka kulkee kokonaan alueen sisällä.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-mitattava-alue" %}
Aluemaisen geometrian sisäosan pinta-ala on oltava mitattavissa, eli alueeseen tulee sisältyä pisteitä, jotka eivät ole osa alueen ulkoreunaa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-pinnan-orientaatio" %}
Aluemaisten geometrioiden kiertosuuntien tulee noudattaa ISO 19107 -standardin määritelmää: Geometrioiden reunojen kiertosuunnat tulee valita siten, että pinnan yläpuolelta katsottuna ulkorajan reunan kiertosuunta on vastapäivään ja pinnan mahdollisten reikien reunojen kiertosuunnat ovat myötäpäivään. Mikäli pinta on osa 3-ulotteisten geometrian ulkorajaa, ulkopuoli vastaa yläpuolta.
{% include common/clause_end.html %}

### Päivämäärät ja kelloanajat
Tietomallin yksittäisiä ajanhetkiä kuvaavat attribuutit ovat ISO 19108 -standardin määrittämää tyyppiä [TM_Instant](dokumentaatio/#tm_instant) ja aikavälejä kuvaavat attribuutit tyyppiä [TM_Period](dokumentaatio/#tm_period). Päivämäärät annetaan käyttäen Gregoriaanista kalenteria ja kellonajat käyttäen 24 tunnin kelloaikamuotoa alkaen kellonajasta 00:00:00.000  ja päättyen ajanhetkeen 23:59:59.999 (tunti, minuutti, sekunti, millisekunti).

{% include common/clause_start.html type="req" id="laatu/vaat-ajanhetki-tarkkuus" %}
Yksittäisiä ajanhetkiä kuvaavat attribuutit ilmaistaan joko pelkän päivämäärän tai päivämäärän ja kelloajan avulla. Päivämäärät ilmaistaan antamalla vuoden, kuukauden ja kuukauden päivän numeeriset arvot. Kellonajat ilmaistaan vähintään yhden minuutin ja enintään yhden millisekunnin tarkkuudella antamalla tunnin, minuutin, sekunnin ja millisekunnin numeeriset arvot.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-aikavyohykkeet" %}
Päivämäärien ja kellonaikojen yhteydessä voidaan antaa myös tieto aikavyöhykkeestä tai aikojen poikkeamasta UTC-ajasta. Mikäli muuta ei tietoa ei anneta, tulee ajanhetkitiedot tulkita siten, että ne kuvaavat Suomen aikaa noudattaen kyseisellä ajanhetkellä voimassaolleita asetuksia kesäaikaan liittyen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="rec" id="laatu/suos-ajanhetki-muoto" %}
Mikäli fyysinen tietomalli ei aseta ajanhetken muodolle rajoituksia, on suositeltavaa käyttää [IETF RFC 3339 Date and Time on the Internet: Timestamps](https://tools.ietf.org/html/rfc3339)-standardin määrittelemää syntaksia.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-aikavali-maar" %}
Aikavälejä kuvaavat attribuutit voidaan antaa joko sekä alku- että loppuajanhetken avulla tai vain joko alku- tai loppuajanhetken avulla. Mikäli alkuajanhetkeä ei anneta, tulkitaan aikavälin sisältävän minkä tahansa ajanhetken loppuajanhetkeen saakka. Vastaavasti mikäli loppuajanhetkeä ei anneta, tulkitaan aikavälin sisältävän minkä tahansa ajanhetken alkujanhetkestä lähtien.
{% include common/clause_end.html %}

## Luokkakohtaiset säännöt

### Rakennuspaikka

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuspaikan-osoite" %}
[Rakennuspaikka](dokumentaatio/#rakennuspaikka)-luokan objektin, joka on liitetty [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan objektiin assosiaation ```paikka``` avulla, tulee sisältää vähintään yksi assosiaation ```rakennuspaikanOsoite``` avulla kuvattu osoitetieto.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuspaikan-kaava" %}
[Rakennuspaikka](dokumentaatio/#rakennuspaikka)-luokan objektin, joka on liitetty [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan objektiin assosiaation ```paikka``` avulla, ja joka sijaitsee rakentamista ohjaavan kaavan alueella, tulee viitata rakentamista kyseisellä rakennuspaikalla ohjaavaan kaavaan assosiaation ```rakentamistaOhjaavaKaava``` avulla.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuspaikan-kaavayksikko" %}
Mikäli vähintään yksi [Rakennuspaikka](dokumentaatio/#rakennuspaikka)-luokan objektin ```rakentamistaOhjaavaKaava``` assosiaation {% include common/moduleLink.html moduleId="kaavatiedot" path="looginenmalli/dokumentaatio/#kaava" title="Kaava" %}-luokan attribuutin ```laji``` koodiarvo on jokin koodin ```3 - Asemakaava``` alikoodi, on rakennuspaikan kaavayksikkö annettava assosiaation ```kaavayksikkö``` avulla.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuspaikan-geometria" %}
[Rakennuspaikka](dokumentaatio/#rakennuspaikka)-luokan objektilla on oltava ```geometria``` attribuutin arvo, joka kuvaa kyseisen rakennuspaikan sijainnin tai alueen joko piste- tai aluemaisena.
{% include common/clause_end.html %}

### RakennuskohteenToimenpide

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuskohteen-toimenpide-maaritelma" %}
[RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide) kuvaa toimenpiteen, joka kohdistuu yhden Rakennuskohteen rakentamiseen, korjaamiseen, laajentamiseen tai purkamiseen. Erikoistapauksena sama toimenpide voi kohdistua useampaan kuin yhteen Rakennuskohteeseen, kun toimenpide kohdistuu useampaan [RakennuksenOsa](dokumentaatio/#rakennuksenosa)- tai [RakennelmanOsa](dokumentaatio/#rakennelmanosa)-luokan objektiin, tai kun toimenpiteen johdosta yhdistetään useampia aiemmin erillisiä Rakennuskohteita yhdeksi tai kun pilkotaan yksi Rakennnuskohde useammaksi Rakennuskohteeksi.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuskohteen-toimenpide-rakennuspaikat" %}
[Rakennuspaikan](dokumentaatio/#rakennuspaikka), johon rakennuskohteen toimenpide kohdistuu, tulee liittyä [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan objektiin assosiaation ```paikka``` avulla.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-toimenpiteen-kohde" %}
[RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan objektin on sisällettävä vähintään yksi [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokan kuvaama tietokokonaisuus attribuutin ```suunniteltuMuutos``` arvona. Samaan rakennuskohteen toimenpiteeseen voi kuulua saman rakennuksen tai rakennelman eri osia koskevia suunniteltuja muutoksia. 
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-laajentamistoimenpiteen-muutostiedot" %}
Mikäli [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan objektin attribuutilla ```toimenpiteenLaji``` on arvo [02 - Laajentaminen](http://uri.suomi.fi/codelist/rytj/Rakentamistoimenpide/code/02), tulee sen rakenteisella attribuutin ```suunniteltuMuutos``` attribuuteilla ```tilavuudenMuutos```, ```kerrosalanMuutos``` ja ```kokonaisalanMuutos``` olla arvot.
{% include common/clause_end.html %}

{% include common/clause_start.html type="rec" id="laatu/suos-laajentamistoimenpiteen-laajennusosa" %}
Mikäli [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan objektin attribuutilla ```toimenpiteenLaji``` on arvo [02 - Laajentaminen](http://uri.suomi.fi/codelist/rytj/Rakentamistoimenpide/code/02), tulisi rakennuksen laajennososa kuvata omana [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektinaan siten, että ```suunniteltuMuutos```-attribuutin assosiaatiolla ```kohdeMuutoksenJälkeen``` viitattu [Rakennus](dokumentaatio/#rakennus)-luokan objekti sisältää kyseisen laajennusosan sen sellaisen rakenteisen attribuutin ```osittelu``` assosiaation ```osa``` kautta liitettynä, jonka ```ositteluperuste```-attribuutilla on arvo [2 - Rakentamishistoriaan perustuva osittelu](http://uri.suomi.fi/codelist/rytj/rak-osittelun-laji/code/2). Kyseisellä [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektilla on tällöin myös oltava rakenteisen attribuutin ```ulkokuorenTiedot``` attribuuttien ```tilavuus```, ```kerrosala``` ja ```kokonaisala```.
{% include common/clause_end.html %}

### Rakennuskohde

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuskohteen-geometria" %}
[Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan jonkin konkreettisen aliluokan objektilla on oltava ```geometria``` attribuutin arvo, joka kuvaa kyseisen rakennuskohteen sijainnin.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuskohteen-kokonaisala" %}
Mikäli [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan jonkin konkreettisen aliluokan objektilla on attribuutin ```kokonaisala``` arvo, sen arvon tulee olla kokonaisluku väliltä 1 - 9999999 (1 <= x < 10^7), ja yksikkö neliömetri (```m2```).
{% include common/clause_end.html %}

### RakennuskohteenSijaintitiedot

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuskohteen-sijainnin-kuntanumero" %}
Mikäli [RakennuskohteenSijaintitiedot](dokumentaatio/#rakennuskohteensijaintitiedot)-luokan objektille on annettu ```kuntanumero```-attribuutin arvo, sen tulee vastata rakennuskohteen sijaintikuntaa tiedon päivityshetkellä. ```kuntanumero```-attribuutin arvon on oltava merkkijono, joka esittää numeroa 0-999 siten, että numeroiden 1-9 edessä käytetään kahta alkunollaa ja numeroiden 10-99 edessä yhtä alkunollaa.
{% include common/clause_end.html %}

### RakennuskohteenOmistaja

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuskohteen-omistaja" %}
[RakennuskohteenOmistaja](dokumentaatio/#rakennuskohteenomistaja)-luokan objektin on sisällettävä vain joko ```tunnuksellinenOmistaja```-assosiaation tai ```tunnuksetonOmistaja```-attribuutin arvo. Ensisijaisesti on annettava {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#toimija" title="Toimija" %}-rajapinnan mukainen tieto assosiaation ```tunnuksellinenOmistaja``` kautta. Mikäli omistajan yksilöivää tunnusta ei ole saatavissa, esimerkiksi ulkomaisen omistajan tapauksessa, annetaan omistajan tiedot luokan [TunnuksettomanOmistajanTiedot](dokumentaatio/#tunnuksettomanomistajantiedot) kuvaaman rakenteisen ```tunnuksetonOmistaja```-attribuutin avulla.
{% include common/clause_end.html %}

### RakennuskohteenMuutos
{% include common/clause_start.html type="req" id="laatu/vaat-kohde-ennen-muutosta" %}
RakennuskohteenMuutos-luokan assosiaation ```kohdeEnnenMuutosta``` tulee viitata [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan objektiin, johon suunniteltu muuutos kohdistuu. Mikäli kyseessä on uusi rakennuskohde (esim. uudisrakennus), ei assosiaatiota ```kohdeEnnenMuutosta``` käytetä.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-kohde-muutoksen-jalkeen" %}
RakennuskohteenMuutos-luokan assosiaation ```kohdeMuutoksenJälkeen``` tulee viitata [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan objektiin, joka kuvaa rakennuskohteen uutta tilaa suunnitellun muutoksen toteuttamisen jälkeen.
{% include common/clause_end.html %}

### HuoneistonMuutos

{% include common/clause_start.html type="req" id="laatu/vaat-huoneiston-muutos-huonemaara" %}
Mikäli [HuoneistonMuutos](dokumentaatio/#huoneistonmuutos)-luokan objektilla on attribuutin ```huonemääränMuutos``` arvo, sen arvon tulee olla kokonaisluku, joka on yli -1000 ja alle 1000.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-huoneiston-muutos-pakolliset-attribuutit" %}
Mikäli [HuoneistonMuutos](dokumentaatio/#huoneistonmuutos)-luokan objektilla on attribuutin ```laji``` on koodi [01 - Lisäys](http://uri.suomi.fi/codelist/rytj/huoneistonmuutoksenlaji/code/01) tai [02 - Muutos](http://uri.suomi.fi/codelist/rytj/huoneistonmuutoksenlaji/code/02), tulee siihen assosiaation ```muuttunutHuoneisto``` kautta liittyvällä [Huoneisto](dokumentaatio/#huoneisto)-luokan objektin seuraavilla attribuuteilla olla arvo:

* ```huoneidenLukumäärä```
* ```keittötyyppi``` ja
* ```huoneistoala```
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-huoneiston-tilavuuden-muutos" %}
Mikäli [HuoneistonMuutos](dokumentaatio/#huoneistonmuutos)-luokan objektilla on attribuutin ```tilavuudenMuutos``` arvo, sen arvon tulee olla kokonaisluku väliltä -9999999 - 9999999 (-10^7 < x < 10^7), ja yksikkö neliömetri (```m2```).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-huoneiston-kerrosalan-muutos" %}
Mikäli [HuoneistonMuutos](dokumentaatio/#huoneistonmuutos)-luokan objektilla on attribuutin ```kerrosalanMuutos``` arvo, sen arvon tulee olla kokonaisluku väliltä -9999999 - 9999999 (-10^7 < x < 10^7), ja yksikkö neliömetri (```m2```).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-huoneiston-kokonaisalan-muutos" %}
Mikäli [HuoneistonMuutos](dokumentaatio/#huoneistonmuutos)-luokan objektilla on attribuutin ```kokonaisalanMuutos``` arvo, sen arvon tulee olla kokonaisluku väliltä -9999999 - 9999999 (-10^7 < x < 10^7), ja yksikkö neliömetri (```m2```).
{% include common/clause_end.html %}

{% include common/question.html content="HuoneistonMuutos.muutoksenLaji-attribuutin arvojen (lisäys, muutos, poisto) arvojen yhteyttä liittyvien Huoneistojen ```elinkaarenVaihe```-attribuutin arvoihin tulisi ehkä tarkentaa. Kaikki kombinaatiot eivät liene mielekkäitä, esim. puretun huoneiston lisäys rakennukseen" %}

### RakennusTaiSenOsa

{% include common/clause_start.html type="req" id="laatu/vaat-sahkolammitys-sahkoliittyma" %}
Mikäli [RakennusTaiSenOsa](dokumentaatio/#rakennustaisenosa)-luokan konkreettisen aliluokan rakenteisella attribuutilla ```energiatiedot``` attribuutilla ```lämmitysenergianLähde``` on arvo, joka on koodiston [Lämmitysenergianlähteen laji](http://uri.suomi.fi/codelist/rytj/lammitysenergianlahde) koodi [04 - Sähkö](http://uri.suomi.fi/codelist/rytj/lammitysenergianlahde/code/04), niin sillä on oltava
* rakenteisen attribuutin ```varuste``` arvo, jonka attribuutti ```laji``` on koodisto [Rakennuksen varusteet](http://uri.suomi.fi/codelist/rytj/RakennusVaruste) koodi [01 - Sähkö](http://uri.suomi.fi/codelist/rytj/RakennusVaruste/code/01) ja attribuutin ```kuuluuKohteeseen``` arvo ```true```, ja
* rakenteisen attribuutin ```talotekniikkatiedot``` rakenteisen attribuutin ```verkostoliittymä``` arvo, jonka attribuutin ```laji``` arvo on koodiston [Verkostoliittymän laji](http://uri.suomi.fi/codelist/rytj/verkliit) koodi [04 - sähkö](http://uri.suomi.fi/codelist/rytj/verkliit/code/04).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-sahkolammitystapa-sahkoenergianlahde" %}
Mikäli [RakennusTaiSenOsa](dokumentaatio/#rakennustaisenosa)-luokan konkreettisen aliluokan rakenteisella attribuutilla ```energiatiedot``` attribuutilla ```lämmitystapa``` on arvo, joka on koodiston [Lämmitystavan laji](http://uri.suomi.fi/codelist/rytj/lammitystapa) koodi [03 - Sähkölämmitys](http://uri.suomi.fi/codelist/rytj/lammitystapa/code/03), niin sen rakenteisen attribuutin ```energiatiedot``` attribuutilla ```lämmitysenergianLähde``` on oltava arvo, joka on koodiston [Lämmitysenergianlähteen laji](http://uri.suomi.fi/codelist/rytj/lammitysenergianlahde) koodi [04 - Sähkö](http://uri.suomi.fi/codelist/rytj/lammitysenergianlahde/code/04).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-lammitystapa-lammitysenergianlahde" %}
Mikäli [RakennusTaiSenOsa](dokumentaatio/#rakennustaisenosa)-luokan konkreettisen aliluokan rakenteisella attribuutilla ```energiatiedot``` attribuutilla ```lämmitystapa``` on arvo, joka on koodiston [Lämmitystavan laji](http://uri.suomi.fi/codelist/rytj/lammitystapa) koodi [07 - Ei kiinteää lämmityslaitetta](http://uri.suomi.fi/codelist/rytj/lammitystapa/code/07), niin sen rakenteisen attribuutin ```energiatiedot``` attribuutilla ```lämmitysenergianLähde``` ei saa olla arvoa.

Toisaalta mikäli ```lämmitystapa``` on arvo, joka koodiston [Lämmitystavan laji](http://uri.suomi.fi/codelist/rytj/lammitystapa) on jokin muu koodi koodi kuin [07 - Ei kiinteää lämmityslaitetta](http://uri.suomi.fi/codelist/rytj/lammitystapa/code/07), tulee sen rakenteisen attribuutin ```energiatiedot``` attribuutilla ```lämmitysenergianLähde``` olla arvo.
{% include common/clause_end.html %}

### Rakennus

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-geometria" %}
[Rakennus](dokumentaatio/#rakennus)-luokan objektilla on oltava ```geometria``` attribuutin arvo, joka kuvaa kyseisen rakennuksen sijainnin aluemaisena tai 3-ulotteisena geometriana. Mikäli geometria annetaan aluemaisena, sen tulee vastata rakennuksen pohjapinta-alaa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-ensisijainen-sisaankaynti" %}
[Rakennus](dokumentaatio/#rakennus)-luokan objektilla voi olla enintään yksi sellainen assosiaatio ```sisäänkäynti```, jonka assosiaatioluokan [RakennuksenSisäänkäynti](dokumentaatio/#rakennuksensisäänkäynti) attribuutin ```ensisijainen``` arvo on ```true```. 
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-tilavuus-pakollinen" %}
[Rakennus](dokumentaatio/#rakennus)-luokan objektin rakenteisen attribuutin ```ulkokuorenTiedot``` attribuutilla ```tilavuus``` tulee olla arvo.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-kerrosala-pakollinen" %}
[Rakennus](dokumentaatio/#rakennus)-luokan objektin rakenteisen attribuutin ```ulkokuorenTiedot``` attribuutilla ```kerrosala``` tulee olla arvo.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-kerrosluku-pakollinen" %}
[Rakennus](dokumentaatio/#rakennus)-luokan objektin rakenteisen attribuutin ```ulkokuorenTiedot``` attribuutilla ```kerrosluku``` tulee olla arvo.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-kokonaisala-pakollinen" %}
[Rakennus](dokumentaatio/#rakennus)-luokan objektin attribuutilla ```kokonaisala``` tulee olla arvo.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-asuinrakennuksen-vahimmaispinta-ala" %}
Mikäli [Rakennus](dokumentaatio/#rakennus)-luokan objektin rakenteisen attribuutin ```käyttötiedot``` rakenteisen attribuutin ```käyttötarkoitus``` attribuutin ```ensisijainen``` arvo on ```true``` ja attribuutin ```laji``` arvo on [Rakennusluokitus 2018](http://uri.suomi.fi/codelist/jhs/rakennus_1_20180712)-koodiston koodi [01 -Asuinrakennukset](http://uri.suomi.fi/codelist/jhs/rakennus_1_20180712/code/01) tai jokin sen alakoodeista, ja rakenteisen attribuutin ```ulkokuorenTiedot``` attribuutille ```kerrosala``` on annettu arvo, sen arvon tulee olla suurempi kuin ```7```, ja yksikön neliömetri (```m2```).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-asuinrakennuksen-aanestysaluenro" %}
Mikäli [Rakennus](dokumentaatio/#rakennus)-luokan objektin rakenteisen attribuutin ```käyttötiedot``` rakenteisen attribuutin ```käyttötarkoitus``` attribuutin ```ensisijainen``` arvo on ```true``` ja attribuutin ```laji``` arvo on [Rakennusluokitus 2018](http://uri.suomi.fi/codelist/jhs/rakennus_1_20180712)-koodiston koodi [01 -Asuinrakennukset](http://uri.suomi.fi/codelist/jhs/rakennus_1_20180712/code/01) tai jokin sen alakoodeista, ja rakenteisen attribuutin ```sijaintitiedot``` attribuutilla ```äänestysaluenumero``` on oltava arvo.
{% include common/clause_end.html %}

#### Rakennuksen osittelut

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-osittelu-maaritelma" %}
[Rakennus](dokumentaatio/#rakennus)-luokan ```osittelu```-attribuutin avulla kuvataan rakennuksen osittelut, joissa rakennus on jaettu [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan avulla kuvattaviin loogisiin tai fyysisiin osiin esimerkiksi sen rakentamishistorian tai käyttötarkoituksen perusteella.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-uniikki-osittelu" %}
[Rakennus](dokumentaatio/#rakennus)-luokan objekti voi sisältää enintään yhden rakenteisen ```osittelu```-attributin arvon kutakin attribuutin ```osittelunPeruste``` arvoa kohti.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-osittelun-geometriat" %}
[Rakennus](dokumentaatio/#rakennus)-luokan objektiin sen eri ```osittelu```-attribuuttien arvojen avulla liitettyjen [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektien ```geometria```-attribuutin ilmaisemat alueet voivat olla päällekkäisiä tai sisäkkäisiä keskenään tai leikata toisiaan.

Kunkin yhden [Rakennus](dokumentaatio/#rakennus)-luokan objektin sisältämien [RakennuksenOsittelu](dokumentaatio/#rakennuksenosittelu)-luokan assosiaation ```osa``` avulla liitettyjen [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektien ```geometria```-attribuutin ilmaisemat alueet eivät kuitenkaan saa olla päällekkäisiä eivätkä leikata toisiaan, mikäli niitä ei ole rajattu pystysuunnassa ei-päällekkäisille korkeustasoille ```pystysuuntainenRajaus```-attribuutin arvojen avulla.
{% include common/clause_end.html %}

Osittelut mahdollistavat esimerkiksi [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-, [Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)- ja [Materiaaliselostus](dokumentaatio/#materiaaliselostus)-luokkien objektien kohdistamisen vain osaan rakennusta.

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-historiaosittelu" %}
Mikäli [Rakennus](dokumentaatio/#rakennus)-luokan objekti kuvaava rakennusta, jota on luvanvaraisesti laajennettu alkuperäisestä, tai sen osia on luvanvaraisesti purettu, sen tulee sisältää yksi sellainen rakenteisen ```osittelu```-attribuutin arvo, jonka attribuutin ```osittelunPeruste``` arvo on ```2 - Rakentamishistoriaan perustuva osittelu```. Rakennuksen laajennusosat tai puretut osat tulee kuvata kyseiseen ```osittelu```-attribuuttiin sen assosiaation ```osa``` kautta liitettyinä [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objekteina. Suunniteltuja laajennusosia tai purettavia osia kuvaavat RakennuksenOsa-luokan objektit tulee eritellä toteuman mukaisista tiedoista niiden  ```tiedonLaji```-attribuutin avulla, kuten kuvattu elinkaarisääntöjen luvussa [Suunnitelman ja toteuman mukaiset Rakennuskohteet](elinkaarisaannot.html##suunnitelman-ja-toteuman-mukaiset-rakennuskohteet).
{% include common/clause_end.html %}


### RakennuksenOsa

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-osan-geometria" %}
[RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektilla on oltava ```geometria``` attribuutin arvo, joka kuvaa kyseisen rakennuksen osan aluemaisena tai 3-ulotteisena geometriana. Mikäli geometria annetaan aluemaisena, sen tulee vastata rakennuksen osan pohjapinta-alaa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-osien-geometriat" %}
[Rakennus](dokumentaatio/#rakennus)-luokan objektiin sisältyvien [RakennuksenOsittelu](dokumentaatio/#rakennuksenosittelu)-luokan assosiaation ```osa``` avulla liitettyjen [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektien ```geometria```-attribuutin arvojen tulee olla sen [Rakennus](dokumentaatio/#rakennus)-luokan objektin ```geometria```-attribuutin arvon sisällä, johon ne kuuluvat, poislukien osat, jotka ovat elinkaaren vaiheissa ```05 - tuhoutunut```, ```06 - purettu``` tai ```07 - yhdistetty tai jaettu```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="rec" id="laatu/suos-rakennuksen-osan-tilat" %}
[RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektiin tulisi liittää siihen fyysisesti sisältyvät [RakennettuTila](dokumentaatio/#rakennettutila)-luokan objektit attribuutin ```sisältyväTila``` avulla.
{% include common/clause_end.html %}

{% include common/clause_start.html type="rec" id="laatu/suos-rakennuksen-osan-huoneistot" %}
[RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektiin tulisi liittää siihen fyysisesti sisältyvät [Huoneisto](dokumentaatio/#huoneisto)-luokan objektit attribuutin ```sisältyväHuoneisto``` avulla.
{% include common/clause_end.html %}

### Rakennelma

{% include common/clause_start.html type="req" id="laatu/vaat-rakennelman-geometria" %}
[Rakennelma](dokumentaatio/#rakennelma)-luokan objektilla on oltava ```geometria``` attribuutin arvo, joka kuvaa kyseisen rakennelman sijainnin aluemaisena tai 3-ulotteisena geometriana. Mikäli geometria annetaan aluemaisena, sen tulee vastata rakennelman pohjapinta-alaa.
{% include common/clause_end.html %}

### RakennelmanOsa

{% include common/clause_start.html type="req" id="laatu/vaat-rakennelman-osan-geometria" %}
[RakennelmanOsa](dokumentaatio/#rakennelmanosa)-luokan objektilla on oltava ```geometria``` attribuutin arvo, joka kuvaa kyseisen rakennelman osan aluemaisena tai 3-ulotteisena geometriana. Mikäli geometria annetaan aluemaisena, sen tulee vastata rakennelman osan pohjapinta-alaa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennelman-ja-sen-osien-geometriat" %}
[Rakennelma](dokumentaatio/#rakennelma)-luokan objektiin assosiaation ```osa``` avulla sisältyvien [RakennelmanOsa](dokumentaatio/#rakennelmanosa)-luokkien objektien ```geometria```-attribuutin arvojen tulee olla sen [Rakennelma](dokumentaatio/#rakennelma)-luokan objektin ```geometria```-attribuutin arvon sisällä, johon ne kuuluvat, poislukien osat, jotka ovat elinkaaren vaiheissa ```05 - tuhoutunut```, ```06 - purettu``` tai ```07 - yhdistetty tai jaettu```.
{% include common/clause_end.html %}

### RakennettuTila

{% include common/clause_start.html type="rec" id="laatu/suos-tilan-yhteys-rakennuksen-osaan" %}
[RakennettuTila](dokumentaatio/#rakennettutila)-luokan objekti tulisi liittää kuhunkin [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektiin, johon se fyysisesti sisältyy käyttäen assosiaatiota ```sisältäväRakennuksenOsa```.
{% include common/clause_end.html %}

### Huone

{% include common/clause_start.html type="req" id="laatu/vaat-huoneala-vahimmaismaara" %}
Mikäli [Huone](dokumentaatio/#huone)-luokan objektin attribuutille ```huoneala``` on annettu arvo, sen tulee olla suurempi kuin ```7```, yksikkönä neliömetri (```m2```). 
{% include common/clause_end.html %}

### Huoneisto

{% include common/clause_start.html type="req" id="laatu/vaat-huoneiston-tunnus" %}
Mikäli [Huoneisto](dokumentaatio/#huoneisto)-luokan objektilla ei ole attribuutin ```pysyväHuoneistoTunnus``` arvoa, sillä tulee olla attribuutin ```osoiteHuoneistoTunnus``` arvo.
{% include common/clause_end.html %}

{% include common/clause_start.html type="rec" id="laatu/suos-huoneiston-yhteys-rakennuksen-osaan" %}
[Huoneisto](dokumentaatio/#huoneisto)-luokan objekti tulisi liittää kuhunkin [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektiin, johon se fyysisesti sisältyy käyttäen assosiaatiota ```sisältäväRakennuksenOsa```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-huoneistoala" %}
Mikäli [Huoneisto](dokumentaatio/#huoneisto)-luokan objektilla on attribuutin ```huoneistoala``` arvo, sen arvon tulee olla kokonaisluku väliltä 1 - 99999 (1 <= x < 10^5), ja yksikkö neliömetri (```m2```). 
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-huoneisto-kayttoala" %}
Mikäli [Huoneisto](dokumentaatio/#huoneisto)-luokan objektilla on attribuutin ```käyttöala``` arvo, sen arvon tulee olla kokonaisluku väliltä 1 - 99999 (1 <= x < 10^5), ja yksikkö neliömetri (```m2```).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-huoneisto-huoneiden-lkm" %}
Mikäli [Huoneisto](dokumentaatio/#huoneisto)-luokan objektilla on attribuutin ```huoneidenLukumäärä``` arvo, sen arvon tulee olla kokonaisluku väliltä 1 - 99 ilman yksikkötietoa.
{% include common/clause_end.html %}

### Sisäänkäynti
{% include common/clause_start.html type="req" id="laatu/vaat-sisaankaynnin-geometria" %}
[Sisäänkäynti](dokumentaatio/#sisäänkäynti)-luokan objektilla on oltava ```geometria``` attribuutin arvo, joka kuvaa kyseisen sisäänkäynnin sijainnin pistemäisenä.
{% include common/clause_end.html %}

### Hissi
{% include common/clause_start.html type="req" id="laatu/vaat-hissin-geometria" %}
Mikäli [Hissi](dokumentaatio/#hissi)-luokan objektille annetaan ```geometria``` attribuutin arvo, sen on oltava kuvattava hissin sijainti pistemäisenä.
{% include common/clause_end.html %}

### Materiaalitiedot

{% include common/clause_start.html type="req" id="laatu/vaat-ensisijainen-kant-rak-rakennusaine" %}
[Materiaalitiedot](dokumentaatio/#materiaalitiedot)-luokan kuvaamassa rakenteisessa attribuutissa tulee olla enintään yksi sellainen attribuutin ```kantavienRakenteidenRakennusaine```-attribuutin arvo, jonka attribuutin ```ensisijainen``` arvo to ```true```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-ensisijainen-julkisivumateriaali" %}
[Materiaalitiedot](dokumentaatio/#materiaalitiedot)-luokan kuvaamassa rakenteisessa attribuutissa tulee olla enintään yksi sellainen attribuutin ```julkisivumateriaali```-attribuutin arvo, jonka attribuutin ```ensisijainen``` arvo to ```true```.
{% include common/clause_end.html %}

### RakennuksenKäyttötiedot

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-ensisijainen-kayttotarkoitus" %}
[RakennuksenKäyttötiedot](dokumentaatio/#rakennuksenkäyttötiedot)-luokan kuvaamassa rakenteisessa attribuutissa tulee olla enintään yksi sellainen attribuutin ```käyttötarkoitus```-attribuutin arvo, jonka attribuutin ```ensisijainen``` arvo to ```true```.
{% include common/clause_end.html %}

{% include common/question.html content="Tulisiko kaikilla rakennuksilla olla ensisijainen käyttötarkoitus?" %}

### Energiatiedot

{% include common/clause_start.html type="req" id="laatu/vaat-ensisijainen-lammitystapa" %}
[Energiatiedot](dokumentaatio/#energiatiedot)-luokan kuvaamassa rakenteisessa attribuutissa tulee olla enintään yksi sellainen attribuutin ```lämmitystapa```-attribuutin arvo, jonka attribuutin ```ensisijainen``` arvo to ```true```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-ensisijainen-lammitysenergian-lahde" %}
[Energiatiedot](dokumentaatio/#energiatiedot)-luokan kuvaamassa rakenteisessa attribuutissa tulee olla enintään yksi sellainen attribuutin ```lämmitysenergianLähde```-attribuutin arvo, jonka attribuutin ```ensisijainen``` arvo to ```true```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-ensisijainen-jaahdytystapa" %}
[Energiatiedot](dokumentaatio/#energiatiedot)-luokan kuvaamassa rakenteisessa attribuutissa tulee olla enintään yksi sellainen attribuutin ```jäähdytystapa```-attribuutin arvo, jonka attribuutin ```ensisijainen``` arvo to ```true```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-ensisijainen-jaahdytysenergian-lahde" %}
[Energiatiedot](dokumentaatio/#energiatiedot)-luokan kuvaamassa rakenteisessa attribuutissa tulee olla enintään yksi sellainen attribuutin ```jäähdytysenergianLähde```-attribuutin arvo, jonka attribuutin ```ensisijainen``` arvo to ```true```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-ensisijainen-sahkoenergian-lahde" %}
[Energiatiedot](dokumentaatio/#energiatiedot)-luokan kuvaamassa rakenteisessa attribuutissa tulee olla enintään yksi sellainen attribuutin ```sähköenergianLähde```-attribuutin arvo, jonka attribuutin ```ensisijainen``` arvo to ```true```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-energiamaaran-mittayksikko" %}
[Energiankulutus](dokumentaatio/#energiankulutus)-luokan objektin ```energiamääräVuodessa``` -attribuutin on oltava tyyppiä {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#numeerinenarvo" title="NumeerinenArvo" %} ja sen ```mittayksikkö``` -attribuutin arvon on oltava kilowattitunti (```kWh```) tai megajoule (```MJ```).
{% include common/clause_end.html %}

### Talotekniikkatiedot

{% include common/clause_start.html type="req" id="laatu/vaat-ensisijainen-ilmanvaihtotapa" %}
[Talotekniikkatiedot](dokumentaatio/#talotekniikkatiedot)-luokan kuvaamassa rakenteisessa attribuutissa tulee olla enintään yksi sellainen attribuutin ```ilmanvaihtotapa```-attribuutin arvo, jonka attribuutin ```ensisijainen``` arvo to ```true```.
{% include common/clause_end.html %}


### UlkokuorenTiedot

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-kerrosala" %}
Mikäli [UlkokuorenTiedot](dokumentaatio/#ulkokuorentiedot)-luokan objektilla on attribuutin ```kerrosala``` arvo, sen arvon tulee olla kokonaisluku väliltä 1 - 9999999 (1 <= x <  10^7) ja yksikkö neliömetri (```m2```).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-kerrosluku" %}
Mikäli [UlkokuorenTiedot](dokumentaatio/#ulkokuorentiedot)-luokan objektilla on attribuutin ```kerrosluku``` arvo, sen arvon tulee olla kokonaisluku väliltä 1 - 99 ilman yksikkötietoa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-tilavuus" %}
Mikäli [UlkokuorenTiedot](dokumentaatio/#ulkokuorentiedot)-luokan objektilla on attribuutin ```tilavuus``` arvo, sen arvon tulee olla kokonaisluku väliltä 1 - 9999999 (1 <= x <  10^7) ja yksikkö kuutiometri (```m3```).
{% include common/clause_end.html %}

### SisätilojenTiedot

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuksen-kellariala" %}
Mikäli [SisätilojenTiedot](dokumentaatio/#sisätilojentiedot)-luokan objektilla on attribuutin ```kellariala``` arvo, sen arvon tulee olla kokonaisluku väliltä 1 - 9999999 (1 <= x <  10^7) ja yksikkö neliömetri (```m2```).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-vaestosuojan-hlomaara" %}
Mikäli [SisätilojenTiedot](dokumentaatio/#sisätilojentiedot)-luokan objektilla on attribuutin ```väestösuojanHenkilömäärä``` arvo, sen arvon tulee olla kokonaisluku väliltä 1 - 99999 (1 <= x <  10^5).
{% include common/clause_end.html %}

### Ilmastoselvitys

Ilmastoselvitys tulee voida aina liittää rakennukseen sen pysyvän rakennustunnuksen (PRT) kautta. Rakentamisen lupapäätösten tietomallissa [Ilmastoselvitys](dokumentaatio/#ilmaistoselvitys)-luokalla on ```1..*``` assosiaatio [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokkaan, jonka konkreettisia aliluokkia ovat muun muassa [Rakennus](dokumentaatio/#rakennus) ja [RakennuksenOsa](dokumentaatio/#rakennuksenosa). 

Ilmastoselvitys liitetään tavallisesti joko suoraan koko rakennusta kuvaavaan [Rakennus](dokumentaatio/#rakennus)-luokan objektiin tai siihen [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektiin, jota luvanvaraisella toimenpiteellä muutetaan, tai joka syntyy suunnitellun laajennuksen tuloksena. Jälkimmäisessä tapauksessa yhteys pysyvään rakennustunnukseen syntyy [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan pakollisen ```rakennus:Rakennus```-assosiaation kautta.

{% include common/clause_start.html type="req" id="laatu/vaat-ilmastoselvitys-rakennuskohde-pysyva-rakennustunnus-oltava" %}
Kuhunkin [Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektiin tulee liittyä vähintään yksi (1) [RakennusTaiSenOsa](dokumentaatio/#rakennustaisenosa)-luokan aliluokkien objekti, jonka kautta ilmastoselvitys voidaan liittää rakennuksen pysyvään rakennustunnukseen. 
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-ilmastoselvitys-kaikki-ostoenergian-lahteet-annettava" %}
[Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektin tulee sisältää tiedot sen koskeman rakennuksen laskennallisesta ostoenergian kulutuksesta energialähteittäin. Ostoenergian kulutus annetaan assosiaation ```kohde``` kautta liitettyjen [RakennusTaiSenOsa](dokumentaatio/#rakennustaisenosa)-luokan objektin rakenteisen ```energiatiedot```-attribuutin osana olevan ```laskennallinenOstoenergianKulutus```-attribuutin avulla kullekin energialajille.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-ilmastoselvitys-rakennuksen-kayttajamaara" %}
[Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektin tulee sisältää tiedot rakennuksen rakennuksen suunnitellusta käyttäjämäärästä. Käyttäjämäärä annetaan assosiaation ```kohde``` kautta liitettyjen [RakennusTaiSenOsa](dokumentaatio/#rakennustaisenosa)-luokan objektin rakenteisen ```käyttötiedot```-attribuutin osana olevan ```suunniteltuKäyttäjämäärä```-attribuutin avulla. Attribuutin arvon yksikköä ei tule käyttää.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-ilmastoselvitys-rakennuksen-kayttoika" %}
[Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektin tulee sisältää tiedot rakennuksen rakennuksen tavoitteellisesta käyttöiästä. Tavoitteellinen käyttöikä annetaan assosiaation ```kohde``` kautta liitettyjen [RakennusTaiSenOsa](dokumentaatio/#rakennustaisenosa)-luokan objektin rakenteisen ```käyttötiedot```-attribuutin osana olevan ```tavoitteellinenKäyttöikä```-attribuutin avulla. Attribuutin arvon yksikön tulee olla yksi vuosi (```a```).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-ilmastoselvitys-rakennuspaikan-pinta-ala" %}
[Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektin tulee sisältää tiedot rakennuksen rakennuspaikan pinta-alasta. Rakenteisen attribuutin ```paikanVähähiilisyys``` assosiaatiolla ```paikka``` viitatuilla [Rakennuspaikka](dokumentaatio/#rakennuspaikka)-luokan objekteilla tulee olla attribuutin ```pintaAla``` arvo, jonka yksikön tulee olla neliömetri (```m2```).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-ilmastoselvitys-arviointijakso-yksikko" %}
[Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan ```käytetynArviointijaksonPituus```-attribuutin arvon yksikön tulee olla yksi vuosi (```a```).
{% include common/clause_end.html %}

#### Vähähiilisyyden arvioinnin arvot ja yksiköt

Ilmastoselvityksen vähähiilisyystiedot ilmoitetaan suunnitellun rakentamistoimenpiteen arvioitua hiilijalan- ja -kädenjälkeä kuvaavina numeroarvoina. 

{% include common/clause_start.html type="req" id="laatu/vaat-vahahiilisyystiedot-suureen-arvo" %}
Sekä [Hiilijalanjälkitiedot](dokumentaatio/#hiilijalanjälkitiedot)-luokkien että [Hiilikädenjälkitiedot](dokumentaatio/#hiilikädenjälkitiedot)-luokkien vähähiilisyyden arvioinnin tuloksia koskevat ```osatekijä```-attribuuttien arvot annetaan luokan {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %} objekteina siten, että niiden ```arvo```-attribuuttien arvot ovat luokan {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#numeerinenarvo" title="NumeerinenArvo" %} objekteja, joiden attribuutin arvo ```yksikkö``` on hiilidioksidiekvivalenttikilogramma per pinta-alan neliö per vuosi (```kgCO2e/m2/a```), ja joiden ```numero``` -attribuutin arvo ilmoitettu pyöristettynä symmetrisesti kahden desimaalin tarkkuudella.
{% include common/clause_end.html %}


#### Hiilijalanjälkitiedot

{% include common/clause_start.html type="req" id="laatu/vaat-hiilijalanjalki-rakennuksen-elinkaarienvaiheittain" %}
[Hiilijalanjälkitiedot](dokumentaatio/#hiilijalanjälkitiedot)-luokan objektien tulee sisältää arviot toimenpiteestä syntyvien hiilipäästöjen määristä seuraavien rakentamisen elinkaaren vaiheiden osalta:

* A1-3 - Rakennustuotteiden valmistus
* A4 - Kuljetukset
* A5 - Työmaatoiminnot
* B4 - Rakennustuotteiden vaihdot
* B6 - Energian käyttö
* C1 - Purkaminen
* C2 - Purkujätteen kuljetukset
* C3 - Purkujätteen käsittely
* C4 - Purkujätteen loppusijoitus

Yllä luetellut päästötiedot ilmoitetaan siten, että kukin [Hiilijalanjälkitiedot](dokumentaatio/#hiilijalanjälkitiedot)-luokan objekti sisältää tasan yhden (1) kappaleen kutakin yllä lueteltua rakennuksen elinkaaren vaiheen päästötietoa koskevaa ```osatekijä```-attribuutin arvoa. Näiden ```osatekijä```-attribuutin arvojen {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %}-luokan ```suure```-attribuutin ```tunnus```-attribuutin arvojen on oltava [IlmastoselvityksenHiilijalanjälkisuure](dokumentaatio/#ilmastoselvityksenhiilijalanjälkisuure)-koodiston koodien tunnuksia. 

[Hiilijalanjälkitiedot](dokumentaatio/#hiilijalanjälkitiedot)-luokan objektin voivat sisältää myös ```osatekijä```-attribuutin arvoja, jotka kuvaavat muita kuin [IlmastoselvityksenHiilijalanjälkisuure](dokumentaatio/#ilmastoselvityksenhiilijalanjälkisuure)-koodiston kuvaamia suureita.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-hiilijalanjalki-paastosumma-yksikko" %}
Arvioidun kokonaishiilijalanjäljen ilmoittamisessa koko seuranta-ajanjaksolla sekä rakennuksen että rakennuspaikan osalta on käytettävä mittayksikköä hiilidioksidiekvivalenttikilogramma (```kgCO2e```).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-hiilijalanjalki-per-ala-per-vuosi-yksikko" %}
Arvioidun hiilijalanjäljen ilmoittamisessa suhteessa pinta-alaan ja ajanjaksoon sekä rakennuksen lämmitetyn nettoalan että rakennuspaikan pinta-alan osalta on käytettävä mittayksikköä hiilidioksidiekvivalenttikilogramma per neliömetri per vuosi (```kgCO2e/m2/a```).
{% include common/clause_end.html %}

#### Hiilikädenjälkitiedot 

{% include common/clause_start.html type="req" id="laatu/vaat-hiilikadenjalki-osatekijoittain" %}
Sekä [Hiilikädenjälkitiedot](dokumentaatio/#hiilikädenjälkitiedot)-luokan objektien tulee sisältää arviot vältettyjen tai poistettujen kasvihuonekaasupäästöjen määristä ennen rakennuksen käyttöä, rakennuksen käytön aikaa ja käytön jälkeistä aikaa seuraavien osatekijöiden osalta:

* D1 - Uudelleenkäyttö ja kierrätys
* D2 - Hyödyntäminen energiana
* D3 - Ylimääräinen uusiutuva energia
* D4 - Tuotteiden hiilivarastovaikutus
* D5 - Karbonatisoituminen
* D6 - Istutettu puusto

Hiilikädenjäljen arvioinnin on sisällettävä ainoastaan sellaiset vältetyt ja poistetut kasvihuonekaasupäästöt, joita ei aiheutuisi ilman rakennushanketta.

Osatekijä "D6 - Istutettu puusto" tulee sisällyttää ainoastaan sellaisiin ilmastoselvityksiin, jotka koskevat asemakaava-alueella tapahtumaa rakentamista.

Yllä luetellut osatekijöiden tiedot ilmoitetaan siten, että kukin [Hiilikädenjälkitiedot](dokumentaatio/#hiilikädenjälkitiedot)-luokan objekti sisältää tasan yhden (1) kappaleen kutakin yllä lueteltua osatekijää koskevaa ```osatekijä```-attribuutin arvoa. Näiden ```osatekijä```-attribuutin arvojen {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %}-luokan ```suure```-attribuutin ```tunnus```-attribuutin arvojen on oltava [IlmastoselvityksenHiilikädenjälkisuure](dokumentaatio/#ilmastoselvityksenhiilikädenjälkisuure)-koodiston koodien tunnuksia. 

[Hiilikädenjälkitiedot](dokumentaatio/#hiilikädenjälkitiedot)-luokan objektin voivat sisältää myös ```osatekijä```-attribuutin arvoja, jotka kuvaavat muita kuin [IlmastoselvityksenHiilikädenjälkisuure](dokumentaatio/#ilmastoselvityksenhiilikädenjälkisuure)-koodiston kuvaamia suureita.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-hiilikadenjalki-per-ala-per-vuosi-yksikko" %}
Arvioidun hiilikädenjäljen ilmoittamisessa suhteessa pinta-alaan ja ajanjaksoon sekä rakennuksen lämmitetyn nettoalan että rakennuspaikan pinta-alan osalta on käytettävä mittayksikköä hiilidioksidiekvivalenttikilogramma per neliömetri per vuosi (```kgCO2e/m2/a```).
{% include common/clause_end.html %}

#### Rakennuskohdekohtaiset vähähiilisyystiedot

{% include common/clause_start.html type="req" id="laatu/vaat-vahahiilisyystiedot-rakennuksen-osittain" %}
Mikäli ilmastoselvitys liittyy rakentamistoimenpiteeseen, joka koskee vain tiettyjä osia koko rakennuksesta, tulee [Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektiin liittää yksi rakenteisen attribuutin ```kohteenVähähiilisyys``` arvo kutakin [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektia ja kunkin niistä sisältämää eri käyttötarkoitukseen varattua tilaa kohti. 
{% include common/clause_end.html %}

Ilmastoselvityksessä voidaan viitata vain sellaisiin rakennuksen osiin, jotka ovat osa rakennuksen rakentamishistoriaan perustuvaa rakennuksen osittelua. 

{% include common/clause_start.html type="req" id="laatu/vaat-vahahiilisyystiedot-rakennuksen-osittelun-peruste" %}
[RakennuskohdekohtaisetVähähiilisyystiedot](dokumentaatio/#rakennuskohdekohtaisetvähähiilisyystiedot)-luokan objektin assosiaation ```kohde``` avulla voidaan viitata vain sellaisiin [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objekteihin, joihin viitataan toimenpiteen kohteena olevan [Rakennus](dokumentaatio/#rakennus)-luokan objektin sellaisesta ```osittelu```-attribuutin arvosta, jonka ```ositteluperuste```-attribuutin arvo on ```2 - Rakentamishistoriaan perustuva osittelu```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuskohteenvahahiilisyystiedot-lammitetty-nettoala" %}
Rakennuksen lämmitetyllä nettoalalla tarkoitetaan lämmitettyjen kerrostasoalojen summaa kerrostasoja ympäröivien ulkoseinien sisäpintojen mukaan laskettuna. Rakennuksen toimenpidealueen lämmitetty nettoalalla kunkin [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan objektin tiettyyn käyttötarkoitukseen varatun osan osalta ilmoitetaan [RakennuskohdekohtaisetVähähiilisyystiedot](dokumentaatio/#rakennuskohdekohtaisetvähäliilisyystiedot)-luokan objektien ```lämmitettyNettoala```-attribuuttien avulla, yksikkönä neliömetri (```m2```).  
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuskohteen-hiilijalanjalki-per-pinta-ala-per-vuosi" %}
[RakennuskohdekohtaisetVähähiilisyystiedot](dokumentaatio/#rakennuskohdekohtaisetvähäliilisyystiedot)-luokan objektien rakenteisen ```hiilijalanjälki```-attribuutin sisältämien ```osatekijä```-attribuuttien numeeriset arvot annetaan hiilidioksidiekvivalenttikilogrammoina per rakennuskohteen annettuun käyttötarkoitukseen tarkoitetun osan lämmitetty nettoala per vuosi.
{% include common/clause_end.html %}


{% include common/clause_start.html type="req" id="laatu/vaat-rakennuskohteen-hiilikadenjalki-per-pinta-ala-per-vuosi" %}
[RakennuskohdekohtaisetVähähiilisyystiedot](dokumentaatio/#rakennuskohdekohtaisetvähäliilisyystiedot)-luokan objektien rakenteisen ```hiilikädenjälki```-attribuutin sisältämien ```osatekijä```-attribuuttien numeeriset arvot annetaan hiilidioksidiekvivalenttikilogrammoina per rakennuskohteen annettuun käyttötarkoitukseen tarkoitetun osan lämmitetty nettoala per vuosi.
{% include common/clause_end.html %}

##### Hiilijalanjäljen summat koko toimenpidealan osalta

Useita eri käyttötarkoituksia sisältävän rakennuksen toimenpidealueen hiilijalanjälkitiedot ilmoitetaan erikseen kuhunkin käyttötarkoitukseen tarkoitetun, toimenpidealueeseen kuuluvan lämmitetyn nettopinta-alan osalta. Koko toimenpidealueen kaikkien käyttötarkoituskohtaisten lämmitettyjen nettopinta-alojen hiilijalanjäljen osuuksien summaa (```kgCO2e/m2/a```) ei ilmoiteta erikseen, vaan se lasketaan ilmoitettujen käyttötarkoituskohtaisten hiilijalanjälkiarvioiden summana.

{% include common/clause_start.html type="req" id="laatu/vaat-hiilijalanjalki-summa-rakennukselle-per-ala-per-vuosi" %}
Rakentamistoimenpiteestä aiheutuva arvioitu hiilijalanjälki rakennuksen osalta toimenpidealueen lämmitettyä nettoneliömetriä kohti vuodessa lasketaan seuraavasti:

Lasketaan ensin kunkin [Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektiin sisältyvän ```kohteenVähähiilisyys```-attribuutin osalta sellaisten sen ```hiilijalanjälki```-attribuutin  sisältämien ```osatekijä```-attribuuttien arvojen ```arvo```-attribuuttien ```numero```-attribuuttien lukujen summa, joiden ```suure```-attribuutin ```tunnus```-attribuutin arvo on jokin [IlmastoselvityksenHiilijalanjälkisuure](dokumentaatio/#ilmastoselvityksenhiilijalanjälkisuure)-koodiston koodeista. Lopuksi lasketaan rakennuskohde- ja käyttötarkoituskohtaiset summat yhteen.
{% include common/clause_end.html %}

Seuraava pseudokoodiesitys kuvaa yllä kuvatun vaatimuksen laskenta-algoritmia:
```
let tulos = 0;
for each ilmastoselvitys.kohteenVähähiilisyys as kv {
  for each kv.hiilijalanjälki.osatekija as ot {
    if IlmastoselvityksenHiilijalanjälkisuure.contains(ot.suure.tunnus.koodi) {
      tulos = tulos + ot.arvo.numero;
    }
  }
}
```

Vastaavasti koko toimenpidealueen kaikkien käyttötarkoitusalueiden kokonaishiilijalanjäljen summaa (```kgCOe```) ei ilmoiteta erikseen, vaan se lasketaan ilmoitettujen käyttötarkoituskohtaisten hiilijalanjälkiarvioiden summana kerrottuna kunkin käyttötarkoituksen lämmitetyn nettoalan määrällä ja käytetyn arviontijakson pituudella. 

{% include common/clause_start.html type="req" id="laatu/vaat-hiilijalanjalki-summa-rakennukselle-arviointijaksolla" %}
Rakentamistoimenpiteestä aiheutuva arvioitu kokonaishiilijalanjälki rakennuksen toimenpidealueen osalta koko arviointijakson aikana lasketaan seuraavasti:

Lasketaan ensin kunkin [Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektiin sisältyvän ```kohteenVähähiilisyys```-attribuutin osalta sellaisten sen ```hiilijalanjälki```-attribuutin  sisältämien ```osatekijä```-attribuuttien arvojen ```arvo```-attribuuttien ```numero```-attribuuttien lukujen summa, joiden ```suure```-attribuutin ```tunnus```-attribuutin arvo on jokin [IlmastoselvityksenHiilijalanjälkisuure](dokumentaatio/#ilmastoselvityksenhiilijalanjälkisuure)-koodiston koodeista. Nämä summat kerrotaan sekä kyseisen [RakennuskohdekohtaisetVähähiilisyystiedot](dokumentaatio/#rakennuskohdekohtaisetvähähiilisyystiedot)-luokan objektin ```lämmitettyNettoala```-attribuutin ```value```-attribuutin arvolla että [Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektin ```käytetynArviointijaksonPituus```-attribuutin ```value```-attribuutin arvolla. Lopuksi lasketaan rakennuskohde- ja käyttötarkoituskohtaiset summat yhteen.
{% include common/clause_end.html %}

Seuraava pseudokoodiesitys kuvaa yllä kuvatun vaatimuksen laskenta-algoritmia:
```
let tulos = 0;
for each ilmastoselvitys.kohteenVähähiilisyys as kv {
  for each kv.hiilijalanjälki.osatekija as ot {
    if IlmastoselvityksenHiilijalanjälkisuure.contains(ot.suure.tunnus.koodi) {
      tulos = tulos + ot.arvo.numero * kv.lämmitettyNettoala.value * ilmastoselvitys.käytetynArviointijaksonPituus.value;
    }
  }
}
```

##### Hiilijalanjäljen summat käyttötarkoituksittain

Rakennuksen toimenpidealueen tiettyyn käyttötarkoitukseen tarkoitettua osaa koskevaa kaikkien sen rakentamisen elinkaaren vaiheiden hiilijalanjäljen summaa (```kgCO2e/m2/a```) ei ilmoiteta erikseen, vaan se lasketaan elinkaarenvaihekohtaisesti ilmoitettujen hiilijalanjälkitietojen summana. 

{% include common/clause_start.html type="req" id="laatu/vaat-hiilijalanjalki-summa-rakennuksen-kayttotarkoitukselle-per-ala-per-vuosi" %}
Rakentamistoimenpiteestä aiheutuva arvioitu hiilijalanjälki rakennuksen toimenpidealueen tiettyyn käyttötarkoitukseen tarkoitetun lämmitetyn nettoalan osalta neliömetriä kohti vuodessa lasketaan seuraavasti:

Lasketaan ensin kunkin [Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektiin sisältyvän, valittua käyttötarkoitusta koskevan ```kohteenVähähiilisyys```-attribuutin osalta sellaisten sen ```hiilijalanjälki```-attribuutin  sisältämien ```osatekijä```-attribuuttien arvojen ```arvo```-attribuuttien ```numero```-attribuuttien lukujen summa, joiden ```suure```-attribuutin ```tunnus```-attribuutin arvo on jokin [IlmastoselvityksenHiilijalanjälkisuure](dokumentaatio/#ilmastoselvityksenhiilijalanjälkisuure)-koodiston koodeista. Lopuksi lasketaan rakennuskohde- ja käyttötarkoituskohtaiset summat yhteen.
{% include common/clause_end.html %}

Seuraava pseudokoodiesitys kuvaa yllä kuvatun vaatimuksen laskenta-algoritmia (esimerkin käyttötapausluokka '2 - Asuinkerrostalo'):
```
let tulos = 0;
let kt = '2 - Asuinkerrostalo';
for each ilmastoselvitys.kohteenVähähiilisyys as kv {
  if (kv.käyttötarkoitusluokka == kt) {
    for each kv.hiilijalanjälki.osatekija as ot {
      if IlmastoselvityksenHiilijalanjälkisuure.contains(ot.suure.tunnus.koodi) {
        tulos = tulos + ot.arvo.numero;
      }
    }
  }
}
```

Vastaavasti rakennuksen toimenpidealueen tiettyyn käyttötarkoitukseen tarkoitettua osaa koskevaa kokonaishiilijalanjälkeä (```kgCO2e```) ei ilmoiteta erikseen, vaan se lasketaan sen ko. käyttötarkoitusta koskevan rakennuksen osan elinkaarivaihekohtaisten arvojen summana kerrottuna ko. käyttötarkoituksen lämmitetyn nettoalan määrällä ja käytetyn arviontijakson pituudella.

{% include common/clause_start.html type="req" id="laatu/vaat-hiilijalanjalki-summa-rakennuksen-kayttotarkoitukselle-arviointijaksolla" %}
Rakentamistoimenpiteestä aiheutuva arvioitu kokonaishiilijalanjälki rakennuksen tiettyyn käyttötarkoitukseen tarkoitetun toimenpidealueen osalta koko arviointijakson aikana lasketaan seuraavasti:

Lasketaan ensin kunkin [Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektiin sisältyvän, valittua käyttötarkoitusta koskevan ```kohteenVähähiilisyys```-attribuutin osalta sellaisten sen ```hiilijalanjälki```-attribuutin  sisältämien ```osatekijä```-attribuuttien arvojen ```arvo```-attribuuttien ```numero```-attribuuttien lukujen summa, joiden ```suure```-attribuutin ```tunnus```-attribuutin arvo on jokin [IlmastoselvityksenHiilijalanjälkisuure](dokumentaatio/#ilmastoselvityksenhiilijalanjälkisuure)-koodiston koodeista. Nämä summat kerrotaan sekä kyseisen [RakennuskohdekohtaisetVähähiilisyystiedot](dokumentaatio/#rakennuskohdekohtaisetvähähiilisyystiedot)-luokan objektin ```lämmitettyNettoala```-attribuutin ```value```-attribuutin arvolla että [Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektin ```käytetynArviointijaksonPituus```-attribuutin ```value```-attribuutin arvolla. Lopuksi lasketaan rakennuskohde- ja käyttötarkoituskohtaiset summat yhteen.
{% include common/clause_end.html %}

Seuraava pseudokoodiesitys kuvaa yllä kuvatun vaatimuksen laskenta-algoritmia (esimerkin käyttötapausluokka '2 - Asuinkerrostalo'):
```
let tulos = 0;
let kt = '2 - Asuinkerrostalo';
for each ilmastoselvitys.kohteenVähähiilisyys as kv {
  if (kv.käyttötarkoitusluokka == kt) {
    for each kv.hiilijalanjälki.osatekija as ot {
      if IlmastoselvityksenHiilijalanjälkisuure.contains(ot.suure.tunnus.koodi) {
        tulos = tulos + ot.arvo.numero * kv.lämmitettyNettoala.value * ilmastoselvitys.käytetynArviointijaksonPituus.value;
      }
    }
  }
}
```

#### Rakennuspaikkakohtaiset vähähiilisyystiedot

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuspaikan-hiilijalanjalki-per-pinta-ala-per-vuosi" %}
[RakennuspaikkakohtaisetVähähiilisyystiedot](dokumentaatio/#rakennuspaikkakohtaisetvähäliilisyystiedot)-luokan objektien rakenteisen ```hiilijalanjälki```-attribuutin sisältämien ```osatekijä```-attribuuttien numeeriset arvot annetaan hiilidioksidiekvivalenttikilogrammoina per rakennuspaikan pinta-ala per vuosi.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuspaikan-hiilikadenjalki-per-pinta-ala-per-vuosi" %}
[RakennuspaikkakohtaisetVähähiilisyystiedot](dokumentaatio/#rakennuspaikkakohtaisetvähäliilisyystiedot)-luokan objektien rakenteisen ```hiilikädenjälki```-attribuutin sisältämien ```osatekijä```-attribuuttien numeeriset arvot annetaan hiilidioksidiekvivalenttikilogrammoina per rakennuspaikan pinta-ala per vuosi.
{% include common/clause_end.html %}

##### Hiilijalanjäljen summat rakennuspaikan osalta

Samoin kuin rakennuksen osalta, rakennuspaikan ominaisuuksista johtuvan arvioidun rakentamisen hiilijalanjäljen yhteismäärää rakennuspaikan pinta-alan suhteen (```kgCO2e/m2/a```) ei ilmoiteta erikseen, vaan se lasketaan rakennuspaikan osalta eri rakentamisen elinkaarivaiheille ilmoitettujen arvojen summana. 

{% include common/clause_start.html type="req" id="laatu/vaat-hiilijalanjalki-summa-rakennuspaikalle-per-ala-per-vuosi" %}
Rakentamistoimenpiteestä aiheutuva arvioitu hiilijalanjälki rakennuspaikan osalta sen pinta-alan neliömetriä kohti vuodessa lasketaan seuraavasti:

Lasketaan [Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektiin sisältyvän ```paikanVähähiilisyys```-attribuutin sellaisten sen ```hiilijalanjälki```-attribuutin sisältämien ```osatekijä```-attribuuttien arvojen ```arvo```-attribuuttien ```numero```-attribuuttien lukujen summa, joiden ```suure```-attribuutin ```tunnus```-attribuutin arvo on jokin [IlmastoselvityksenHiilijalanjälkisuure](dokumentaatio/#ilmastoselvityksenhiilijalanjälkisuure)-koodiston koodeista.
{% include common/clause_end.html %}

Seuraava pseudokoodiesitys kuvaa yllä kuvatun vaatimuksen laskenta-algoritmia:
```
let tulos = 0;
for each ilmastoselvitys.paikanVähähiilisyys.hiilijalanjälki.osatekija as ot {
  if IlmastoselvityksenHiilijalanjälkisuure.contains(ot.suure.tunnus.koodi) {
    tulos = tulos + ot.arvo.numero;
  }
}
```

Vastaavasti rakennuspaikan ominaisuuksista johtuvan kokonaishiilijalanjäljen arviota (```kgCO2e```) ei ilmoiteta erikseen, vaan se lasketaan ilmoitetuista rakentamisen elikaaren vaiheiden summana kerrotuna arviointijakson pituudella ja rakennuspaikan pinta-alan määrällä. 

{% include common/clause_start.html type="req" id="laatu/vaat-hiilijalanjalki-summa-rakennuspaikalle-arviointijaksolla" %}
Rakentamistoimenpiteestä aiheutuva arvioitu kokonaishiilijalanjälki rakennuspaikan osalta koko arviointijakson aikana lasketaan seuraavasti:

Lasketaan [Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektiin sisältyvän ```paikanVähähiilisyys```-attribuutin sellaisten sen ```hiilijalanjälki```-attribuutin sisältämien ```osatekijä```-attribuuttien arvojen ```arvo```-attribuuttien ```numero```-attribuuttien lukujen summa, joiden ```suure```-attribuutin ```tunnus```-attribuutin arvo on jokin [IlmastoselvityksenHiilijalanjälkisuure](dokumentaatio/#ilmastoselvityksenhiilijalanjälkisuure)-koodiston koodeista. Saatu summa kerrotaan sekä [Ilmastoselvitys](dokumentaatio/#ilmastoselvitys)-luokan objektin ```käytetynArviointijaksonPituus```-attribuutin ```value```-attribuutin arvolla että kyseisen [RakennuspaikkakohtaisetVähähiilisyystiedot](dokumentaatio/#rakennuspaikkakohtaisetvähähiilisyystiedot)-luokan objektin ```paikka```-assosiaatiolla viitatun [Rakennuspaikka](dokumentaatio/#rakennuspaikka)-luokan objektin ```pintaAla```-attribuutin ```value```-attribuutin arvolla.
{% include common/clause_end.html %}

Seuraava pseudokoodiesitys kuvaa yllä kuvatun vaatimuksen laskenta-algoritmia:
```
let tulos = 0;
for each ilmastoselvitys.paikanVähähiilisyys.hiilijalanjälki.osatekija as ot {
  if IlmastoselvityksenHiilijalanjälkisuure.contains(ot.suure.tunnus.koodi) {
    tulos = tulos + ot.arvo.numero * ilmastoselvitys.käytetynArviointijaksonPituus.value * ilmastoselvitys.paikanVähähiilisyys.paikka.pintaAla.value;
  }
}
```


### Materiaaliseloste

Materialiseloste tulee voida aina liittää rakennukseen sen pysyvän rakennustunnuksen (PRT) kautta. Rakentamisen lupapäätösten tietomallissa [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokalla on ```1..*``` assosiaatio [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokkaan, jonka konkreettisia aliluokkia ovat muun muassa [Rakennus](dokumentaatio/#rakennus) ja [RakennuksenOsa](dokumentaatio/#rakennuksenosa).

Materiaaliseloste liitetään tavallisesti joko suoraan koko rakennusta kuvaavaan [Rakennus](dokumentaatio/#rakennus)-luokan objektiin tai siihen [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektiin, jota luvanvaraisella toimenpiteellä muutetaan, tai joka syntyy suunnitellun laajennuksen tuloksena. Jälkimmäisessä tapauksessa yhteys pysyvään rakennustunnukseen syntyy [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan pakollisen ```rakennus:Rakennus```-assosiaation kautta.

{% include common/clause_start.html type="req" id="laatu/vaat-materialiseloste-rakennuskohde-pysyva-rakennustunnus-oltava" %}
Kuhunkin [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektiin tulee liittyä vähintään yksi (1) [RakennusTaiSenOsa](dokumentaatio/#rakennustaisenosa)-luokan aliluokkien objekti, jonka kautta materiaaliseloste voidaan liittää rakennuksen pysyvään rakennustunnukseen. 
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-materiaaliseloste-rakennuksen-kayttoika" %}
[Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin tulee sisältää tiedot rakennuksen rakennuksen tavoitteellisesta käyttöiästä. Tavoitteellinen käyttöikä annetaan assosiaation ```kohde``` kautta liitettyjen [RakennusTaiSenOsa](dokumentaatio/#rakennustaisenosa)-luokan objektin rakenteisen ```käyttötiedot```-attribuutin osana olevan ```tavoitteellinenKäyttöikä```-attribuutin avulla. Attribuutin arvon yksikön tulee olla yksi vuosi (```a```).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-materiaaliseloste-rakennuspaikan-pinta-ala" %}
[Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin tulee sisältää tiedot rakennuksen rakennuspaikan pinta-alasta.  Rakenteisen attribuutin ```rakennuspaikanMateriaalit``` assosiaatiolla ```paikka``` viitatuilla [Rakennuspaikka](dokumentaatio/#rakennuspaikka)-luokan objekteilla tulee olla attribuutin ```pintaAla``` arvo, jonka yksikön tulee olla neliömetri (```m2```).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-materiaaliselostus-lammitetty-nettoala" %}
Rakennuksen lämmitetyllä nettoalalla tarkoitetaan lämmitettyjen kerrostasoalojen summaa kerrostasoja ympäröivien ulkoseinien sisäpintojen mukaan laskettuna. Rakennuksen toimenpidealueen lämmitetty nettoala ilmoitetaan [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```toimenpidealueenLämmitettyNettoala```-attribuutin avulla, yksikkönä neliömetri (```m2```).
{% include common/clause_end.html %}

#### Materiaalimäärät lajeittain

{% include common/clause_start.html type="req" id="laatu/vaat-materiaalilajin-maara" %}
[Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin tulee sisältää tiedot rakennustoimenpiteen yhteydessä käytettävien materiaalien määristä painon mukaan niiden tyypillisessä käyttökosteudessa kuvaavina kokonaislukuarvoina seuraavien materiaalilajien osalta:

* Betoni-, tiili-, kivennäislaatta-, keramiikka- ja luonnonkivimateriaalit
* Puu- ja luonnonkuitupohjaiset materiaalit rakennustuotteissa
* Lasimateriaalit
* Muovit ja kumit
* Bitumimateriaalit ja -seokset
* Metallit
* Lämmöneristemateriaalit
* Kipsit
* Koneet ja laitteet
* Muut materiaalit
* Maa- ja kiviainekset ja
* Istutetut puut

Materiaalilaji ```Istutetut puut``` tulee sisällyttää ainoastaan sellaisiin materiaaliselosteisiin, jotka koskevat asemakaava-alueella tapahtumaa rakentamista.

Yllä luetellut materiaalilajien tiedot ilmoitetaan siten, että kukin [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objekti sisältää tasan yhden (1) kappaleen kutakin yllä lueteltua materiaalilajia koskevaa ```materiaalilajinMäärä```-attribuutin arvoa. Näiden ```materiaalilajinMäärä```-attribuutin arvojen {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %}-luokan ```suure```-attribuutin ```tunnus```-attribuutin arvojen on oltava [RakentamisessaKäytettävänMateriaalilajinMäärä](dokumentaatio/#rakentamisessakäytettävänmateriaalilajinmäärä)-koodiston koodien tunnuksia, ja 
 niiden ```arvo```-attribuuttien arvot ovat luokan {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#numeerinenarvo" title="NumeerinenArvo" %} objekteja, joiden attribuutin arvo ```yksikkö``` on kilogramma (```kg```), ja joiden ```numero``` -attribuutin arvo on ilmoitettu pyöristettynä kokonaiseen lukuun ilman desimaaleja.

[Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin voivat sisältää myös ```materiaalilajinMäärä```-attribuutin arvoja, jotka kuvaavat muita kuin [RakentamisessaKäytettävänMateriaalilajinMäärä](dokumentaatio/#rakentamisessakäytettävänmateriaalilajinmäärä)-koodiston kuvaamia suureita.
{% include common/clause_end.html %}

Kunkin ilmoitettavan materiaalilajin osalta materiaaliselosteesta tulee ilmetä materiaalimäärä myös suhteessa rakennuksen toimenpidealueen lämmitettyyn nettoalaan. Tätä suhteellista määrää ei ilmoiteta erikseen, vaan se voidaan laskea jakamalla annettu materiaalimäärä kilogrammoissa toimenpidealueen lämmitetyn nettoalan arvolla neliöissä. 

{% include common/clause_start.html type="req" id="laatu/vaat-materiaalilajin-maara-per-nelio" %}
Kunkin materiaalilajin määrä suhteessa rakennuksen toimenpidealueen lämmittyyn nettoalaan saadaan jakamalla  [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin kunkin ```materiaalilajinMäärä```-attribuutin arvon {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %}-luokan ```arvo```-attribuutin ```numero``` -attribuutin arvo [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```toimenpidealueenLämmitettyNettoala```-attribuutin arvolla.
{% include common/clause_end.html %}

#### Materiaalien alkuperä

##### Vaarallisten aineiden määrä

{% include common/clause_start.html type="req" id="laatu/vaat-materiaaliselostus-vaaralliset-aineiden-maara" %}
Materiaaliselosteessa ilmoitettava vaarallisten aineiden kokonaismäärä ilmoitetaan [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektien ```vaarallistenAineidenMäärä```-attribuutin avulla, yksikkönä neliömetri (```kg```), ja joiden ```numero``` -attribuutin arvo on ilmoitettu pyöristettynä kokonaiseen lukuun ilman desimaaleja.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-materiaaliselostus-vaaralliset-aineiden-maara-per-nelio" %}
Vaarallisten aineiden määrä suhteessa rakennuksen toimenpidealueen lämmittyyn nettoalaan saadaan jakamalla  [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin kunkin ```vaarallistenAineidenMäärä```-attribuutin arvon {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %}-luokan ```arvo```-attribuutin ```numero``` -attribuutin arvo [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```toimenpidealueenLämmitettyNettoala```-attribuutin arvolla.
{% include common/clause_end.html %}

##### Uusiutuvan materiaalin määrä

{% include common/clause_start.html type="req" id="laatu/vaat-materiaaliselostus-uusiutuvan-materiaalin-maara" %}
Materiaaliselosteessa ilmoitettava uusiutuvan materiaalin kokonaismäärä ilmoitetaan [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektien ```uusiutuvanMateriaalinMäärä```-attribuutin avulla, yksikkönä neliömetri (```kg```), ja joiden ```numero``` -attribuutin arvo on ilmoitettu pyöristettynä kokonaiseen lukuun ilman desimaaleja.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-materiaaliselostus-uusiutuvan-materiaalin-maara-per-nelio" %}
Uusiutuvan materiaalien määrä suhteessa rakennuksen toimenpidealueen lämmittyyn nettoalaan saadaan jakamalla  [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin kunkin ```uusiutuvanMateriaalinMäärä```-attribuutin arvon {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %}-luokan ```arvo```-attribuutin ```numero``` -attribuutin arvo [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```toimenpidealueenLämmitettyNettoala```-attribuutin arvolla.
{% include common/clause_end.html %}

##### Uusiutumattoman materiaalin määrä

{% include common/clause_start.html type="req" id="laatu/vaat-materiaaliselostus-uusiutumattoman-materiaalin-maara" %}
Materiaaliselosteessa ilmoitettava uusiutumattoman materiaalin kokonaismäärä ilmoitetaan [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektien ```uusiutumattomanMateriaalinMäärä```-attribuutin avulla, yksikkönä neliömetri (```kg```), ja joiden ```numero``` -attribuutin arvo on ilmoitettu pyöristettynä kokonaiseen lukuun ilman desimaaleja.
{% include common/clause_end.html %}


{% include common/clause_start.html type="req" id="laatu/vaat-materiaaliselostus-uusiutumattoman-materiaalin-maara-per-nelio" %}
Uusiutumattoman materiaalien määrä suhteessa rakennuksen toimenpidealueen lämmittyyn nettoalaan saadaan jakamalla  [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin kunkin ```uusiutumattomanMateriaalinMäärä```-attribuutin arvon {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %}-luokan ```arvo```-attribuutin ```numero``` -attribuutin arvo [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```toimenpidealueenLämmitettyNettoala```-attribuutin arvolla.
{% include common/clause_end.html %}

##### Kierrätetyn materiaalin määrä

{% include common/clause_start.html type="req" id="laatu/vaat-materiaaliselostus-kierratetyn-materiaalin-maara" %}
Materiaaliselosteessa ilmoitettava kierrätetyn materiaalin kokonaismäärä ilmoitetaan [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektien ```kierrätetynMateriaalinMäärä```-attribuutin avulla, yksikkönä neliömetri (```kg```), ja joiden ```numero``` -attribuutin arvo on ilmoitettu pyöristettynä kokonaiseen lukuun ilman desimaaleja.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-materiaaliselostus-kierratetyn-materiaalin-maara-per-nelio" %}
Kierrätetyn materiaalien määrä suhteessa rakennuksen toimenpidealueen lämmittyyn nettoalaan saadaan jakamalla  [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin kunkin ```kierrätetynMateriaalinMäärä```-attribuutin arvon {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %}-luokan ```arvo```-attribuutin ```numero``` -attribuutin arvo [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```toimenpidealueenLämmitettyNettoala```-attribuutin arvolla.
{% include common/clause_end.html %}

##### Uudelleenkäytetyn materiaalin määrä

{% include common/clause_start.html type="req" id="laatu/vaat-materiaaliselostus-uudelleenkaytetyn-materiaalin-maara" %}
Materiaaliselosteessa ilmoitettava uudelleenkäytetyn materiaalin kokonaismäärä ilmoitetaan [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektien ```uudelleenkäytetynMateriaalinMäärä```-attribuutin avulla, yksikkönä neliömetri (```kg```), ja joiden ```numero``` -attribuutin arvo on ilmoitettu pyöristettynä kokonaiseen lukuun ilman desimaaleja.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-materiaaliselostus-uudelleenkaytetyn-materiaalin-maara-per-nelio" %}
Uudelleenkäytetyn materiaalien määrä suhteessa rakennuksen toimenpidealueen lämmittyyn nettoalaan saadaan jakamalla  [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin kunkin ```uudelleenkäytetynMateriaalinMäärä```-attribuutin arvon {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %}-luokan ```arvo```-attribuutin ```numero``` -attribuutin arvo [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```toimenpidealueenLämmitettyNettoala```-attribuutin arvolla.
{% include common/clause_end.html %}

### Rakennuspaikkakohteiset materiaalimäärät rakennusosittain

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuspaikan-materiaalimaarat-rakennusosittain" %}
Materiaaliselosteen on sisällettävä tiedot rakentamistoimenpiteessä käytettävien materiaalien määristä siltä osin, kuin ne kohdistuvat rakennuspaikkaan. Materiaalimäärät on ilmoitettava seuraavien rakennusosaluokkien osalta (suluissa koodiston [Rakennuksen rakennusosan materiaalin määrä](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara) käytettävä koodi):

**Alueosat**:

* Maaosat (koodi [1001](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/1001))
* Tuennat (koodi [1002](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/1002))
* Päällysteet (koodi [1003](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/1003))
* Alueen rakenteet (koodi [1004](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/1004))

**Rakennusosat**:

* Perustukset (koodi [2001](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2001))

**Talotekniikka**:

* Lämmitysjärjestelmän pääosat (koodi [4001](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4001))
* Vesi- ja viemärijärjestelmän pääosat (koodi [4002](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4002))
* Jäähdytysjärjestelmän pääosat (koodi [4004](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4004))
* Sähköjärjestelmän pääosat (koodi [4006](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4006))

Yllä luetellut rakennusosakohtaisten materiaalimäärien tiedot ilmoitetaan siten, että [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```rakennuspaikanMateriaalit```-attribuutin arvon [RakennuspaikkakohteisetMateriaalimäärät](dokumentaatio/#rakennuspaikkakohtaisetmateriaalimäärät)-luokan mukainen objekti sisältää tasan yhden (1) kappaleen kutakin yllä lueteltua rakennusosaa koskevaa ```rakennusosanOsuus```-attribuutin arvoa. Näiden ```rakennusosanOsuus```-attribuutin arvojen {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %}-luokan ```suure```-attribuutin ```tunnus```-attribuutin arvojen on oltava [Rakennuksen rakennusosan materiaalin määrä](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara)-koodiston koodien tunnuksia.

[RakennuspaikkakohteisetMateriaalimäärät](dokumentaatio/#rakennuspaikkakohtaisetmateriaalimäärät)-luokan objektin voivat sisältää myös ```rakennusosanOsuus```-attribuutin arvoja, jotka kuvaavat muita kuin yllä lueteltuja suureita.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuspaikan-osien-materiaalimaarat-suureen-arvo" %}
[RakennuspaikkakohteisetMateriaalimäärät](dokumentaatio/#rakennuspaikkakohtaisetmateriaalimäärät)-luokkien objektien ```rakennusosanOsuus```-attribuuttien arvot annetaan luokan {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %} objekteina siten, että niiden ```arvo```-attribuuttien arvot ovat luokan {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#numeerinenarvo" title="NumeerinenArvo" %} objekteja, joiden attribuutin arvo ```yksikkö``` on kilogramma (```kg```), ja joiden ```numero``` -attribuutin arvo on ilmoitettu pyöristettynä kokonaiseen lukuun ilman desimaaleja.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuspaikan-osien-materiaalimaarat-per-nelio" %}
Kunkin rakennusosakohtaisen materiaalin määrä suhteessa rakennuspaikan pinta-alaan saadaan jakamalla [RakennuspaikkakohteisetMateriaalimäärät](dokumentaatio/#rakennuspaikkakohtaisetmateriaalimäärät)-luokan objektin kyseistä rakennusosaa koskevan ```rakennusosanOsuus```-attribuutin sisältämän ```arvo```-attribuutin ```numero``` -attribuutin arvo [RakennuspaikkakohteisetMateriaalimäärät](dokumentaatio/#rakennuspaikkakohtaisetmateriaalimäärät)-luokan objektin assosiaatiolla ```paikka``` viitatun [Rakennuspaikka](dokumentaatio/#rakennuspaikka)-luokan objektin ```pintaAla```-attribuutin arvolla.
{% include common/clause_end.html %}


#### Materiaalimäärien summat rakennuspaikan osalta

Rakennuspaikkaan kohdistuvat materiaalimäärät ilmoitetaan materiaalilajeittain kuten yllä on kuvattu. Kaikkien ilmoitettavien materiaalilajien määrien summaa ei ilmoiteta erikseen, vaan se lasketaan ilmoitettujen materiaalilajikohtaisten määrien summana. Tulee huomata, että tämä summa ei välttämättä vastaa kaikkien rakennuspaikan rakentamiseen käytetyn materiaalin kokonaismäärää, sillä kaikkia käytettäviä materiaalilajeja ei tarvitse ilmoittaa.

{% include common/clause_start.html type="req" id="laatu/vaat-materiaalilajien-maarien-summa-rakennuspaikalle" %}
Rakennuspaikkaan kohdistuvien, materiaaliselosteessa ilmoitetavien materiaalilajien yhteismäärä saadaan laskemalla yhteen kaikkien [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```rakennuspaikanMateriaalit```-attribuutin arvon [RakennuspaikkakohteisetMateriaalimäärät](dokumentaatio/#rakennuspaikkakohtaisetmateriaalimäärät)-luokan mukaisen objektin sellaiset ```rakennusosanOsuus```-attribuutin ilmoittamat materiaalimäärät, joiden ilmoittaminen vaaditaan materiaaliselostuksessa kohdistettuna rakennuspaikalle.
{% include common/clause_end.html %}

Seuraava pseudokoodiesitys kuvaa yllä kuvatun vaatimuksen laskenta-algoritmia:
```
let tulos = 0;
let RP_OSAT = { 
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/1001",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/1002",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/1003",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/1004",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2001",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4001",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4002",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4004",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4006"
};
for each materiaaliselostus.rakennuspaikanMateriaalit.rakennusosanOsuus as roo {
  if RP_OSAT.contains(roo.suure.tunnus.koodi) {
    tulos = tulos + roo.arvo.numero;
  }
}
```

Vastaavasti rakennuspaikkaan kohdistuvien materiaalajien määrien summaa suhteessa rakennuspaikan pinta-alaan ei ilmoiteta erikseen, vaan se lasketaan ilmoitettujen materiaalilajikohtaisten määrien summana jaettuna rakennuspaikan pinta-alalla.

{% include common/clause_start.html type="req" id="laatu/vaat-materiaalilajien-maarien-summa-rakennuspaikalle-per-nelio" %}
Rakennuspaikkaan kohdistuvien, materiaaliselosteessa ilmoitetavien materiaalilajien yhteismäärä suhteessa rakennuspaikan pinta-alaan saadaan laskemalla ensin yhteen kaikkien [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```rakennuspaikanMateriaalit```-attribuutin arvon [RakennuspaikkakohteisetMateriaalimäärät](dokumentaatio/#rakennuspaikkakohtaisetmateriaalimäärät)-luokan mukaisen objektin sellaiset ```rakennusosanOsuus```-attribuutin ilmoittamat materiaalimäärät, joiden ilmoittaminen vaaditaan materiaaliselostuksessa kohdistettuna rakennuspaikalle. Lopuksi jaetaan saatu summa [RakennuspaikkakohteisetMateriaalimäärät](dokumentaatio/#rakennuspaikkakohtaisetmateriaalimäärät)-luokan objektin assosiaatiolla ```paikka``` viitatun [Rakennuspaikka](dokumentaatio/#rakennuspaikka)-luokan objektin ```pintaAla```-attribuutin arvolla.
{% include common/clause_end.html %}

Seuraava pseudokoodiesitys kuvaa yllä kuvatun vaatimuksen laskenta-algoritmia:
```
let tulos = 0;
let RP_OSAT = { 
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/1001",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/1002",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/1003",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/1004",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2001",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4001",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4002",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4004",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4006"
};
for each materiaaliselostus.rakennuspaikanMateriaalit.rakennusosanOsuus as roo {
  if RP_OSAT.contains(roo.suure.tunnus.koodi) {
    tulos = tulos + roo.arvo.numero;
  }
  tulos = tulos / materiaaliselostus.rakennuspaikanMateriaalit.paikka.pintaAla.value;
}
```

### Rakennuskohdekohteiset materiaalimäärät rakennusosittain

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuskohteen-materiaalimaarat-rakennusosittain" %}
Materiaaliselosteen on sisällettävä tiedot rakentamistoimenpiteessä käytettävien materiaalien määristä siltä osin, kuin ne kohdistuvat rakennukseen tai sen osaan. Materiaalimäärät on ilmoitettava seuraavien rakennusosaluokkien osalta (suluissa koodiston [Rakennuksen rakennusosan materiaalin määrä](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara) käytettävä koodi):

**Rakennusosat**:

* Alapohjat (koodi [2002](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2002))
* Runko (koodi [2003](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2003))
* Julkisivut (koodi [2004](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2004))
* Ovet (koodi [2005](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2005))
* Ikkunat (koodi [2006](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2006))
* Ulkotasot ja parvekkeet (koodi [2007](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2007))
* Katot (koodi [2008](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2008))

**Tilaosat**:

* Väliseinät (koodi [3001](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3001))
* Väliovet (koodi [3002](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3002))
* Portaat (koodi [3003](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3003))
* Lattiat (koodi [3004](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3004))
* Sisäkatot (koodi [3005](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3005))
* Seinät (koodi [3006](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3006))
* Pintakäsittelyt (koodi [3007](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3007))
* Kiintokalusteet (koodi [3008](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3008))
* Keittiölaitteet (koodi [3009](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3009))
* Hormit (koodi [3010](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3010))
* Tulisijat (koodi [3011](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3011))
* Tilaelementit (koodi [3012](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3012))

**Talotekniikka**:

* Lämmitysjärjestelmän pääosat (koodi [4001](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4001))
* Vesi- ja viemärijärjestelmän pääosat (koodi [4002](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4002))
* Ilmastointijärjestelmän pääosat  (koodi [4003](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4003))
* Jäähdytysjärjestelmän pääosat (koodi [4004](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4004))
* Sprinklerijärjestelmän pääosat (koodi [4005](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4005))
* Sähköjärjestelmän pääosat (koodi [4006](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4006))
* Hissit ja liukuportaat (koodi [4007](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4007))

Yllä luetellut rakennusosakohtaisten materiaalimäärien tiedot ilmoitetaan siten, että [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```rakennuksenOsienMateriaalit```-attribuutin arvon kukin [RakennuskohdekohteisetMateriaalimäärät](dokumentaatio/#rakennuskohdekohtaisetmateriaalimäärät)-luokan objekti sisältää tasan yhden (1) kappaleen kutakin yllä lueteltua rakennusosaa koskevaa ```rakennusosanOsuus```-attribuutin arvoa. Näiden ```rakennusosanOsuus```-attribuutin arvojen {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %}-luokan ```suure```-attribuutin ```tunnus```-attribuutin arvojen on oltava [Rakennuksen rakennusosan materiaalin määrä](http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara)-koodiston koodien tunnuksia.

[RakennuskohdekohteisetMateriaalimäärät](dokumentaatio/#rakennuskohdekohtaisetmateriaalimäärät)-luokan objektin voivat sisältää myös ```rakennusosanOsuus```-attribuutin arvoja, jotka kuvaavat muita kuin yllä lueteltuja suureita.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuskohteen-osien-materiaalimaarat-suureen-arvo" %}
[RakennuskohdekohteisetMateriaalimäärät](dokumentaatio/#rakennuskohdekohtaisetmateriaalimäärät)-luokkien objektien ```rakennusosanOsuus```-attribuuttien arvot annetaan luokan {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#suureenarvo" title="SuureenArvo" %} objekteina siten, että niiden ```arvo```-attribuuttien arvot ovat luokan {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#numeerinenarvo" title="NumeerinenArvo" %} objekteja, joiden attribuutin arvo ```yksikkö``` on kilogramma (```kg```), ja joiden ```numero``` -attribuutin arvo on ilmoitettu pyöristettynä kokonaiseen lukuun ilman desimaaleja.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakennuspaikan-osien-materiaalimaarat-per-nelio" %}
Kunkin rakennusosakohtaisen materiaalin määrä suhteessa rakennuksen toimenpidealueen lämmitettyyn nettoalaan saadaan jakamalla [RakennuskohdekohteisetMateriaalimäärät](dokumentaatio/#rakennuskohdekohtaisetmateriaalimäärät)-luokan objektin kyseistä rakennusosaa koskevan ```rakennusosanOsuus```-attribuutin sisältämän ```arvo```-attribuutin ```numero``` -attribuutin arvo [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```toimenpidealueenLämmitettyNettoala```-attribuutin arvolla.
{% include common/clause_end.html %}

#### Materiaalimäärien summat rakennuksen osalta

Rakennukseen tai sen osiin kohdistuvat materiaalimäärät ilmoitetaan materiaalilajeittain kuten yllä on kuvattu. Kaikkien ilmoitettavien materiaalilajien määrien summaa ei ilmoiteta erikseen, vaan se lasketaan ilmoitettujen materiaalilajikohtaisten määrien summana. Tulee huomata, että tämä summa ei välttämättä vastaa kaikkien rakennuksen tai sen osan rakentamiseen käytetyn materiaalin kokonaismäärää, sillä kaikkia käytettäviä materiaalilajeja ei tarvitse ilmoittaa.

{% include common/clause_start.html type="req" id="laatu/vaat-materiaalilajien-maarien-summa-rakennuskohteelle" %}
Rakennukseen tai sen osiin kohdistuvien, materiaaliselosteessa ilmoitetavien materiaalilajien yhteismäärä saadaan laskemalla yhteen kaikkien [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin kaikkien ```rakennuksenOsienMateriaalit```-attribuutin arvojen [RakennuskohdekohteisetMateriaalimäärät](dokumentaatio/#rakennuskohdekohtaisetmateriaalimäärät)-luokan mukaisten objektien sellaiset ```rakennusosanOsuus```-attribuutin ilmoittamat materiaalimäärät, joiden ilmoittaminen vaaditaan materiaaliselostuksessa kohdistettuna rakennukselle.
{% include common/clause_end.html %}

Seuraava pseudokoodiesitys kuvaa yllä kuvatun vaatimuksen laskenta-algoritmia:
```
let tulos = 0;
let RAK_OSAT = { 
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2002",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2002",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2003",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2004",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2005",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2006",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2007",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2008",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3001",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3002",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3003",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3004",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3005",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3006",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3007",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3008",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3009",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3010",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3011",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3012",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4001",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4002",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4003",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4004",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4005",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4006",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4007"
};
for each materiaaliselostus.rakennuskohteenMateriaalit as rkm {
  for each rkm.rakennusosanOsuus as roo {
    if RAK_OSAT.contains(roo.suure.tunnus.koodi) {
      tulos = tulos + roo.arvo.numero;
    }
  }
}
```

Vastaavasti rakennukseen tai sen osiin kohdistuvien materiaalajien määrien summaa suhteessa rakennuspaikan pinta-alaan ei ilmoiteta erikseen, vaan se lasketaan ilmoitettujen materiaalilajikohtaisten määrien summana jaettuna rakennuksen toimenpidealan lämmitetyllä nettoalalla.

{% include common/clause_start.html type="req" id="laatu/vaat-materiaalilajien-maarien-summa-rakennuskohteelle-per-nelio" %}
Rakennukseen tai sen osiin kohdistuvien, materiaaliselosteessa ilmoitetavien materiaalilajien yhteismäärä suhteessa rakennuksen toimenpidealueen lämmitettyyn nettoalaan saadaan laskemalla ensin yhteen kaikkien [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```rakennuksenOsienMateriaalit```-attribuuttien arvojen [RakennuskohdekohteisetMateriaalimäärät](dokumentaatio/#rakennuskohdekohtaisetmateriaalimäärät)-luokan mukaisten objektien sellaiset ```rakennusosanOsuus```-attribuutin ilmoittamat materiaalimäärät, joiden ilmoittaminen vaaditaan materiaaliselostuksessa kohdistettuna rakennukselle. Lopuksi jaetaan saatu summa [Materiaaliseloste](dokumentaatio/#materiaaliseloste)-luokan objektin ```toimenpidealueenLämmitettyNettoala```-attribuutin arvolla.
{% include common/clause_end.html %}

Seuraava pseudokoodiesitys kuvaa yllä kuvatun vaatimuksen laskenta-algoritmia:
```
let tulos = 0;
let RAK_OSAT = { 
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2002",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2002",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2003",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2004",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2005",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2006",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2007",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/2008",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3001",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3002",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3003",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3004",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3005",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3006",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3007",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3008",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3009",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3010",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3011",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/3012",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4001",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4002",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4003",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4004",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4005",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4006",
  "http://uri.suomi.fi/codelist/rytj/ms-rakennusosan-materiaalimaara/code/4007"
};
for each materiaaliselostus.rakennuskohteenMateriaalit as rkm {
  for each rkm.rakennusosanOsuus as roo {
    if RAK_OSAT.contains(roo.suure.tunnus.koodi) {
      tulos = tulos + roo.arvo.numero;
    }
  }
  tulos = tulos / materiaaliselostus.toimenpidealueenLämmitettyNettoala.value;
}
```


