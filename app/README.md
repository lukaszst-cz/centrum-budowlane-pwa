# Centrum Budowlane | Operacje

Responsywna aplikacja **Progressive Web App (PWA)** dla zintegrowanego centrum budowlanego. Model obejmuje hurtownię budowlaną, hurtownię elektryczną, tartak, transport HDS, relacje z inwestorami, zamówienia, zakupy, magazyny, płace, finanse i ryzyka.

**Status: działający prototyp funkcjonalny (local-first) na danych symulacyjnych.** Ten kod **nie jest jeszcze produkcyjnym wielostanowiskowym ERP**. Przełącznik ról służy prezentacji uprawnień w interfejsie, nie zastępuje autoryzacji po stronie serwera.

## Uruchomienie

Najprościej otworzyć plik `podglad.html` w przeglądarce. To samodzielny podgląd, który nie wymaga instalacji zależności. Zawiera całą logikę i oprawę graficzną, lecz nie instaluje się jako PWA z protokołu `file://`.

Aby korzystać z instalowalnego PWA, uruchom lokalny serwer statyczny w katalogu projektu:

```bash
python -m http.server 8080
```

Następnie wejdź na `http://localhost:8080`. Przeglądarka obsługująca PWA może zaoferować opcję instalacji. Na serwerze internetowym użyj HTTPS. Nie trzeba uruchamiać Node.js ani instalować pakietów npm.

## Moduły

| Moduł | Działające operacje |
|---|---|
| Pulpit | Metryki sprzedaży i kosztów, alerty, rejestr zamówień, marże działów |
| Zamówienia | Dodawanie wielopozycyjnych zamówień, wycena, rabaty, kontrola marży, limitu i stanów, statusy, CSV |
| Inwestorzy | Kartoteki inwestorów i budów, etapy, limity kredytowe, należności, terminy, zaliczki, retencje |
| Magazyny | Kartoteki towarowe, stany, rezerwacje, PZ/WZ, ruchy, kontrola braku stanu |
| Zakupy | Dostawcy, zapotrzebowanie, PO, przyjmowanie dostawy do magazynu |
| Tartak | Zlecenia produkcyjne, uzysk, koszty energii i robocizny, rozchód surowca, przyjęcie wyrobu |
| Transport HDS | 6 pojazdów, kalkulacja kosztów floty, harmonogram dostaw, blokada kolizji, WZ, potwierdzenie doręczenia |
| Kadry | 52 etaty w założeniach, wynagrodzenia i premia, składki i szacowany koszt pracodawcy |
| Finanse | Wynik finansowy, EBITDA, EBIT, CIT, VAT ilustracyjny, marże działów, płynność inwestorów |
| Ryzyka | Dodawanie ryzyk, scoring, odpowiedzialni, otwieranie i zamykanie |
| Dziennik | Historia zdarzeń użytkowników w lokalnej przeglądarce |
| Ustawienia | Kopia danych JSON, import, reset, status PWA i trybu lokalnego |
| Import danych | CSV, TSV, Excel XLSX, tabele HTML, mapowanie kolumn i walidacja przed zapisem |
| Obieg dokumentów | Automatyczny rejestr PO, PZ, WZ i rozliczeń, kompletność zamówień, zadania działów, obsługa wyjątków, załączniki i kontrola POD |

## Role

Zarząd, dyrektor operacyjny, handlowiec, opiekun inwestorów B2B, specjalista zakupów, magazynier, kierownik tartaku, planista transportu, kierowca HDS, finanse / księgowość, kadry.

Uprawnienia są zdefiniowane w `ROLE` w `app.js` i sprawdzane w funkcjach modyfikujących dane. W rzeczywistym wdrożeniu wymagana jest niezależna weryfikacja uprawnień na backendzie i polityki dostępu do rekordów.

## Podstawy modelu

- Przychód miesięczny w przykładowym scenariuszu: 5 664 750 zł netto. Wartość wyjściowa, nie rzeczywisty wynik firmy.
- Działy: budowlana 3 500 000 zł, elektryczna 1 200 000 zł, tartak 904 750 zł, transport zewnętrzny 60 000 zł.
- Flota: 3 samochody HDS, 2 dostawcze i 1 ciężarowy bez HDS.
- Kierowca HDS: przyjęte **9 000 zł netto średnio miesięcznie**, szacunkowo 13 003 zł brutto. Dokładne netto i rzeczywisty koszt pracodawcy są zależne od indywidualnej sytuacji podatkowej i składek.
- Wszystkie wartości kosztowe, marże, paliwo, etaty, składki, podatki i wielkość sprzedaży służą **symulacji** i można je edytować.
- W modelu koszty wynagrodzeń kierowców ujmowane są w kadrach, a w kosztach floty paliwo, leasing, ubezpieczenia, serwis, ogumienie i opłaty. Przychodów z wewnętrznego przewozu sprzedanych materiałów nie dodaje się ponownie do sprzedaży firmy.
- Wskaźnik marży transportu zewnętrznego na poziomie przychodu minus COGS jest *przed* przypisaniem kosztów wspólnej floty. Do pełnej rentowności transportu niezbędny jest model rozliczania kilometrów, czasu i alokacji kosztów.

## Import i migracja danych

