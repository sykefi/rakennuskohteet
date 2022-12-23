---
layout: "default"
description: ""
id: "elinkaarisaannot"
status: "Luonnos"
---
# Elinkaarisäännöt
{:.no_toc}

1. 
{:toc}

## Johdanto

Rakennuskohteiden ja huoneistojen tietokohteilla on elinkaari, joka määrää miten kyseiset tietokohteet syntyvät, miten ne voivat muuttua elinkaarensa aikana, ja miten niiden elinkaari päättyy. Elinkaarisääntöjen määrittely liittyy olennaisesti tietokohteiden versionhallintaan, eli miten yksittäisten tietokohteiden niiden elinkaaren aikana muodotettavat versiot voidaan tallentaa ja yksilöidä viittauskelpoisten pysyvien tunnusten avulla. Tässä annetut säännöt pohjautuvat paikkatietokohteiden yksilöivien tunnusten ja elinkaarisääntöjen periaatteisiin, jotka on kuvattu jukishallinnon suosituksessa [JHS 193 - Paikkatiedon yksilöivät tunnukset](http://www.jhs-suositukset.fi/suomi/jhs193).

### HTTP URI -tunnukset

HTTP URI -muotoiset tunnukset ovat [RFC 3986 -standardiin](https://tools.ietf.org/html/rfc3986) perustuvia HTTP(S) -protokollan mukaisia URI-osoitteita (Uniform Resource Identifier), joiden globaali yksilöivyys varmistetaan Internetin DNS-nimipalveluun rekisteröityjen domain-nimien avulla. Kullakin DNS-palveluun rekisteröidyllä domain-nimellä (esim. ```uri.suomi.fi```) on yksiselitteinen omistaja, joka on suoraan tai välillisesti vastuussa ko. domain-nimen alla julkaistavasta sisällöstä. Nimen omistaja on myös ainoa taho, joka voi päättää ko. domain-nimeä käyttävien osoitteiden ohjautumisesta haluttuihin resursseihin, mikä tekee siitä luontevan perustan yksilöivien tunnusten nimiavaruuksille (esim. <http://uri.suomi.fi/object/rytj/kaava>). HTTP URI -muotoisen tunnuksen yksilöivyys perustuu siis domain-nimien ja siten niihin perustuvien nimiavaruuksien keskitettyyn hallintaprosessiin.

URI-tunnuksen ei tarvitse viitata konkreettiseen sijaintiin internetissä, vaan se voi olla abstraktimpi tunnus. [JHS 193 Paikkatiedon yksilöivät tunnukset](http://www.jhs-suositukset.fi/suomi/jhs193) määrittelee paikkatiedon yksilöiville tunnuksille muodon <http://paikkatiedot.fi/{tunnustyyppi}/{aineistotunnus}/{paikallinen tunnus}>, jossa paikkatietokohteiden ```tunnustyyppi``` on ```so```. Rakennennetun ympäristön yhteisiin tietokomponentteihin perustuvissa tietomalleissa on esimerkkinä käytetty tunnusmuotoa 
<http://uri.suomi.fi/object/rytj/{aineistotyyppi}/{TietotyypinNimi}/{paikallinenTunnus}>. HTTP URI -muotoisen tunnuksen etuna on luettavuus sekä DNS- ja HTTP-protokollien tarjoama kyky ratkaista (resolve) tunnus ja ohjata kysyjä sitä kuvaavaan Internet-resurssiin ilman tarvetta erityiselle keskitetylle tunnusrekisterille ja siihen perustuvalle ratkaisupalvelulle.

Tässä tietomallissa HTTP URI -muotoa käytetään [viittaustunnus](#viittaustunnus)-attribuutissa, jonka avulla viitataan tiettyyn versioon tietokohteesta tämän tietomallin ulkopuolelta.

### UUID-tunnukset
UUID (Universally Unique Identifier) on OSF:n (Open Software Foundation) määrittelemä standardoitu tunnusmuoto, jonka avulla voidaan luoda vakiokokoisia, hyvin suurella todennäköisyydellä yksilöiviä tunnuksia ilman keskitettyä hallintajärjestelmää. UUID-tunnukset voivat perustua satunnaislukuihin, aikaleimoihin, tietokoneiden verkkokorttien MAC-osoitteisiin tai merkkijonomuotoisiin nimiavaruuksiin eri yhdistelmissä. UUID-tunnukset erityisen hyvin tietojärjestelmissä, joissa uusia globaalisti pysyviä ja yksilöiviä tunnuksia on tarpeen luoda hajautetusti ilman keskitettyä tunnusrekisteriä.

Tässä tietomallissa UUID-muotoisia tunnuksia suositellaan käytettäväksi [identiteettitunnus](#identiteettitunnus)- ja [tuottajakohtainen tunnus](#tuottajakohtainen-tunnus)-attribuuttien arvoina.

## Tietomallin kohteiden elinkaaren hallinnan periaatteet
Tietomallin elinkaarisäännöt mahdollistavat mallin tietokohteiden käsittelyn, tallentamisen ja muuttamisen hallitusti sekä niiden laatimis- että voimassaolovaiheissa. Tietomallin mukaiset tietosisällöt ovat merkittäviä oikeusvaikutuksia aiheuttavia, juridisesti päteviä aineistoja, joita käsitellään hajautetusti eri toimijoiden tietojärjestelmissä. Tämän vuoksi niiden tunnusten, viittausten ja versionnin hallintaan on syytä kiinnittää erityistä huomiota.

Seuraavat keskeiset periaatteet ohjaavat tietomallin elinkaaren hallintaa:
* Kukin yhteen tietovarastoon tallennetuista tietokohteista saa pysyvän, versiokohtaisen tunnuksen.
* Kuhunkin yietovarastoon tallennettun tietokohteen versioon voidaan viitata sen pysyvän tunnuksen avulla.
* Tietomallin tietokohteiden väliset viittaukset toteutetaan hallitusti sekä tietoa tuottavissa tietojärjestelmissä että yhteisissä tietovarastoissa.
* Tietovarasto vastaa pysyvien tunnusten luomisesta ja antamisesta tallennettaville tietokohteille.

## Tunnukset ja niiden hallinta

### Identiteettitunnus
Identiteettitunnus yhdistää saman tietokohteen kehitysversiot toisiinsa.

{% include common/clause_start.html type="req" id="elinkaari/vaat-identiteettitunnus-maar" %}
Tietomallin tietokohteissa identiteettitunnus kuvataan attribuutilla ```identiteettiTunnus```. Kahdella tietomallin versioitavalla objektilla voi olla sama ```identiteettiTunnus```-attribuutin arvo ainoastaan, mikäli kaikki seuraavista ehdoista ovat tosia:
* Molemmat objektit kuvaavat saman tietokohteen kehityskaaren eri tiloja.
* Molemmat objektit ovat saman loogisen tietomallin luokan edustajia.
{% include common/clause_end.html %}

Yksittäisen tietokohteen tiettyyn tietovarastoon tallennettu kehityshistoria saadaan noutamalla kaikki ko. tyyppisen tietokohteen objektit, joilla on sama ```identiteettiTunnus```-attribuutin arvo.

Tietovarasto on vastuussa uusien identiteettitunnusten luomisesta tarvittaessa tallennustapahtumien yhteydessä, ja niiden välittämisestä tiedoksi tallentavalle tietojärjestelmälle. Tallentavan tietojärjestelmän tulee tallentaa itselleen kopiot tietovaraston tallennustapahtuman yhteydessä palautamista tietokohteiden identiteettitunnuksista, sillä ne tulee sisällyttää ko. tietokohteiden seuraavien versioden tallennettavaksi lähetettäviin objekteihin.

{% include common/clause_start.html type="req" id="elinkaari/vaat-identiteettitunnus-gen" %}
* Mikäli tallennettavalle tietokohteelle ei ole annettu ```identiteettitunnus```-attribuuttia, tai tietovarasto ei sisällä sellaista saman luokan tietokohdetta, jolla sama ```identiteettiTunnus```-attribuutin arvo, tietovarasto luo ko. objektille uuden identiteettitunnuksen, joka korvaa tuottavan tietojärjestelmän objektille mahdollisesti antaman ```identiteettiTunnus```-attribuutin arvon. Tällöin objektia pidetään uuden tietokohteen ensimmäisenä versiona.
* Mikäli tietovarasto sisältää saman luokan tietokohteen, jolla on sama ```identiteettiTunnus```-attribuutin arvo kuin tallennetavalla objektilla, objekti tallennetaan tietovarastoon ko. tietokohteen uutena versiona. Tällöin tallennettavan objektin ```identiteettiTunnus```-attribuutin arvo ei muutu.
{% include common/clause_end.html %}

{% include common/clause_start.html type="rec" id="elinkaari/suos-identiteettitunnus-form" %}
Identiteettitunnuksen suositeltu muoto on UUID.
{% include common/clause_end.html %}

Esimerkki: ```640bff6b-c16a-4947-af8d-d86f89106be1```

### Paikallinen tunnus
Paikallinen tunnus yksilöi tietokohteen yhden version tietovaraston sisällä. 

{% include common/clause_start.html type="req" id="elinkaari/vaat-paikallinentunnus-maar" %}
Tietomallin tietokohteissa paikallinen tunnus kuvataan attribuutilla ```paikallinenTunnus```. Kaikilla saman tietovaraston objekteilla (ml. saman tietokohteen eri versiot) tulee olla eri ```paikallinenTunnus```-attribuutin arvo.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-paikallinentunnus-gen" %}
Tietokohteiden paikallinen tunnus muuttuu sen jokaisen version tallennuksen yhteydessä. Tietovarasto vastaa paikallisten tunnusten luomisesta tallennustapahtuman yhteydessä. Tuottavan tietojärjestelmän mahdollisesti asettamat arvot korvataan.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-paikallinentunnus-form" %}
Paikallinen tunnus koostuu identiteettitunnuksesta ja siihen erotinmerkillä liitetystä versiokohtaisesta, esimerkiksi tarkkaan tallennusajanhetkeen perustuvasta merkkijonosta.
{% include common/clause_end.html %}

{% include common/clause_start.html type="rec" id="elinkaari/suos-paikallinentunnus-merk" %}
Paikallisen tunnuksen muodostamisessa tulee välttää merkkejä, jotka joudutaan URL-koodaamaan rajapintapalvelujen kutsuissa. Paikkatietokohteen paikallista tunnusta käytetään fyysisten tietomallien pääavaimena, esim. GeoJSON Feature ```id```-omaisuuden ja GML:n ```gml:id```-attribuutin arvona, ja siten esimerkiksi OGC Web Feature Service (WFS) - ja OGC API - Features -rajapintapalvelujen paikkatietokohteen yksilöivissä kyselyissä.
{% include common/clause_end.html %}

Tallennusajanhetkeen päättyvää paikallista tunnusta voidaan käyttää ilman sekaannusmahdollisuuksia samalla logiikalla myös paikallisissa versionneissa, eli sellaisissa tietokohteiden versioiden tallennuksissa, joita ei viedä lainkaan tietovarastoon.

Esimerkki: ```640bff6b-c16a-4947-af8d-d86f89106be1.b05cf48d46d8c905c54522f44b0a12daff11604e```

{% include common/note.html content="Käyttämällä paikallisena tunnuksena pelkkää identiteettitunnuksesta riippumatonta UUID-tunnusta päästäisiin lyhyempiin tunnuksiin, mutta menetetään yhteys identiteettitunnusten ja paikallisten tunnusten välillä, mikä saattaa hankaloittaa erilaisten vikatilanteiden selvitystä ja toimintavarmuuden testaamista, kun pelkkien tunnusten perusteella ei voida päätellä ovatko kaksi objektia saman tietokohteen eri versioita." %}

### Nimiavaruus
{% include common/clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-maar" %}
Nimiavaruus määrää tietomallin kaikkien tietokohteiden viittaustunnusten alkuosan yhden tietovaraston sisällä. Tietomallin tietokohteissa paikallinen tunnus kuvataan attribuutilla ```nimiavaruus```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-form" %}
Nimiavaruus on HTTP URI -muotoinen.
{% include common/clause_end.html %}

Nimiavaruus on syytä valita huolella siten, että se olisi mahdollisimman pysyvä, eikä sitä tarvitsisi tulevaisuudessa muuttaa esimerkiksi valtionhallinnon virastojen tai ministeriröiden mahdollisten uudelleenorganisointien ja -nimeämisten johdosta. Valittu URL-osoite tulee myös voida aina tarvittaessa ohjata kulloinkin käytössä olevaan rajapintapalveluun (HTTP redirect). 

{% include common/clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-gen" %}
Tietovarasto vastaa ```nimiavaruus```-attribuuttien asetamisesta tallennustapahtuman yhteydessä. Tuottavan tietojärjestelmän mahdollisesti antamat arvot korvataan.
{% include common/clause_end.html %}

Esimerkki: ```http://uri.suomi.fi/object/rytj/raklupa```

### Viittaustunnus
{% include common/clause_start.html type="req" id="elinkaari/vaat-viittaustunnus-maar" %}
Viittaustunnus yksilöi tietokohteen yhden, tietovaraston tallentun kehitysversion globaalisti. Tietomallin tietokohteissa paikallinen tunnus kuvataan attribuutilla ```viittausTunnus```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-viittaustunnus-form" %}
Viittaustunnus on HTTP URI -muotoinen ja se muodostuu nimiavaruudesta, tietokohteen luokan nimestä ja paikallisesta tunnuksesta yhdessä kauttaviivoilla (```/```) erotettuina.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-gen" %}
Tietovarasto vastaa ```viittausTunnus```-attribuuttien asetamisesta tallennustapahtuman yhteydessä. Tuottavan tietojärjestelmän mahdollisesti antamat arvot korvataan.
{% include common/clause_end.html %}

Tallentavan tietojärjestelmän ei siis tarvitse tallentaa luotuja viittaustunnuksia itselleen seuraavia tallennuksia varten.

{% include common/clause_start.html type="rec" id="elinkaari/suos-viittaustunnus-ohj" %}
Viittaustunnuksen on suositeltavaa ohjautua aina ko. tietokohteen version tietosisältöön kulloinkin toiminnassa olevassa tietovaraston latauspalvelussa.
{% include common/clause_end.html %}

Esimerkki: ```http://uri.suomi.fi/object/rytj/raklupa/BuildingPermit/640bff6b-c16a-4947-af8d-d86f89106be1.b05cf48d46d8c905c54522f44b0a12daff11604e```

### Tuottajakohtainen tunnus

{% include common/clause_start.html type="req" id="elinkaari/vaat-tuottajakohtainen-tunnus-maar" %}
Rakennuskohteiden tietoa tuottavat järjestelmät voivat niin halutessaan käyttää tuottajakohtaista tunnusta niiden omien tietojärjestelmäspesifisten tunnusten antamiseen tietomallin tietokohteille. Tietomallin tietokohteissa tuottajakohtainen tunnus kuvataan attribuutilla ```tuottajakohtainenTunnus```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-tuottajakohtainen-tunnus-gen" %}
Tietovarasto ei koskaan muuta tuottavan tietojärjestelmän mahdollisesti asettamia tuottajakohtaisia tunnuksia, ja ne palautetaan sellaisenaan latattaessa tietokohteita tietovarastosta.
{% include common/clause_end.html %}

Tietojärjestelmät voivat käyttää tuottajakohtaisia tunnuksia kohdistamaan tietovarastoon ja paikallisiin tietojärjestelmiin tallennettuja tietokohteita toisiinsa esimerkiksi päivitettäessä niiden tallennuksen yhteydessä syntyneitä tunnuksia, vertailtaessa tietovarastoon tallennettuja kohteita ja paikallisia kohteita toisiinsa, sekä esitettäessä validointipalvelun tuloksia suunnitteluohjelmiston käyttäjälle.

Tuottajakohtaisilta tunnuksilta ei vaadita yksilöivyyttä tai mitään tiettyä yhtenäistä muotoa, mutta UUID-muodon käyttäminen tarjoaa hyvin määritellyn ja standardoidun tavan luoda tuottajakohtaisista tunnuksista yksilöiviä eri tietojärjestelmien kesken. Tästä saattaa olla etua haluttaessa tehdä tuotettavista rakennuskohteiden tiedoista mahdollisimman järjestelmäriippumattomia ja esimerkiksi taata tuottajakohtaisten tunnusten yksilöivyys yli mahdollisten tietojärjestelmien vaihdosten ja päivitysten. 

{% include common/clause_start.html type="rec" id="elinkaari/suos-tuottajakohtainen-tunnus-form" %}
Tuottajakohtaisen tunnuksen suositeltu muoto on UUID.
{% include common/clause_end.html %}

Esimerkki: ```k-123445```


### Pysyvien tunnusten palauttaminen tuottavalle järjestelmälle

Versionhallinnan näkökulmasta on tärkeää, että rakennuskohteiden tietoja tuottava tietojärjestelmä käyttää samaa, tietovarastoon tallennettua tietokohdetta päivtettäessä sen ensimmäisen tallennuksen yhteydessä luotua identiteettitunnusta, mikäli objektin katsotaan kuvaavan ko. tietokohteen uutta versiota.

{% include common/clause_start.html type="req" id="elinkaari/vaat-tunnusten-palautus" %}
Tietovaraston tallennusrajapinta palauttaa tallennetun rakennuskohteiden tiedot tuottavalle tietojärjestelmälle tallennusoperaation yhteydessä siten, että ne sisältävät yllä mainittujen tunnustenhallintasääntöjen mukaisesti mahdollisesti generoidut tai muokatut identiteettitunnukset, paikalliset tunnukset, nimiavaruudet ja viittaustunnukset kaikille tallennetuille tietokohteille.
{% include common/clause_end.html %}

### Tietokohteisiin viittaaminen ja viitteiden ylläpito

{% include common/clause_start.html type="req" id="elinkaari/vaat-tietovaraston-sisaiset-viittaukset" %}
Tietokohteiden assosiaatiot eri tietomallien tietokohteiden välillä toteutetaan viitattavan tietokohteen [viittaustunnus](#viittaustunnus)-attribuuttia käyttäen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-viittaukset-ulkoa" %}
Pysyvät viittaukset tietomallin tietokohteisiin ulkopuolisista tietojärjestelmistä toteutetaan viitattavan tietokohteen [viittaustunnus](#viittaustunnus)-attribuuttia käyttäen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-viittaukset-tallennettaessa" %}
Tallennettaessa tietomallin tietokohteita tietovarastoon tietokohteiden tunnukset muuttuvat niiden pysyvään muotoon, kuten kuvattu luvussa [Tunnukset ja niiden hallinta](#tunnukset-ja-niiden-hallinta). Tietovaraston vastuulla on päivittää kunkin paikallisen tunnuksen muuttamisen yhteydessä myös kaikkien ko. tietokohteen versioon sen paikallisen tunnuksen avulla viittaavien muiden ko. rakennuskohteiden tietomallin tietokohteiden viittaukset käyttämään tietokohteen muutettua paikallista tunnusta.   
{% include common/clause_end.html %}

### Koodistojen koodien tunnuksiin liittyvät vaatimukset

{% include common/clause_start.html type="req" id="elinkaari/vaat-koodien-yksiloivat-tunnukset" %}
Kullakin koodiston koodilla on oltava pysyvä tunnus, joka sellaisenaan yksilöi kyseisen koodin globaalisti ilman erilistä tietoa koodistosta, johon koodi kuuluu. Koodin tunnus on HTTP URI -muotoinen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-alakoodi-maar" %}
Olkoon koodi ```A``` mikä tahansa hierarkkisen koodiston sisältämä koodi. Koodin ```A``` alakoodilla tarkoitetaan koodia, joka on hierakkiassa sijoitettu koodin ```A``` alle. Koodi voi olla useamman ylemmän tason koodin alakoodi vain mikäli ko. ylemmän tason koodit ovat alakoodisuhteessa keskenään.
{% include common/clause_end.html %}

Käytännössä tietyn koodin alakoodit voidaan tunnistaa vertaamalla niiden tunnuksia:

{% include common/clause_start.html type="req" id="elinkaari/vaat-alakoodi-tunnus" %}
Koodin ```A``` alakoodin ```B``` tunnus alkaa koodin ```A``` tunnuksella ja sisältää sen jälkeen yhden tai useamman merkin.
{% include common/clause_end.html %}

## Muutokset ja tietojen versionti
{% include common/clause_start.html type="req" id="elinkaari/vaat-pysyva-sisalto" %}
Takennuskohteiden tietomallin mukaisten tietojen tallennusoperaatio tietovarastoon muodostaa uuden version tallennettavista tietokohteista, mikäli yksittäinen tietokohde on miltään osin muuttunut verrattuna sen edelliseen versioon. Myös muutokset niissä tietomallin tietokohteissa, joihin tallennettavasta tietokohteesta viitataan, lasketaan ko. tietokohteen muutoksiksi. Tallennetun tietokohteen version sisältö ei voi muuttua tallennuksen jälkeen, poislukien sen voimassaolon päättymiseen, seuraavaan versioon linkittämiseen ja elinkaaritilaan liittyvät attribuutit, joita tietovarasto itse päivittää sen tiettyjen elinkaaritapahtumien yhteydessä.
{% include common/clause_end.html %}

Näin taataan ulkoisten viittausten eheys, sillä kaikkien tietokohteiden paikalliset ja viittaustunnukset viittaavat aina vain tiettyn, sisällöllisesti muuttumattomaan versioon viittatusta kohteesta. Suositeltavaa on, että kaikki tallennusversiot myös pidetään pysyvästi tallessa, jotta mahdolliset keskenäiset ja ulkopuolelta tulevat linkit eivät mene rikki muutosten yhteydessä.

### Yksittäisen tietokohteen muutoshistoria
Tietomalli mahdollistaa tunnistettavien tietokohteiden eri kehitysversioiden erottamisen toisistaan. Kullakin tietomallin kohteella on sekä sen tosimaailman identiteettiin liittyvä ns. identiteettitunnus että yksittäisen tallennusversion tunnus (paikallinen tunnus). Tallennettaessa uutta versiota samasta tietokohteesta, sen identiteettitunnus pysyy ennallaan, mutta sen paikallinen tunnus muuttuu. Versioitavien objektien suhteen samuuden määritteleminen on tietoja tuottavien järjestelmien vastuulla: mikäli objektilla on tallennettavaksi lähetettäessä saman ```identititeettiTunnus```-attribuutin arvo kuin aiemmin tallennetulla, samantyyppisellä tietokohteella, katsotaan uusi objekti on saman tietokohteen uudeksi versioksi.

{% include common/clause_start.html type="req" id="elinkaari/vaat-version-korvaus" %}
Kun tietokohteesta tallennetaan uusi muuttunut versio, jonka on tarkoitus korvata ko. kohteen aiemmin tallennettu versio, tulee tietokohteen edellisen version ```korvattuObjektilla```-assosiaatio asettaa viittaamaan tietokohteen uuteen versioon. Uuden tietokohteen version ```korvaaObjektin```-assosiaatio puolestaan asetetaan viittaamaan tietokohteen edelliseen, korvattavaan versioon. Molempien kohteiden ```tallennusAika```-attribuutin arvoksi asetetaan ajanhetki, jolloin tallennus ja muutos tietovarastoon on tehty.
{% include common/clause_end.html %}

Yksittäisen tietokohteen yksityiskohtainen muutoshistoria tietovarastossa saadaan seuraavalla sen ```korvattuObjektilla```- ja ```korvaaObjektin```-assosiaatioita. 

Attribuutin ```viimeisinMuutos``` arvo kuvaa ajanhetkeä, jolloin ko. tietokohteeseen on tehty sisällöllinen muutos tiedontuottajan tietojärjestelmässä. Tiedontuottajan järjestelmän osalta ei vaadita tiukkaa versiontipolitiikkaa, eli ```paikallinenTunnus```-attribuutin päivittämistä jokaisen tietokohteen muutoksen johdosta. ```viimeisinMuutos```-attribuutin päivittämien riittää kuvaamaan tiedon todellisen muuttumisajankohdan.


## Suunnitelman ja toteuman mukaiset Rakennuskohteet

Tietomallissa sekä suunnitellut että rakentamishankkeiden lopputuloksina toteutuneet rakennuskohteiden tiedot kuvataan saman [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan avulla.

{% include common/clause_start.html type="req" id="elinkaari/vaat-suunniteltu-rakennuskohde" %}
[Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan objekti, jonka ```tiedonLaji```-attribuutin arvo viittaa [RakennuskohteenTiedonLaji](dokumentaatio/#rakennuskohteentiedonlaji)-koodiston koodiin ```1 - Suunnitelman mukainen tieto```, kuvaa rakennuskohteen suunnitelua tilaa siihen kohdistuvan muutoksen toteuttamisen jälkeen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-toteutunut-rakennuskohde" %}
[Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan objekti, jonka ```tiedonLaji```-attribuutin arvo viittaa [RakennuskohteenTiedonLaji](dokumentaatio/#rakennuskohteentiedonlaji)-koodiston koodiin ```2 - Toteuman mukainen tieto```, kuvaa rakennuskohteen toteutunutta tilaa siihen kohdistuvan muutoksen toteuttamisen jälkeen.
{% include common/clause_end.html %}

### Muutossuunnitelman yhteys aiempaan toteumaan
{% include common/clause_start.html type="req" id="elinkaari/vaat-suunnitellun-rakennuskohteen-lahtokohta" %}
Kun toteutettuun rakennuskohteeseen laaditaan muutos-, laajennus- tai korjaussuunnitelma, tehdään kyseisen rakennuskohteen suunniteltua muutosta edeltävän tilan mukaisesta [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan objektista (T1) uusi versio (S1), jonka ```identiteettiTunnus``` pysyy samana, mutta ```tiedonLaji```-attribuutin arvoksi tulee  ```1 - Suunnitelman mukainen tieto```. Objektilla T1 ei tässä tapauksessa saa olla ```korvattuObjektilla```-assosiaatiota objektiin S1, eikä objektilla S1 saa olla ```korvaaObjektin```-assosiaatiota objektiin T1. Objektilla S1 tulee olla assosiaatio ```liittyväKohde``` määritteen ```rooli``` arvolla ```Suunnitelman lähtökohta``` objektiin T1.

Mikäli muutosta edeltävää toteutettua tilaa vastaavaa [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan objektia T1 ei ole saatavilla, luodaan uusi [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan objekti (S1), joka kuvaa rakennuskohteen suunnitelua muutettua tilaa, ja jonka ```tiedonLaji```-attribuutin arvoksi tulee  ```1 - Suunnitelman mukainen tieto```. 
{% include common/clause_end.html %}

### Muutossuunnitelmien päivitys ja yhteys uuteen toteumaan
{% include common/clause_start.html type="req" id="elinkaari/vaat-rakennuskohteen-suunnitelman-muutos" %}
Kun rakennuskohteen suunnitelmaa päivitetään, tehdään kyseisen rakennuskohteen edeltävän suunnitelman mukaisesta [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan objektista (S1) uusi versio (S2), jonka ```identiteettiTunnus``` pysyy samana, ja ```tiedonLaji```-attribuutin arvoksi tulee  ```1 - Suunnitelman mukainen tieto```. Objektilla S1 tulee olla  ```korvattuObjektilla```-assosiaatio objektiin S2, ja objektilla S2 tulee olla ```korvaaObjektin```-assosiaatio objektiin S1. Objektilla S2 tulee olla assosiaatio ```liittyväKohde``` määritteen ```rooli``` arvolla ```Suunnitelman lähtökohta``` objektiin T1.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-rakennuskohteen-uusi-toteuma" %}
Kun rakennuskohteen muutostoimenpide on toteutettu, tehdään kyseisen rakennuskohteen viimeisimmän suunnitelman mukaisesta [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan objektista (S2) uusi versio (T2), jonka tiedot vastaavat rakennuskohteen uutta toteutunutta tilaa. Objektin T2  ```identiteettiTunnus``` pysyy samana, ja ```tiedonLaji```-attribuutin arvoksi tulee  ```2 - Toteuman mukainen tieto```. Objektilla T2 tulee olla  ```korvaaObjektin```-assosiaatio muutosta edeltäneeseen kyseisen rakennuskohteen toteutunutta tilaa kuvaavaan objektiin (T1), ja objektilla T1 tulee olla ```korvattuObjektilla```-assosiaatio objektiin T2. Objektilla T2 tulee olla assosiaatio ```liittyväKohde``` määritteen ```rooli``` arvolla ```Toteutettu suunnitelma``` objektiin S2, ja  assosiaatio ```liittyväKohde``` määritteen ```rooli``` arvolla ```Alkuperäinen suunnitelma``` siihen [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan objektiin (S1), joka kuvaa alkuperäistä muutossuunnitelmaa.
{% include common/clause_end.html %}

### Rakennusten ja rakennelmien elinkaaren vaiheet ja suunnitellut muutokset

Luokilla [RakennusTaiSenOsa](dokumentaatio/rakennustaisenosa) ja [RakennelmaTaiSenOsa](dokumentaatio/rakennelmataisenosa) on attribuutti ```elinkaarenVaihe```, joka arvojoukko on koodiston [RakennuksenElinkaarenVaihe](dokumentaatio/#rakennuksenelinkaarenvaihe) mukainen. 

{% include common/clause_start.html type="req" id="elinkaari/vaat-uudisrakennuksen-elinkaaren-vaihe-ja-suunnitelma" %}
Uudisrakennuksen tai -rakennelman tai niiden uusien osien tapauksessa luokkien [RakennusTaiSenOsa](dokumentaatio/rakennustaisenosa) tai [RakennelmaTaiSenOsa](dokumentaatio/rakennelmataisenosa) attribuutin ```tiedonLaji``` arvon ollessa ```1 - Suunnitelman mukainen tieto```, tulee sen attribuutilla ```elinkaarenVaihe``` olla joko arvo ```01 - suunnitteilla``` tai ```02 - rakenteilla```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-toteutetun-rakennuksen-elinkaaren-vaihe" %}
Toteutettua rakennuskohdetta kuvaavan [RakennusTaiSenOsa](dokumentaatio/rakennustaisenosa) ja [RakennelmaTaiSenOsa](dokumentaatio/rakennelmataisenosa) luokan attribuutin ```tiedonLaji``` arvon ollessa ```2 - Toteuman mukainen tieto```, tulee sen attribuutilla ```elinkaarenVaihe``` olla jokin arvoista ```02 - rakenteilla```, ```03 - käytössä``` tai ```04 - käyttökiellossa/käyttökelvoton```, ```05 - tuhoutunut``` tai ```06 - purettu```. Arvoa ```02 - rakenteilla``` voidaan käyttää vain, mikäli rakennuskohde on valmistunut, mutta sen käyttöönottokatselmusta ei ole vielä hyväksytysti pidetty.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-rakennuksen-elinkaaren-vaihe-ja-muutossuunnitelma" %}
Muutettavan, laajennettavan, korjattavan tai purettavan rakennuksen tai -rakennelman tai niiden uusien osien tapauksessa luokkien [RakennusTaiSenOsa](dokumentaatio/rakennustaisenosa) tai [RakennelmaTaiSenOsa](dokumentaatio/rakennelmataisenosa) attribuutin ```tiedonLaji``` arvon ollessa ```1 - Suunnitelman mukainen tieto```, tulee sen attribuutin ```elinkaarenVaihe``` arvon vastata kuvata suunnitelman toteuttamisen jälkeistä tavoitetilaa: joko ```03 - käytössä``` tai ```06 - purettu```.
{% include common/clause_end.html %}


{% include common/clause_start.html type="req" id="elinkaari/vaat-rakennuksen-elinkaaren-vaiheen-sallitut-muutokset" %}
Luokkien [RakennusTaiSenOsa](dokumentaatio/rakennustaisenosa) tai [RakennelmaTaiSenOsa](dokumentaatio/rakennelmataisenosa) attribuutin ```elinkaarenVaihe``` arvo voi muuttua [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan kuvaamana vain seuraavasti:

* Arvosta ```01 - suunnitteilla``` arvoihin ```02 - rakenteilla``` tai ```03 - käytössä```.
* Arvosta ```02 - rakenteilla``` arvoihin ```03 - käytössä``` tai ```04 - käyttökiellossa/käyttökelvoton```, ```05 - tuhoutunut``` tai ```06 - purettu```.
* Arvosta ```03 - käytössä``` arvoihin ```04 - käyttökiellossa/käyttökelvoton```, ```05 - tuhoutunut```, ```06 - purettu```, ```07 - yhdistetty tai jaettu``` tai ```08 - rakennelma muutettu rakennukseksi```
* Arvosta ```04 - käyttökiellossa/käyttökelvoton``` arvoihin ```02 - rakenteilla```, ```03 - käytössä```, ```05 - tuhoutunut```, ```06 - purettu```, ```07 - yhdistetty tai jaettu``` tai ```08 - rakennelma muutettu rakennukseksi```.
* Arvoista ```05 - tuhoutunut```, ```06 - purettu```, ```07 - yhdistetty tai jaettu``` ja ```08 - rakennelma muutettu rakennukseksi``` ei ole sallittuja muutoksia.
{% include common/clause_end.html %}

## Rakennuskohteiden muutostoimenpiteet

Sekä uusien rakennuskohteiden suunnitelmat että aiemmin toteutettujen rakennuskohteiden muutos-, laajennus-, korjaus- ja purkamissuunnitelmat kuvataan [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan avulla. Luokka sisältää toimenpiteen kuvaustietojen lisäksi varsinaiset suunnitellut muutokset, jotka kuvataan luokan [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokan mukaisina rakenteisina ```suunniteltuMuutos```-attribuutin arvoina.

Rakennettujen tilojen ja huoneistojen suunnitellut muutokset kuvataan osana [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokan tietoja.

### Uudisrakennuskohteen rakentamistoimenpide
{% include common/clause_start.html type="req" id="elinkaari/vaat-uudiskohteen-toimenpide" %}
Uudisrakennuksen tai -rakennelman tai niiden uusien osien suunnitelma kuvataan luokan [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide) objektina, jonka attribuutilla ```toimenpiteenLaji``` on koodiston [RakentamistoimenpiteenLaji](dokumentaatio/#rakentamistoimenpiteenlaji) arvo ```01 - Uusi rakennus tai rakennelma``` tai ```02 - Laajentaminen```.

Attribuuteille ```purkamisenSyy```, ```perusparannus``` ja ```korjausaste``` ei saa antaa arvoja.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-uudiskohteen-toimenpiteen-muutokset" %}
Uudisrakennuksen tai -rakennelman tai niiden uusien osien suunnitelman kuvaamaan [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan objektiin kuuluvan [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokan kuvaaman rakenteisen attribuutin ominaisuuksina annettavien pinta-alojen ja tilavuuksien muutostietojen tulee vastata koko suunnnitellun rakennuskohteen pinta-ala ja tilavuustietoja.
{% include common/clause_end.html %}

### Olemassaolevan rakennuskohteen muutos- laajennus- tai korjaustoimenpide
{% include common/clause_start.html type="req" id="elinkaari/vaat-muutettavan-kohteen-toimenpide" %}
Muutettavan, laajennettavan tai korjattavan rakennuksen tai -rakennelman tai niiden osien suunnitelma kuvataan luokan [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide) objektina, jonka attribuutilla ```toimenpiteenLaji``` on koodiston [RakentamistoimenpiteenLaji](dokumentaatio/#rakentamistoimenpiteenlaji) arvo ```02 - Laajentaminen```, ```03 - Uudelleen rakentamiseen verrattava muutostyö``` tai ```04 - Muu muutostyö```.

Attribuutille ```purkamisenSyy``` ei saa antaa arvoa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-muutettavan-kohteen-toimenpiteen-muutokset" %}
Muutettavan, laajennettavan tai korjattavan rakennuksen tai -rakennelman tai niiden osien suunnitelman kuvaaman  [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan objektiin kuuluvan [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokan kuvaaman rakenteisen attribuutin ominaisuuksina annettavien pinta-alojen ja tilavuuksien muutostietojen tulee vastata rakennuskohteen muutoksessa muuttuvia pinta-ala ja tilavuustietoja. Pinta-alojen tai tilavuuksien pienentyessä muutosattribuuttien arvot ovat negatiivisia.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-kohteen-varusteiden-muutokset" %}
Rakennuskohteeseen sen muutostoimenpiteen johdosta kuuluvat lisättävät ja poistuvat varusteet kuvataan  [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokan Luokan [RakennuksenVaruste](dokumentaatio/#rakennuksenvaruste) mukaisen rakenteisen attribuutin ```varustemuutos``` avulla. Lisättävien varusteiden osalta käytetään attribuutin ```kuuluuKohteeseen``` arvoa ```true```, ja poistuvien varusteen osalta arvoa ```false```.
{% include common/clause_end.html %}


### Olemassaolevien rakennusten tai rakennelmien yhdistäminen

Rakennuskohteen toimenpide voi johtaa kahden tai useamman olemassaolevan, omalla pysyvällä rakennustunnuksella tunnistettavan rakennuksen tai rakennelman yhdistämiseen yhdeksi rakennukseksi. Jäljelle jäävä rakennus voi olla joko jompi kumpi alkuperäisistä rakennuksista tai uusi rakennus tai rakennelma.

{% include common/note.html content="Vaatinee ristiintarkitusta ja harmonisointia DVV:n (PRT) rakennustietojen elinkaaren tapahtumien kanssa" %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-yhdistaminen-kohteen-osittelut" %}
Mikäli yhdistämisessä jäljelle jäävä tai uutena luotu Rakennus- tai Rakennelma-luokan objekti koostuu on valmiiksi osista, päivitetään osittelut vastaamaan uutta kokonaisuutta vastaavasti kuin rakennuksen tai rakennelman laajentamistoimenpiteen tapauksessa. Mikäli taas yhdistämisessä jäljelle jäävä tai uutena luotu Rakennus- tai Rakennelma-luokan objekti ei aiemmin koostunut [RakennuksenOsa](dokumentaatio/#rakennuksenosa)- tai [RakennelmanOsa](dokumentaatio/#rakennelmanosa)-luokkien objekteista, tulee yhdistämisessä laatia uudet, poistuvia erillisiä Rakennus- ja Rakennelma-luokkien objekteja vastaavat RakennuksenOsa- ja RakennelmanOsa-luokat, jotka yhdistetään ne kokoavaan Rakennus- tai Rakennelma-luokan objektiin assosiaation ```rakennus``` tai ```rakennelma``` avulla. Yhdistettävien rakennusten tapauksessa luodaan uusi [RakennuksenOsittelu](dokumentaatio/#rakennuksenosittelu)-luokan kuvaama rakenteinen attribuutti ```osittelu```, jonka attribuutti ```ositteluperuste``` saa arvon ```2 - Rakentamishistoriaan perustuva osittelu```, ja johon uudet RakennuksenOsa-luokan objektit liitetään assosiaatiolla ```osa```. Yhdistettävien rakennelmien tapauksessa uudet RakennelmanOsa-luokan objektit liitetään suoraan Rakennelma-luokan objektiin sen assosiaatiolla ```osa```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-yhdistaminen-kohde-ennen-jalkeen" %}
Yhdistämisen sisältävää muutosta kuvaavaan [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokan objektiin tulee yhdistää assosiaation ```kohdeEnnenMuutosta``` avulla kaikkiin niihin Rakennus- tai Rakennelma-luokan objekteihin, jotka kuvaavat yhdistetyn rakennuksen tai rakennelman osia ennen niiden yhdistämistä. Samaan RakennuskohteenMuutos-luokan objektiin tulee yhdistää assosiaation ```kohdeMuutoksenJälkeen``` avulla jäljelle jäävä tai uutena luoto Rakennus- tai Rakennelma-luokan objekti.
{% include common/clause_end.html %}

#### Yhdistyminen olemassaolevaan kohteeseen

{% include common/clause_start.html type="req" id="elinkaari/vaat-kohteen-yhdistaminen-toiseen" %}
Kun kaksi tai useampi [Rakennus](dokumentaatio/#rakennus)- tai [Rakennelma](dokumentaatio/#rakennelma)-luokan objektia yhdistetään samaksi Rakennus- tai Rakennelma-kohteeksi osana [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan kuvaamaa rakentamistoimenpidettä siten, että yksi alkuperäisistä rakennuksista tai rakennelmista laajenee siihen yhdistettävillä entisten erillisten kohteiden muodostamilla osilla, tulee yhdistetyn Rakennus- tai Rakennelma-kohteen tiedot päivittää kuvaamaan uutta yhdistettyä rakennusta tai rakennelmaa. 

Jäljelle jäävän Rakennus- tai Rakennelma-luokan objektin attribuutin ```pysyväRakennusTunnus``` arvo säilyy muuttumattomana, samoin kuin sen ```identiteettiTunnus```-attribuutin arvo. Poistuvien, jäljelle jäävän kohteen uusiksi osiksi yhdistettyjen Rakennus- tai Rakennelma-luokan objektien attribuutin ```elinkaarenVaihe``` arvoksi tulee ```07 - Yhdistetty tai jaettu```.
{% include common/clause_end.html %}

#### Yhdistyminen uudeksi kohteeksi

{% include common/clause_start.html type="req" id="elinkaari/vaat-kohteen-yhdistaminen-toiseen" %}
Kun kaksi tai useampi [Rakennus](dokumentaatio/#rakennus)- tai [Rakennelma](dokumentaatio/#rakennelma)-luokan objektia yhdistetään samaksi Rakennus- tai Rakennelma-kohteeksi osana [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan kuvaamaa rakentamistoimenpidettä siten, että yhdistetylle kohteelle luodaan uusi Rakennus- tai Rakennelma-luokan objekti, tulee uuden Rakennus- tai Rakennelma-kohteen tiedoissa kuvava koko yhdistettyn rakennuksen tai rakennelman tiedot. 

Uudelle Rakennus- tai Rakennelma-luokan objektille annetaan uudet attribuuttien ```pysyväRakennusTunnus```- ja ```identiteettiTunnus``` arvot. Poistuvien, uuden kohteen uusiksi osiksi yhdistettyjen Rakennus- tai Rakennelma-luokan objektien attribuutin ```elinkaarenVaihe``` arvoksi tulee ```07 - yhdistetty tai jaettu```.
{% include common/clause_end.html %}

### Olemassaolevan rakennusten tai rakennelmien jakaminen eri rakennuskohteiksi

Rakennuskohteen toimenpide voi johtaa olemassaolevan, omalla pysyvällä rakennustunnuksella tunnistettavan rakennuksen tai rakennelman jakamiseen kahdeksi tai useammaksi rakennukseksi tai rakennelmaksi, joilla on kullakin oma pysyvä rakennustunnus. Alkuperäinen jaettava kohde voi olla yksi jäljelle jäävistä kohteista, tai sen elinkaari voi kokonaan päättyä.

{% include common/note.html content="Vaatinee ristiintarkitusta ja harmonisointia DVV:n (PRT) rakennustietojen elinkaaren tapahtumien kanssa" %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-jakamienn-kohde-ennen-jalkeen" %}
Jakamisen sisältävää muutosta kuvaavaan [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokan objektiin tulee yhdistää assosiaation ```kohdeEnnenMuutosta``` avulla siihen Rakennus- tai Rakennelma-luokan objektiin, joka kuvaa rakennusta tai rakennelmaa ennen sen jakamista. Samaan RakennuskohteenMuutos-luokan objektiin tulee yhdistää assosiaation ```kohdeMuutoksenJälkeen``` avulla sekä mahdollinen jäljelle jäävä että uutena luodut Rakennus- tai Rakennelma-luokan objektit.

Jakamisessa mahdollisesti jäljelle jäävän Rakennus- tai Rakennelma-luokan objektin tiedot sisältäen sen mahdolliset osittelut päivitetään vastaamaan uutta kokonaisuutta vastaavasti kuin rakennuksen tai rakennelman muutostoimenpiteen tapauksessa.
{% include common/clause_end.html %}

#### Rakennuskohteesta jaetaan osia eri rakennuskohteiksi

{% include common/clause_start.html type="req" id="elinkaari/vaat-kohteen-yhdistaminen-toiseen" %}
Kun [Rakennus](dokumentaatio/#rakennus)- tai [Rakennelma](dokumentaatio/#rakennelma)-luokan objekti jaetaan kahdeksi tai useammaksi Rakennus- tai Rakennelma-kohteeksi osana [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan kuvaamaa rakentamistoimenpidettä siten, että yksi alkuperäisistä rakennuksista tai rakennelmista jää jäljelle alkuperäistä pienempänä, tulee sekä alkuperäisen että uutena luotavien Rakennus- tai Rakennelma-kohteiden tiedot antaa siten, että ne kuvaavat uusia jaettuja rakennuksia tai rakennelmia. 

Jäljelle jäävän Rakennus- tai Rakennelma-luokan objektin attribuutin ```pysyväRakennusTunnus``` arvo säilyy muuttumattomana, samoin kuin sen ```identiteettiTunnus```-attribuutin arvo.  Uusille Rakennus- tai Rakennelma-luokkien objektille annetaan uudet attribuuttien ```pysyväRakennusTunnus```- ja ```identiteettiTunnus``` arvot.
{% include common/clause_end.html %}

#### Rakennuskohde korvataan eri rakennuskohteilla

{% include common/clause_start.html type="req" id="elinkaari/vaat-kohteen-yhdistaminen-toiseen" %}
Kun [Rakennus](dokumentaatio/#rakennus)- tai [Rakennelma](dokumentaatio/#rakennelma)-luokan objekti korvataan kahdella tai useammalla uudella Rakennus- tai Rakennelma-luokan objektilla osana [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan kuvaamaa rakentamistoimenpidettä ilman että alkuperäistä rakennuskohdetta puretaan, tulee uusien rakennuskohteiden tiedot antaa siten, että ne kuvaavat uusi jaettuja rakennuksia tai rakennelmia. 

Poistuvan, elinkaarensa päättävän Rakennus- tai Rakennelma-luokan objektin attribuutin attribuutin ```elinkaarenVaihe``` arvoksi tulee ```07 - yhdistetty tai jaettu```.  Uusille Rakennus- tai Rakennelma-luokkien objektille annetaan uudet attribuuttien ```pysyväRakennusTunnus```- ja ```identiteettiTunnus``` arvot.
{% include common/clause_end.html %}

### Monimutkaiset jakamis- ja yhdistämistoimenpiteet

Yhden rakentamistoimenpiteen avulla voidaan kuvata myös muutoksia, jotka sisältävät sekä olemassaolevien rakennuskohteiden jakamista erillisiksi rakennuskohteiksi että niiden yhdistämistä samoiksi rakennuskohteiksi. Esimerkiksi kaksi olemassaolevaa, toisiinsa kiinni rakennettua rakennusta muutetaan kolmeksi erilliseksi rakennukseksi siten, että toinen alkuperäisistä rakennuksista jää jäljelle samalla pysyvällä rakennustunnuksella, mutta osa sen tilasta siirtyy toiseen uusista rakennuksista. Toisen alkuperäisen rakennnuksen elinkaari päättyy muutokseen. Tuloksena luodaan kaksi uutta rakennusta, joista toiseen kuuluu tiloja molemmmista alkuperäisistä rakennuksista ja toiseen vain osa poistuvasta alkuperäisestä rakennuksesta.

{% include common/clause_start.html type="req" id="elinkaari/vaat-monimutkaiset-toimenpiteet" %}
Mikäli [RakentamiskohteenToimenpide](dokumentaatio/#rakentamiskohteentoimenpide)-luokan objektina kuvatussa muutoksessa tehdään sekä olemassa olevien rakennuskohteiden jakamista osiin että niiden yhdistämistä samoiksi rakennuskohteiksi, tulee kaikki muutostoimenpiteen piiriin kuuluvat olemassa olevat [Rakennuskohde](dokumentaatio/#rakennuskohde)-luokan objektit liittää [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokan objektiin assosiaation ```kohdeEnnenMuutosta``` avulla. Samaan RakennuskohteenMuutos-luokan objektiin tulee yhdistää assosiaation ```kohdeMuutoksenJälkeen``` avulla kaikki muutoksen jälkeen jäljelle jäävät tai uutena luodut Rakennuskohde-luokan objektit.

Kaikkien muutoksessa poistuvien, elinkaarensa päättävien Rakennus- ja Rakennelma-luokan objektien ```elinkaarenVaihe```-attribuuttien arvoksi tulee asettaa ```07 - yhdistetty tai jaettu```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-rakentaminen-ja-purkaminen-erikseen" %}
Mikäli samassa rakentamishankkeessa tehdään sekä uuden rakennuskohteen rakentamista tai olemassa olevan muuttamista että vanhan rakennuskohteen purkamista kokonaan tai osittain, tulee purkaminen kuvata eri [RakentamiskohteenToimenpide](dokumentaatio/#rakentamiskohteentoimenpide)-luokan objektin avulla kuin rakentaminen ja muuttaminen.
{% include common/clause_end.html %}

### Rakennelman korvaaminen rakennuksella

Entinen rakennelma voidaan korvata uudella rakennuksella rakentamistoimenpiteen seurauksena.

{% include common/clause_start.html type="req" id="elinkaari/vaat-rakennelman-muutos-rakennukseksi" %}
Kun rakennelma korvataan uudella rakennuksella osana [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan kuvaamaa rakentamistoimenpidettä, tulee luoda uusi [Rakennus](dokumentaatio/#rakennus)-luokan objekti. Uudelle Rakennus-objektille annetaan uudet attribuuttien ```pysyväRakennusTunnus```- ja ```identiteettiTunnus``` arvot. Poistuvan [Rakennelma](dokumentaatio/#rakennelma)-luokan objektin attribuutin ```elinkaarenVaihe``` arvoksi tulee ```08 - rakennelma korvattu rakennuksella```.

Poistuva Rakennelma-luokan objekti tulee yhdistää muutosta kuvaavaan [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokan objektiin assosiaation ```kohdeEnnenMuutosta``` avulla. Uusi Rakennus-luokan objekti tule yhdistää samaan RakennuskohteenMuutos-luokan objektiin assosiaation ```kohdeMuutoksenJälkeen``` avulla.
{% include common/clause_end.html %}

### Rakennuksen osittelujen lisäykset ja muutokset

[Rakennus](dokumentaatio/#rakennus) voidaan jakaa loogisiin tai fyysisiin osiin, joista kukin kuvataan [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektin avulla, ks. [Laatusäännöt, Rakennuksen osittelut](laatusaannot.html/#rakennuksenosittelut). [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokan kuvaamaan rakennuksen tietojen muutoksen yhteydessä rakennuksen osittelua voidaan muuttaa tai lisätä sille uusi osittelu. Osittelun lisääminen tai muuttaminen ei välttämättä liity rakentamis-, muutos-, korjaamis- tai laajennustoimenpiteeseen, vaan sen kirjaaminen Rakennuksen tietoihin voi olla tarpeen puhtaasti olemassa olevan rakennuksen tietojen täydentämiseksi.

### Huoneistotietojen muutokset

Rakennettujen tilojen ja huoneistojen tietoja voidaan muuttaa osana [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan avulla kuvattavaa rakennuksen tai sen osan rakentamistoimenpidettä. Suunnitellut tilojen ja huoneistojen tiedot  kuvataan osana suunnitelman mukaisia [Rakennus](dokumentaatio/#rakennus)- tai [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-objekteja, ks. vaatimus [elinkaari/vaat-suunniteltu-rakennuskohde](#elinkaari/vaat-suunniteltu-rakennuskohde). Toimenpiteen sisältämää suunniteltua muutosta kuvaavan [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokan attribuutti ```huoneistonMuutos``` sisältää uuden rakennetavan huoneiston, olemassaolevan huoneiston muutoksen tai huoneiston poiston tiedot.

[HuoneistonMuutos](dokumentaatio/#huoneistonmuutos)-luokka tarjoaa [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokkaa rajoitetumman linkityksen rakennuksen sisältämien huoneistojen muutoshistorian seuraamiseen, sillä siihen liitetään vain suunnitellun tai toteutuneen huoneiston tila (attribuutti ```muuttunutHuoneisto```), ei huoneiston tilaa ennen muutosta. Huoneiston aiempikin tila on kuitenkin saatavissa epäsuorasti, sillä Rakennus-luokan objektin muutosta edeltävä tila, sisältäen huoneistojen tiedot, löytyy RakennuskohteenMuutos-luokan ```kohdeEnnenMuutosta``` avulla.

{% include common/clause_start.html type="req" id="elinkaari/vaat-huoneisto-elinkaaren-vaiheen-sallitut-muutokset" %}
[Huoneisto](dokumentaatio/#huoneisto)-luokan objektien ```elinkaarenVaihe``` arvot voivat muuttua [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan kuvaamana vain seuraavasti:

* Arvosta ```1 - Suunnitteilla``` arvoihin ```2 - Muuttovalmis```, ```3 - Käytössä``` tai ```4 - Muuttokiellossa```.
* Arvosta ```2 - Muuttovalmis``` arvoihin ```3 - Käytössä```, ```4 - Muuttokiellossa```, ```5 - Purettu```, ```6 - Tuhoutunut```, ```7 - Poistettu``` tai ```8 - Yhdistetty tai jaettu```.
* Arvosta ```3 - Käytössä``` arvoihin ```4 - Muuttokiellossa```, ```5 - Purettu```, ```6 - Tuhoutunut```, ```7 - Poistettu``` tai ```8 - Yhdistetty tai jaettu```.
* Arvosta ```4 - Muuttokiellossa``` arvoihin ```2 - Muuttovalmis```, ```3 - Käytössä```, ```5 - Purettu```, ```6 - Tuhoutunut```, ```7 - Poistettu``` tai ```8 - Yhdistetty tai jaettu```.
* Arvoista ```5 - Purettu```, ```6 - Tuhoutunut```, ```7 - Poistettu``` ja ```8 - Yhdistetty tai jaettu``` ei ole sallittuja siirtymiä.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-huoneiston-varusteiden-muutokset" %}
Huoneistoon sen muutostoimenpiteen johdosta lisättävät ja poistuvat varusteet kuvataan  [HuoneistonMuutos](dokumentaatio/#huoneistonmuutos)-luokan Luokan [HuoneistonVaruste](dokumentaatio/#huoneistonvaruste) mukaisen rakenteisen attribuutin ```varustemuutos``` avulla. Lisättävien varusteiden osalta käytetään attribuutin ```kuuluuKohteeseen``` arvoa ```true```, ja poistuvien varusteen osalta arvoa ```false```.
{% include common/clause_end.html %}

### Hissien ja sisäänkäyntien muutokset

[Rakennus](dokumentaatio/#rakennus)-luokan objektiin voi liittyä nolla tai useampia [Hissi](dokumentaatio/#hissi)- ja [Sisäänkäynti](dokumentaatio/#sisäänkäynti)-luokan objekteja. Assosiaation tyyppi on kompositio, joten hissit ja sisäänkäynnit kuuluvat elinkaarensa aikana vain yhteen rakennukseen, eivätkä ne voi olla olemassa, jos rakennus lakkaa olemasta. Tietomallissa hissillä tarkoitetaan siis juuri tiettyyn rakennukseen rakennettua hissiä, jota ei voida siirtää toiseen rakennukseen, ei tiettyä hissikoneistoa. Vastaavasti sisäänkäynnillä tarkoitetaan tietyn rakennuksen ovean tai aukkoa, josta on kulku kohteeseen sen ulkopuolelta, ei tiettyä fyysistä ovea tai sen rakenteita.

{% include common/clause_start.html type="req" id="elinkaari/vaat-hissi-sisaankaynti-elinkaaren-vaiheen-sallitut-muutokset" %}
[Hissi](dokumentaatio/#hissi)- ja [Sisäänkäynti](dokumentaatio/#sisäänkäynti)-luokan objektien ```elinkaarenVaihe```-attribuuttien arvot voivat muuttua [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan kuvaamana vain seuraavasti:

* Arvosta ```1 - Suunnitteilla``` arvoihin ```2 - Käytössä```, ```3 - Tilapäisesti pois käytöstä``` tai ```5 - Poistettu```.
* Arvosta ```2 - Käytössä``` arvoihin ```3 - Tilapäisesti pois käytöstä```, ```4 - Poistettu käytöstä```, ```5 - Poistettu``` tai ```6 - Purettu```.
* Arvosta ```3 - Tilapäisesti pois käytöstä``` arvoihin ```2 - Käytössä```, ```4 - Poistettu käytöstä```, ```5 - Poistettu``` tai ```6 - Purettu```.
* Arvosta ```4 - Poistettu käytöstä``` arvoihin ```2 - Käytössä```, ```3 - Tilapäisesti pois käytöstä```, ```5 - Poistettu``` tai ```6 - Purettu```.
* Arvoista ```5 - Poistettu``` ja ```6 - Purettu``` ei ole sallittuja siirtymiä.
{% include common/clause_end.html %}


{% include common/clause_start.html type="req" id="elinkaari/vaat-hissin-sisaankaynnin-ja-rakennuksen-elinkaaret" %}
Mikäli [Rakennus](dokumentaatio)-luokan objektin ```elinkaarenVaihe```-attribuutin arvo muuttuu alla esitettyihin tiloihin, on myös siihen mahdollisesti liitettyjen [Hissi](dokumentaatio/#hissi)- ja [Sisäänkäynti](dokumentaatio/#sisäänkäynti)-luokan objektien ```elinkaarenVaihe```-attribuuttien muututtava seuraavasti:

| Rakennuksen elinkaarenVaihe         | Hissin tai Sisäänkäynnin elinkaarenVaihe      |
|-------------------------------------|-----------------------------------------------|
| ```05 - tuhoutunut```               | ```5 - Poistettu``` *                        |
| ```06 - purettu```                  | ```6 - Purettu``` *                          |
| ```07 - yhdistetty tai jaettu```    | ```5 - Poistettu``` *                        |

*) ellei ```elinkaarenVaihe``` ole jo ennestään joko ```5 - Poistettu``` tai ```6 - Purettu```.

Mikäli [Rakennus](dokumentaatio)-luokan objektin ```elinkaarenVaihe```-attribuutin arvo on ```01 - suunnitteilla```, siihen mahdollisesti liitettyjen [Hissi](dokumentaatio/#hissi)- ja [Sisäänkäynti](dokumentaatio/#sisäänkäynti)-luokan objektien ```elinkaarenVaihe```-attribuuttien arvojen on oltava ```1 - Suunnitteilla```.

[Hissi](dokumentaatio/#hissi)- ja [Sisäänkäynti](dokumentaatio/#sisäänkäynti)-luokan objektien ```elinkaarenVaihe```-attribuuttien muutokset eivät vaadi muutoksia niihin liittyviin [Rakennus](dokumentaatio/#rakennus)-luokan objekteihin.
{% include common/clause_end.html %}

### Rakennuskohteen purkaminen kokonaan tai osittain

Purettaessa Rakennus tai Rakennelma osittain, muutetaan purettavan osan elinkaaren vaiheeksi *purettu*. Purettavan osan kuvaava RakennuksenOsa tai RakennelmanOsa muodostetaan tarvittaessa purkamistoimenpiteen kuvauksen yhteydessä. 

{% include common/clause_start.html type="req" id="elinkaari/vaat-kohteen-purkamistoimenpide" %}
Rakennuksen tai rakennelman tai niiden uusien osien suunniteltu purkaminen kuvataan luokan [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide) objektina, jonka attribuutilla ```toimenpiteenLaji``` on koodiston [RakentamistoimenpiteenLaji](dokumentaatio/#rakentamistoimenpiteenlaji) arvo ```05 - Purkaminen``` tai ```08 - Rakennuksen osittainen purkaminen```.

Attribuutin ```purkamisenSyy``` avulla voidaan kuvata, miksi purkaminen tehdään. Atttribuuteille ```perusparannus``` ja ```korjausaste``` ei saa antaa arvoja.

Mikäli purkamistoimenpiteen kuvaava [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan objekti liittyy sen ```suunniteltuMuutos```-attribuutin ja edelleen sen ```kohdeEnnenMuutosta```-assosiaation kautta luokkien [Rakennus](dokumentaatio/#rakennus), [RakennuksenOsa](dokumentaatio/#rakennuksenosa),  [Rakennelma](dokumentaatio/#rakennelma), tai [RakennelmanOsa](dokumentaatio/#rakennelmanosa) objekteihin, tulee näiden objektien ```elinkaarenVaihe```-attribuutin arvojen olla jokin seuraavista: ```02 - rakenteilla```, ```03 - käytössä``` tai ```04 - käyttökiellossa/käyttökelvoton``` tai ```05 - tuhoutunut```. Saman ```suunniteltuMuutos```-attribuutin sisältämän ```kohdeMuutoksenJälkeen```-assosiaatiolla viitattavan [Rakennus](dokumentaatio/#rakennus)-, [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-,  [Rakennelma](dokumentaatio/#rakennelma)-, tai [RakennelmanOsa](dokumentaatio/#rakennelmanosa)-luokkien objektien ```elinkaarenVaihe```-attribuuttien arvojen tulee olla ```06 - purettu```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-osittainen-purkaminen-rakennuksen-osat" %}
Mikäli rakennus puretaan osittain, on purettava osa mahdollisuuksien mukaan kuvattava omana [RakennuksenOsa](dokumentaatio/#rakennuksenosa)-luokan objektinaan, joka on liitetty siihen [Rakennus](dokumentaatio/#rakennnus)-luokan objektiin, jonka osaan purkaminen kohdistuu, käyttäen [RakennuksenOsittelu](dokumentaatio/#rakennuksenosittelu)-luokan attribuutin ```osittelunPeruste``` arvoa ```2 - Rakentamishistoriaan perustuva osittelu```. Tälläinen osittelu ja purettavaa osaa kuvaava RakennuksenOsa-luokan objekti kuvataan [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan objektin ```suunniteltuMuutos```-attribuutin ja edelleen sen ```kohdeMuutoksenJälkeen```-assosiaatiolla liitettävässä Rakennus-luokan objektin ```osittelu```-attribuutin arvona.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-osittainen-purkaminen-rakennelman-osat" %}
Mikäli rakennelma puretaan osittain, on purettava osa mahdollisuuksien mukaan kuvattava omana [RakennelmanOsa](dokumentaatio/#rakennelmanosa)-luokan objektinaan, joka on liitetty siihen [Rakennelma](dokumentaatio/#rakennelma)-luokan objektiin, jonka osaan purkaminen kohdistuu. Tälläinen purettavaa osaa kuvaava RakennelmanOsa-luokan objekti kuvataan [RakennuskohteenToimenpide](dokumentaatio/#rakennuskohteentoimenpide)-luokan objektin ```suunniteltuMuutos```-attribuutin ja edelleen sen ```kohdeMuutoksenJälkeen```-assosiaatiolla liitettävän Rakennelma-luokan objektin ```osa```-assosiaation avulla.
{% include common/clause_end.html %}

## Tietojen päivittäminen ilman toimenpiteitä

Tietomallissa ei ole määritelty omaa luokkaa rakennuskohteen tietosisältöä täydentäville tai korjaaville tietopäivityksille, johoin ei liity rakennuskohteiden muutostoimenpiteitä, koska tällaisten tietopäivitysten kuvailutietojen siirtämiseen eri tietojärjestelmien välillä ei nähdä harmonisointitarvetta. Järjestelmäkohtaisissa tietomalleissa voidaan kuitenkin käyttää [RakennuskohteenMuutos](dokumentaatio/#rakennuskohteenmuutos)-luokan mukaista rakennetta päivityksen varsinaisen muutostietosisällön kuvaamiseen vastaavasti kuin [Rakentamistoimenpide](dokumentaatio/#rakentamistoimenpide)-luokan ```suunniteltuMuutos```-attribuutissa.



