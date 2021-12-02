### Tietokanta palveluna vs itse ylläpidettynä

Tietokanta palveluna on kehittäjälle helppo ratkaisua. Tällöin ylläpitoon liittyvät tehtävät jää pois ja ne kuuluvat palvelun hintaan. Organisaatio tarvitsee vähemmän resursseja tietokannan ylläpitoon ja varmuuskopiointiin itse ylläpidetyissä tietokannoissa.

Mikäli ei tarvita jatkuvaa seurantaa esim. kehitysympäristössä voi tietokantaa ajaa itse ylläpidettävässä kontissa esim. kehittäjän koneella, mutta tuotantokäyttöön tällainen ratkaisu harvemmin soveltuu. Joissakin Iot-ratkaisuissa voi olla järkevää ajaa omaa tietokantapalvelua paikallisesti esim. verkkohäiriöiden varalta, jolloin data saadaan tallennettua myös verkkohäiriöiden aikana.

Kustannuksiltaan palvelu on edullisempi, jos työlle lasketaan hinta. Käytännössä alle 100e kuukaudessa on saatavilla useita kohtuullisen tehokkaita tuotantokäyttöön soveltuvia palveluita, jotka soveltuvat esim. keskisuurten sivustojen tietokantaratkaisuiksi. Usein näissä palveluissa tietokanta on clusteroitu, mitä ainakaan ei voi totetuttaa halvemmalla on prem-ympäristössä. Myös pavelun maantieteellinen hajauttaminen on mahdollista, mikä onkin välttämätöntä kansainvälisissä palveluissa. Periaatteessa palvelun voisi rakentaa esim. kubernetes-ympäristöön, mutta se on kalliimpi ja alttiimpi teknisesti ongelmille ja monimutkaisesti kuin palveluna tarjottava ratkaisu.

Palvelu tulisi kuitenkin valita siten, että palvelun tarjoajan vaihtaminen on jatkossa mahdollista, mahdollisimman pienin kustannuksin, mikäli ei ole teknisiä rajoitteita, jotka pakottavat käyttämään tiettyä tietokantaa. SQL on tässä suhteessa turvallisempi ratkaisu kuin NoSQL-pohjaiset tietokannat, joissa tietokannan huomattavasti enemmän ohjelmistosidonnaista kuin SQL-kannoissa.

Plussat:
- kustannustehokkuus
- soveltuu erinomaisesti organisaatioille, joilla on käytössä niukasti resursseja tietokannan ylläpitoon ja hallinnointiin
- nopeuttaa kehittämistä
- tietokantojen ominaisuudet ja niihin liittyvät oheispalvelut kehittyvät nopeammin
- palvelun saatavuus ja latenssi on hyvä
- palvelua voi tarvittaessa hajauttaa usealle mantereelle
- skaalautuvuus ruuhka-aikoina, ei tarvitse maksaa koko vuotta "Black Fridayn-kapasiteetista"
- organisaatio voi keskittää resurssit kehittämiseen ylläpitämisen sijasta
- mahdollistaa PaaS-tyyppisten palveluiden rakentamisen, jolloin sovelluksen kehittäminen voidaan pitää omissa käsissä, vaikka kehittäminen ulkoistettaisiin. Datan hallinta säilyy organisaatiolla. Saas ratkaisussa organisaatio on enemmän yhden ohjelmistotoimittajan varassa ja datan hallinta ei ole enää kokonaan organisaation omissa käsissä.
- integrointi kolmannen osapuolen palveluihin on helpompaa, esim. koneoppiminen, lokipalvelut jne.

Miinukset
- lainsäädäntö ja säädökset voivat estää tiedon siirtämisen julkiseen pilveen esim. arkaluonteisten tietojen osalta
- hinnoittelu voi olla monimutkaista
- palveluiden mitoittaminen oikein voi olla haasteellisesta ainakin monipilviympäristöissä
- vendor locking
- verkkoinfrastruktuurin on oltava hyvä (koskee myös sähköverkkoa)
- huomioitava organisaation toiminnan kannalta myös poikkeusolosuhteet, jossa esim. Internetin ja sähköverkon toiminta estyy osittain tai kokonaan

### DBaaS vs DIY

A database as a service is an easy solution for a developer. In this case, the tasks related to maintenance are omitted and are included in the price of the service. An organization needs fewer resources to maintain and back up its database on self-maintained databases.

If continuous monitoring is not required, eg in a development environment, the database can be run in a self-maintained container, eg on the developer's machine, but such a solution is less suitable for production use. In some IoT solutions, it may make sense to run your own database service locally, for example in the event of a network disruption, so that data can also be stored during a network disruption.

The cost of the service is cheaper if a price is calculated for the work. In practice, in a period of less than 100e per month, a number of reasonably efficient services suitable for production use are available, which are suitable, for example, for database solutions for medium-sized websites. Often in these services, the database is clustered, which at least cannot be found cheaper in the Prem environment. Geographical decentralization of the service is also possible, which is essential in international services. In principle, the service could be built in a kubernetes environment, for example, but it is more expensive and more prone to technical problems and complexity than the solution offered as a service.

However, the service should be chosen in such a way that it is possible to change service provider in the future, at the lowest possible cost, provided that there are no technical constraints on the use of a particular database. SQL is a more secure solution in this regard than NoSQL-based databases, where the database is significantly more software-dependent than SQL databases.

Pros:
- cost-effectiveness
- Ideal for organizations with limited resources for database maintenance and management
- accelerate development
- the capabilities of databases and related ancillary services are evolving faster
- service availability and latency are good
- the service can be spread over several continents if necessary
- scalability during peak hours, no need to pay for "Black Friday capacity" all year round
- the organization can focus resources on development rather than maintenance
- enables the construction of PaaS-type services, so that the development of the application can be kept in their own hands, even if the development is outsourced. Data management remains with the organization. In a solution, the organization is more dependent on a single software vendor, and data management is no longer entirely in the organization's own hands.
- integration with third party services is easier, eg machine learning, log services, etc.

Cons
- Legislation and regulations can prevent the transfer of information to the public cloud, for example for sensitive information
- Pricing can be complicated
- Proper sizing of services can be challenging, at least in multi-cloud environments
- vendor locking
- the network infrastructure must be good (also applies to the electricity network)
- take into account, from the point of view of the organisation's operations, exceptional circumstances in which, for example, the operation of the Internet and the electricity network is partially or completely blocked;
Lisätietoja tästä lähdetekstistäLähdeteksti vaaditaan käännöksen lisätietoihin
Lähetä palautetta
Sivupaneelit
