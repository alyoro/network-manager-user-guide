# network-manager-user-guide

To repozytorium zawiera plik docker-compose.yml oraz podręcznik użytkownika aplikacji NetworkManager.

## Proste uruchomienie

Jeżeli na serwerze jest zainstalowany oraz uruchomiony docker deamon to aplikację uuruchamiamy:

```docker-compose up --build``` w folderze z plikiem *docker-compose.yml*

[WAŻNE Po pierwszym uruchomieniu link](#Po-pierwszym-uruchomieniu)

## Proces budowania obrazu

Aplikacja jest uruchamiana jako obraz Docker'a. Poniżej lista w jaki sposób zbudować i uruchomić własny obraz ze źródeł.


* Skompilować źródła aplikacji internetowej (Github: network-manager): 
     ```npm run build```

* Przenieść skompilowane źródła aplikacji internetowej do folderu części serwerowej: ```/src/main/resources/static/```

* Stworzyć artefakt części serwerowej (Github: networkManager): ```gradle bootJar```

* Wykonać komendę budującą obraz (. jeśli w folderze z artefaktem /build/libs/): ```docker build -t ayloro/network-manager-server .```

* Uruchomić bazę danych oraz aplikację poprzez wykonanie komendy w folderze z plikiem *docker-compose.yml*: ```docker-compose up --build```

### Po pierwszym uruchomieniu

* Po pierwszym uruchomieniu bazy danych należy udać się na stronę bazy danych(localhost:7474 lub o innym adresie np. dla Windows: 192.168.99.100:7474), aby utworzyć nowego użytkownika potrzebnego aplikacji. Aplikacja domyślnie spróbuje się połączyć za pomocą użytkownika: __networkManager__ i hasła: __appPassword__. Zmienić to można w pliku konfiguracyjnym:  ```/src/main/resources/application.yml``` Taka zmiana wymagała będzie ponownego zbudowania artefaktu części serwerowej oraz zbudowania obrazu.

Do poprawnego działania aplikacji wymagane jest stworzenie kilku węzłów w bazie danych:

* Tworzenie węzła do przechowywania prędkości portów
```create (n:PortSpeed {names: ['Ethernet1Gb','Ethernet10Gb']})```

* Tworzenie węzła do przechowywania VLAN
```create (n:Vlans {names: ['vlan1','vlan2','vlan3']})```

* Po utworzeniu pierwszego urządzenia należy dodać constraint który zagwaratuje unikalność urzadzeń pod względem identyfikatora
```CREATE CONSTRAINT ON (d:DeviceNode) ASSERT d.identifier IS UNIQUE```




