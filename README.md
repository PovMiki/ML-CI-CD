Zadanie 1: Przygotowanie repozytorium z przykładowym modelem ML i testami jednostkowymi  

<img width="580" height="713" alt="image" src="https://github.com/user-attachments/assets/a35fd79b-b591-4cd0-a096-7cb3717bb570" />

Zaimplementowałem za pomocą FastAPI TestClient i pytest testy jednostkowe które używają HTTP bez konieczności uruchamiania Uvicorna

Testy dotyczyły : 
- weryfikacji czy serwer zwraca status 200 po wysłaniu ciała JSON z hours : 5.0. Plik JSON ma być parsowany aby upewnić się że klucz predicted_score istnieje i nie zwraca pustej wartości None
- sprawdzenie odporności API na zapytania sekwencyjne oraz walidacja typowania zmiennych (wysyłanie różnych wartości godzin)
- test walidacji i obsługi błędów (symulowanie wstrzyknięcia -1.0 godziny)
- test dokładności matematycznej modelu ML

Zadanie 2 : Konfiguracja GitHub Actions do automatycznego testowania

<img width="388" height="639" alt="image" src="https://github.com/user-attachments/assets/b46c163d-c186-490d-92be-ff62d4a045ae" />

Projekt reague na zdarzenie push, które automatycznie się uruchamia po nowych zmianach oraz pull_request po prośbie o dołączenie zmian na main

środowisko uruchomieniowe runs-on wykonuje się w ubuntu-latest

Maszyna wykonuje sekwencje steps : 
- kolonowanie kodu 
- inicjalizacja interpretera python
- aktualizacja pip i bibliotek z requirements
- wywołanie polecenia pytest test_main.py

<img width="855" height="294" alt="image" src="https://github.com/user-attachments/assets/a15daa78-4ad1-49a1-8e60-dd5c2da61bda" />

Poprawność wdrożenia CI została zweryfikowana w Actions ponieważ system zainicjalizował wirtualną maszynę, pobrał kod, zainstalował zależności i wykonał testy które zakończyły się powodzeniem

Zadanie 3 : Automatyczne budowanie obrazu Dockera i jego publikacja

<img width="602" height="709" alt="image" src="https://github.com/user-attachments/assets/6a368207-4475-4d9c-af33-6ff748603c3b" />

- on : push to wyzwalacz który uruchamia się po zmianie na main
- permissions wymuszają na maszynie wirtualnej uprawnienia write
- log in to Github lologuje się do ghcr.io
- build and push Dokcer kompiluje dokcerfile i wypycha kontener do chmury

**Wnioski :**

Laboratorium nauczyło jak wykorzystywać automatyzację CI/CD za pomocą Actions na githubie, co stabilizuje kod oraz pilnuje poprawności działania modelu przy każdych zmianach. Testy jednostkowe w pytest automatycznie pilnują czy margines błędu regresji jest w limicie. 

