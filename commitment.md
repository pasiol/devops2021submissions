## Tietokannan valinta projektia varten

Valinta on Postgres, koska tehtävien tekemiseen on käytettävissä rajallisesti aikaan. Osassa 2 backendiin valittiin tietokantayhteyttä varten gorm-kirjasto, jonka avulla tietokannan vaihtaminen on helppoa, mutta gorm ei tue Google Cloud SQL:ää. Tietokannan vaihdoksen takia pitäisi tietokantaa käsittelevät osat kirjoittaa uusiksi. Helpompi olisi valita Postgres-palvelu Googlen tarjonnasta, jos haluisia hyödyntää DbaaS-palvelua.

https://gorm.io/docs/connecting_to_the_database.html

## Commitment

The choice is Postgres because of the limited time available to complete exercises. In Part 2, a gorm library was selected for the database connection for the backend, making it easy to switch databases, but gorm does not support Google Cloud SQL. Due to the change in the database, the sections dealing with the database should be rewritten. It would be easier to choose Postgres from Google if you want to take advantage of DbaaS.

https://gorm.io/docs/connecting_to_the_database.html
