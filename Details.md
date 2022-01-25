## Java EE:n asennus palvelimelle

Yritimme asentaa Java EE:n, mutta valitettavasti emme päässeet haluttuun lopputulokseen, koska netissä olevat ohjeet olivat vanhentuneita. 

Laitoimme `sudo add-apt-repository ppa:webupd8team/java` -komennon. Tämän jälkeen teimme `sudo apt update` -komennon. Tämän jälkeen laitoimme `sudo apt install oracle-java11-installer` -komennon, joka johti virheilmoitukseen: "paketti on vanhentunut". Yritimmme myös noudattaa toista ohjetta, mutta päädyimme samaan ongelmaan. 

Tämän jälkeen käytimme stackoverflow:ssa olevaa ohjetta ja menimme `sudoedit /etc/apt/sources.list` -komennolla muokkaamaan sources.list -tiedostoa. Tiedostosta ei löytynyt packages.ros.org/ros/ -tiedostoa. Päätimme edetä seuraavaan vaiheeseen, koska emme saaneet asennettua javaa.
