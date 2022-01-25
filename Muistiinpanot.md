# Muistiinpanot

### 1. Vaihe
- [ ] Java EE
- [x] JRE 
- [x] SDK

Kirjuduimme sisään Puttyn avulla opettajan luomalle palvelimelle. Javaa ei löytynyt oletuksena palvelimelta, joten lähdimme asentamaan Javaa `sudo apt install default-jdk` -komennolla. Tämän jälkeen tuli ilmoitus, että se on jo manuaalisesti asennettu. Laitettuamme komennon `java --version` komentorivi näytti, että JRE ja JDK löytyvät. Ohessa kuva komentoriviltä:

![unknown](https://user-images.githubusercontent.com/77921212/150959410-e77ee360-18cc-4142-a6fe-c674796a66f0.png)




<br />
<br />

### 2. Vaihe (lähde: https://www.vultr.com/docs/install-the-postgis-extension-for-postgresql-on-ubuntu-linux/) 
- [x] POSTGIS

`$ sudo apt -y install gnupg2` -komennolla lähdimme asentamaan Gnu Privacy Guard Dependecy -riippuvuutta. Tämän jälkeen importoitiin PGP signing key komennolla `$ wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -` -komennolla. Viimeiseksi lisäsimme PostgreSQL apt -repositorion komennolla ```$ echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list```

Seuraavaksi lähdimme asentamaan postgresql:n komennolla `$ sudo apt -y install postgresql-12 postgresql-client-12`. Sitten asensimme PostGIS:n komennolla `$ sudo apt install postgis postgresql-12-postgis-3`. Lopuksi asensimme vielä tarvittavat paketit komennolla: ```$ sudo apt-get install postgresql-12-postgis-3-scripts```. 

Tämän jälkeen kirjauduimme superkäyttäjälle komennolla `sudo su - postgres`. Seuraavaksi loimme uuden käyttäjän komennolla `createuser cgiuser1`. Sitten asetimme salasanan komennolla `$ psql -c "alter user exampleuser with password 'yourPassword'`. Tämän jälkeen lähdimme luomaan uutta tietokantaa komennolla `$ createdb my_db -O exampleuser`. 

Loimme vielä yhteyden uuteen tietokantaan komennolla: `$ psql -d cgi_db`. Pääsimme onnistuneesti sisään tietokantaan. Sitten lisäsimme PostGIS laajennuksen tietokantaan komennolla: ```my_db=# CREATE EXTENSION postgis;```

Tarkistimme lopuksi onko POSTGIS asentunut onnistuneesti komennolla: `my_db=# SELECT PostGIS_version();`. 

![fdab4154-07ba-46dc-833f-660c90b0cfaf](https://user-images.githubusercontent.com/77921212/150959632-dc90b6ff-88b9-465d-9efa-95ee3e6e3c95.jpg)



<br />
<br />


### 3. Vaihe (http://geoserver.org/release/stable/ ja https://medium.com/random-gis-talks/installing-geoserver-binary%EF%B8%8F-on-ubuntu-18-04-using-terminal-ff9429ab47fa)
- [x] Geoserver

Käytimme `wget`-komentoa zip paketin hakemiseen komennolla: `wget https://sourceforge.net/projects/geoserver/files/GeoServer/2.20.2/geoserver-2.20.2-bin.zip`. Tämä löytyi geoserver-sivuston "Packages Platform Independent Binary" -kohdasta. Ennen zip-kansion purkamista asensimme `unzip`-työkalun komennolla `sudo apt install unzip`. Tämän jälkeen purimme `geoserver`-kansion `unzip geoserver-2.20.2-bin.zip` -komennolla. `echo "export GEOSERVER_HOME=/usr/share/geoserver" >> ~/.profile. ~/.profile` -komennolla asensimme muuttujan, jolla  saimme GeoServerin käytettäväksi.

Muutimme oikeuksia, jotta käyttäjälle tulee oikeudet tiedostoon: `sudo chown -R USER_NAME /usr/share/geoserver/`. Tämän jälkeen käynnistimme geoserverin komennolla `sh startup.sh`. 

![unknown](https://user-images.githubusercontent.com/77921212/150963741-37153174-41f2-4549-a8e1-f9a7e5be7071.png)