W module **Import / migracja danych** można wczytać CSV (również z separatorem `;`), TSV, pierwszą tabelę HTML oraz plik XLSX (pierwszy arkusz, bez makr), wybrać kartotekę docelową i przed importem sprawdzić podgląd oraz przyporządkowanie kolumn. Obsługiwane kartoteki: **produkty, inwestorzy, dostawcy**. Zgodne identyfikatory aktualizują rekordy, pozostałe są dodawane. Błędne kwoty i ujemne stany blokują zatwierdzenie. W ustawieniach działa eksport i przywracanie pełnej kopii JSON.

PDF, JPG, PNG, WebP, HEIC i DOCX nie są automatycznie zamieniane na wpisy kartotekowe, ponieważ bez warstwy OCR lub rozpoznawania dokumentów byłoby to zawodne. Można je natomiast dołączyć jako dokument dostawy. Przed importem danych z realnego systemu warto usunąć dane osobowe i wykonać kopię zapasową.

## Obieg dokumentów 2.0

Kierowca HDS może dołączyć zdjęcie z aparatu lub dokument WZ/POD/protokół do określonej dostawy. Plik jest przechowywany lokalnie na używanym urządzeniu, do limitu rozmiaru. Biuro ma widok dokumentów oczekujących, może dokument zaakceptować lub zwrócić do poprawy. Zatwierdzone potwierdzenie odbioru (POD) służy jako warunek rozliczenia dostawy w lokalnym modelu. Jeśli kierowca zgłosi szkodę lub braki, potrzebny jest również zaakceptowany protokół i zamknięcie wyjątku przez biuro. **W tej wersji dokument nie jest przesyłany automatycznie między urządzeniami.** W docelowej wersji potrzebne są centralne repozytorium plików, prawdziwe konta, kontrola dostępu, powiadomienia i audyt serwerowy.

### Usprawnienia procesowe

- **Powiązanie z procesem, bez przepisywania numerów:** po złożeniu zamówienia zakupowego pojawia się wpis PO; po jego przyjęciu PZ; po wyjeździe dostawy WZ; po ukończeniu zlecenia tartaku dokument produkcyjny; po rozliczeniu zamówienia robocze zestawienie. Rejestr systemowy budowany jest z etapów operacji i można go wyeksportować do CSV. Dostępne są robocze wydruki HTML, nie są to faktury.
- **Kolejka działań:** automatyczne zadania dla brakującego POD, sprawdzenia dokumentu w biurze, poprawy odrzuconego pliku, faktury zakupowej po PZ, rozliczenia doręczonego zamówienia oraz rozstrzygnięcia szkody. Osobne zadania do uzupełnienia można przydzielić do działu i terminować.
- **Kompletność zamówień:** czterostopniowa lista kontrolna w każdym zamówieniu: zatwierdzenie, WZ, zaakceptowany POD, rozliczenie.
- **Obsługa szkód:** zgłoszenie kierowcy blokuje rozliczenie. Biuro zamyka wyjątek dopiero po zatwierdzeniu protokołu.
- **Rejestr plików:** załączniki PDF, zdjęcia, DOCX i XLSX przypisane do dostaw, zakupów, zamówień, produkcji lub inwestorów. Pliki o identycznej zawartości w danej sprawie mogą być rozpoznawane przez sumę SHA-256, gdy przeglądarka umożliwia jej obliczenie.
- **Kontrola jakości:** odesłanie pliku do poprawy wymaga uzasadnienia, a odrzuconego pliku nie można zatwierdzić bez dołączenia poprawionej wersji.

**Granice funkcjonalne:** nie ma jeszcze współdzielonej chmury, synchronizacji na żywo ani OCR. Generowane dokumenty są robocze, nie zastępują wymaganych prawnie dokumentów, faktur ani integracji KSeF. Import JSON przenosi metadane dokumentów i zadania, ale nie przenosi plików z magazynu IndexedDB.

## Zdjęcia i identyfikacja wizualna

Motyw: mocny granat `#07162b`, przygaszona czerwień `#b43e50`, jasne panele tabel. Na pulpicie oraz w sekcji importu znajdują się prawdziwe zdjęcia branżowe. Ich źródła i licencje są w `FOTOGRAFIE_I_LICENCJE.md`. Zdjęcia pobierane są z Pexels przy połączeniu z internetem; offline używane są tła zastępcze SVG.

## Zapis danych i działanie offline

Dane są zapisywane w `localStorage` przeglądarki. `sw.js` przechowuje pliki aplikacji do użytku offline przy uruchomieniu przez HTTPS lub localhost. Nie ma synchronizacji między komputerami, realnych kont, bazy danych, prawdziwych faktur ani usług zewnętrznych. Kopie JSON pozwalają przenosić stan między urządzeniami ręcznie.

## Przed wdrożeniem w rzeczywistej firmie

Należy wdrożyć centralną bazę danych i transakcje z blokadami magazynowymi, logowanie i role po stronie serwera, dziennik audytu, backupy, polityki retencji i ochrony danych, obsługę klientów rzeczywistych, integrację księgową i KSeF, aktualną logikę podatkowo-płacową, indywidualne stawki VAT, formalne potwierdzenia dostaw i dokumenty sprzedaży, a także testy współbieżności i bezpieczeństwa.

## GitHub

Repozytorium na GitHubie **nie zostało jeszcze opublikowane**. Pliki są przygotowane do umieszczenia w repozytorium w kolejnym, ostatnim etapie pracy.

W repozytorium warto uwzględnić: opis architektury, zrzuty ekranów na desktopie i telefonie, instrukcję uruchomienia, zestaw scenariuszy testowych, plan wdrożenia backendu i politykę prywatności. Przed publikacją należy uzgodnić docelową nazwę i widoczność repozytorium.
