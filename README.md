# network-manager-userguide

To repozytorium zawiera plik docker-compose.yml oraz podręcznik użytkownika aplikacji NetworkManager.

## Proces budowania obrazu

# network-manager-userguide

To repozytorium zawiera plik docker-compose.yml oraz podręcznik użytkownika aplikacji NetworkManager.

## Proces budowania obrazu


Aplikacja jest uruchamiana jako obraz Docker'a. Poniżej lista w jaki sposób zbudować i uruchomić własny obraz ze źródeł.


* Skompilować źródła aplikacji internetowej (Github: network-manager): 
     ```npm run build```

* Przenieść skompilowane źródła aplikacji internetowej do folderu części serwerowej: ```/src/main/resources/static/```

* Stworzyć artefakt części serwerowej (Github: networkManager): ```gradle bootJar```

* Wykonać komendę budującą obraz: ```docker build -t ayloro/network-manager-server .```

* Uruchomić bazę danych oraz aplikację poprzez wykonanie komendy w folderze z plikiem \textit{docker-compose.yml}: ```docker-compose up --build```

* Po pierwszym uruchomieniu bazy danych należy udać się na stronę bazy danych(localhost:7474 lub o innym adresie np. dla Windows: 192.168.99.100:7474), aby utworzyć nowego użytkownika potrzebnego aplikacji. Aplikacja domyślnie spróbuje się połączyć za pomocą użytkownika: __networkManager__ i hasła: __appPassword__. Zmienić to można w pliku konfiguracyjnym:  ```/src/main/resources/application.yml``` Taka zmiana wymagała będzie ponownego zbudowania artefaktu części serwerowej oraz zbudowania obrazu.


