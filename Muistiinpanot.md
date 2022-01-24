# Muistiinpanot

1. Vaihe: Java, JRE, SDK

Kirjuduimme sisään Puttyn avulla opettajan luomalle palvelimelle. Javaa ei löytynyt oletuksena palvelimelta, joten lähdimme asentamaan Javaaa `sudo apt install default-jdk ` -komennolla. Tämän jälkeen tuli ilmoitus, että se on jo manuaalisesti asennettu. Seuraavaksi laitoimme `sudo add-apt-repository ppa:webupd8team/java` -komennon. Tämän jälkeen teimme `sudo apt update` -komennon. Tämän jälkeen laitoimme `sudo apt install oracle-java11-installer` -komennon, joka johti virheilmoitukseen: "paketti on vanhentunut". Yritimmme myös noudattaa toista ohjetta, mutta päädyimme samaan ongelmaan. 

Tämän jälkeen käytimme stackoverflow:ssa olevaa ohjetta ja menimme `sudoedit /etc/apt/sources.list` -komennolla muokkaamaan sources.list -tiedostoa. Tiedostosta ei löytynyt packages.ros.org/ros/ -tiedostoa. Päätimme edetä seuraavaan vaiheeseen, koska emme saaneet asennettua javaa.




2. Vaihe: POSTGIS (lähde: https://www.vultr.com/docs/install-the-postgis-extension-for-postgresql-on-ubuntu-linux/) 

`$ sudo apt -y install gnupg2` -komennolla lähdimme asentamaan Gnu Privacy Guard Dependecy -riippuvuutta. Tämän jälkeen importointiin PGP signing key komennolla `$ wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -` -komennolla. Tämän jälkeen lisäsimme `$ echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list` -komennolla PGP signing key -avaimen. Viimeiseksi lisäsimme PostgreSQL apt -repositorion komennolla `$ echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list`

Seuraavaksi asensimme postgresql:n komennolla `$ sudo apt -y install postgresql-12 postgresql-client-12`. Seuraavaksi asensimme PostGIS:n komennolla `$ sudo apt install postgis postgresql-12-postgis-3`. Lopuksi asensimme vielä tarvittavat paketit komennolla: ´$ sudo apt-get install postgresql-12-postgis-3-scripts`. 

Tämän jälkeen kirjauduimme superkäyttäjälle komennolla `sudo su - postgres`. Tämän jälkeen loimme uuden käyttäjän komennolla `createuser cgiuser1`. Tämän jälkeen asetimme salasanan komennolla `$ psql -c "alter user exampleuser with password 'yourPassword'`. Tämän jälkeen lähdimme luomaan uutta tietokantaa komennolla `$ createdb my_db -O exampleuser`. 

Sitten loimme yhteyden uuteen tietokantaan komennolla: `$ psql -d cgi_db`. Pääsimme onnistuneesti sisään tietokantaan. Sitten lisäsimme PostGIS laajennuksen tietokantaan komennolla: `my_db=# CREATE EXTENSION postgis;`

Kokeilimme lopuksi PostGIS laajennusta komennolla: `my_db=# SELECT PostGIS_version();`. 






3. Vaihe (http://geoserver.org/release/stable/ ja https://medium.com/random-gis-talks/installing-geoserver-binary%EF%B8%8F-on-ubuntu-18-04-using-terminal-ff9429ab47fa)

Käytimme wget komentoa zip paketin hakemiseen: `wget https://sourceforge.net/projects/geoserver/files/GeoServer/2.20.2/geoserver-2.20.2-bin.zip`. Tämä löytyi geoserverin Packages Platform Independent Binary -kohdasta. Tämän jälkeen purimme paketin `unzip geoserver-2.20.2-bin.zip` -komennolla. `echo "export GEOSERVER_HOME=/usr/share/geoserver" >> ~/.profile. ~/.profile` -komennolla asensimme muuuttujan, jolla yritimme saada GeoServerin käytettäväksi. Tämä ei kuitenkaan onnistunut, koska tarvittavaa muuttujaa ei löytynyt.

Toimme `/user/share` -hakemistoon uudestaan zip tiedosto aikaisemmalla wget-komennolla. Sittem purimme paketin `unzip geoserver-2.20.2-bin.zip` -komennolla. Tämän jälkeen käytimme `echo "export GEOSERVER_HOME=/usr/share/geoserver" >> ~/.profile. ~/.profile` -komentoa, jonka jälkeen muutimme oikeuksia, jotta käyttäjälle tulee oikeudet tiedostoon: `sudo chown -R USER_NAME /usr/share/geoserver/`. Tämän jälkeen käynnistimme geoserverin komennolla `sh startup.sh`. 







