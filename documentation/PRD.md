# Dokument wymagań produktu (PRD) - VibeTravels

## 1. Przegląd produktu

VibeTravels to aplikacja webowa, która pomaga turystom amatorom w efektywnym planowaniu wycieczek. Główną funkcjonalnością aplikacji jest umożliwienie użytkownikom tworzenia notatek o miejscach i atrakcjach, które chcą odwiedzić, a następnie organizowanie ich w spójne plany wycieczek. Aplikacja wykorzystuje sztuczną inteligencję (Perplexity PRO) do analizy notatek i generowania sugestii, które pomagają użytkownikom w optymalizacji ich planów podróży.

Aplikacja pozwala na:
- Tworzenie i zarządzanie wycieczkami
- Dodawanie notatek z informacjami o atrakcjach, datach i cenach
- Organizowanie notatek w chronologicznej kolejności
- Generowanie sugestii AI dotyczących usprawnień planu
- Eksportowanie planów wycieczek w prostym formacie

MVP aplikacji skupia się na podstawowych funkcjonalnościach, które umożliwiają użytkownikom efektywne planowanie podróży, z naciskiem na prostotę interfejsu i łatwość użytkowania.

## 2. Problem użytkownika

Głównym problemem, który VibeTravels rozwiązuje, jest trudność w efektywnym planowaniu podróży między miejscami, co często prowadzi do marnowania cennego czasu podczas wycieczki. Turyści amatorzy często nie mają wystarczającej wiedzy o miejscach, które chcą odwiedzić, co może prowadzić do nieefektywnych planów podróży.

Konkretne problemy, które aplikacja adresuje:
- Trudność w ustaleniu optymalnej kolejności zwiedzania atrakcji
- Brak świadomości o godzinach otwarcia, dniach zamknięcia lub innych ograniczeniach dotyczących atrakcji
- Trudność w oszacowaniu całkowitych kosztów wycieczki
- Brak narzędzia do organizowania i przechowywania informacji o planowanych wycieczkach

VibeTravels pomaga użytkownikom tworzyć lepsze plany podróży poprzez organizację notatek i dostarczanie inteligentnych sugestii, które optymalizują ich doświadczenie podróżnicze.

## 3. Wymagania funkcjonalne

### 3.1 Zarządzanie kontami użytkowników
- Rejestracja i logowanie użytkowników
- Profil użytkownika z preferencjami podróżniczymi (rodzaj transportu, preferowane atrakcje, poziom aktywności)
- Zarządzanie danymi konta

### 3.2 Zarządzanie wycieczkami
- Tworzenie nowych wycieczek (z nazwą)
- Przeglądanie listy wycieczek
- Wyszukiwanie wycieczek po nazwie i lokalizacji
- Edycja i usuwanie wycieczek

### 3.3 Zarządzanie notatkami
- Dodawanie notatek do wycieczki z informacjami o dacie, lokalizacji, atrakcjach i cenach
- Dodawanie informacji o zakwaterowaniu
- Edycja i usuwanie notatek
- Zmiana kolejności notatek (chronologiczne uporządkowanie)

### 3.4 Integracja z AI
- Generowanie opinii i sugestii na podstawie notatek użytkownika
- Analiza spójności planu wycieczki
- Sugestie dotyczące potencjalnych problemów (np. zamknięte atrakcje w planowanych dniach)

### 3.5 Prezentacja i eksport danych
- Wyświetlanie notatek w formie listy lub osi czasu
- Sumowanie kosztów z wszystkich notatek dla całkowitej estymacji budżetu
- Eksport planu wycieczki do formatu markdown/JSON

## 4. Granice produktu

### 4.1 Co wchodzi w zakres MVP
- Prosty system kont użytkowników
- Tworzenie, edycja, przeglądanie i usuwanie wycieczek
- Dodawanie, edycja, przeglądanie i usuwanie notatek
- Podstawowa integracja z AI (Perplexity PRO) do generowania sugestii
- Prezentacja notatek w formie listy/osi czasu
- Wyszukiwanie wycieczek po nazwie i lokalizacji
- Sumowanie kosztów atrakcji
- Eksport wycieczki do prostego formatu

### 4.2 Co NIE wchodzi w zakres MVP
- Współdzielenie planów wycieczkowych między kontami
- Bogata obsługa i analiza multimediów (np. zdjęć miejsc do odwiedzenia)
- Zaawansowane planowanie czasu i logistyki
- Różne widoki planów (np. mapowy)
- Mechanizmy zbierania opinii użytkowników
- Zaawansowane filtrowanie i wyszukiwanie w treści notatek

## 5. Historyjki użytkowników

### US-001: Rejestracja konta
- Tytuł: Rejestracja nowego konta użytkownika
- Opis: Jako nowy użytkownik, chcę utworzyć konto w aplikacji, aby móc korzystać z jej funkcjonalności.
- Kryteria akceptacji:
  1. Użytkownik może wprowadzić dane rejestracyjne (email, hasło)
  2. System waliduje poprawność wprowadzonych danych
  3. Po pomyślnej rejestracji, użytkownik otrzymuje potwierdzenie
  4. Użytkownik może zalogować się przy użyciu utworzonych danych

### US-002: Logowanie do aplikacji
- Tytuł: Logowanie do istniejącego konta
- Opis: Jako zarejestrowany użytkownik, chcę zalogować się do aplikacji, aby uzyskać dostęp do moich wycieczek i notatek.
- Kryteria akceptacji:
  1. Użytkownik może wprowadzić dane logowania (email, hasło)
  2. System waliduje poprawność danych
  3. Po pomyślnym logowaniu, użytkownik jest przekierowany do głównego widoku aplikacji
  4. W przypadku niepoprawnych danych, użytkownik otrzymuje stosowny komunikat

### US-003: Ustawienie preferencji podróżniczych
- Tytuł: Konfiguracja preferencji podróżniczych w profilu
- Opis: Jako użytkownik, chcę określić moje preferencje podróżnicze, aby AI mogło lepiej analizować moje wycieczki.
- Kryteria akceptacji:
  1. Użytkownik może określić preferowany rodzaj transportu (samochód, pociąg, samolot)
  2. Użytkownik może wybrać preferowane atrakcje (muzea, parki, plaże)
  3. Użytkownik może określić preferowany poziom aktywności (niski, średni, wysoki)
  4. Preferencje są zapisywane i uwzględniane przy generowaniu sugestii AI

### US-004: Tworzenie nowej wycieczki
- Tytuł: Utworzenie nowej wycieczki
- Opis: Jako użytkownik, chcę utworzyć nową wycieczkę z nazwą, aby rozpocząć proces planowania.
- Kryteria akceptacji:
  1. Użytkownik może wprowadzić nazwę wycieczki
  2. System tworzy nową, pustą wycieczkę
  3. Nowa wycieczka pojawia się na liście wycieczek użytkownika
  4. Użytkownik może przejść do widoku szczegółów wycieczki

### US-005: Dodawanie notatki do wycieczki
- Tytuł: Dodanie notatki z informacjami o atrakcji
- Opis: Jako użytkownik, chcę dodać notatkę do wycieczki zawierającą informacje o dacie, lokalizacji i atrakcjach.
- Kryteria akceptacji:
  1. Użytkownik może wprowadzić datę (zakres dat lub pojedynczy dzień)
  2. Użytkownik może wprowadzić lokalizację
  3. Użytkownik może wprowadzić informacje o atrakcjach
  4. Użytkownik może wprowadzić szacunkowe ceny za atrakcje
  5. Notatka jest zapisywana i wyświetlana w widoku wycieczki

### US-006: Dodawanie informacji o zakwaterowaniu
- Tytuł: Dodanie informacji o zakwaterowaniu do notatki
- Opis: Jako użytkownik, chcę dodać informacje o zakwaterowaniu do mojej notatki, włączając w to linki do rezerwacji.
- Kryteria akceptacji:
  1. Użytkownik może wprowadzić informacje o zakwaterowaniu w dedykowanym polu
  2. Użytkownik może dodać linki do stron rezerwacyjnych
  3. Informacje o zakwaterowaniu są zapisywane i wyświetlane w notatce

### US-007: Edycja notatki
- Tytuł: Edycja istniejącej notatki
- Opis: Jako użytkownik, chcę edytować moje notatki, aby aktualizować informacje lub dostosować je do sugestii AI.
- Kryteria akceptacji:
  1. Użytkownik może wybrać notatkę do edycji
  2. System wyświetla formularz z aktualnymi danymi notatki
  3. Użytkownik może modyfikować wszystkie pola notatki
  4. Zmiany są zapisywane po zatwierdzeniu

### US-008: Usuwanie notatki
- Tytuł: Usunięcie notatki z wycieczki
- Opis: Jako użytkownik, chcę usunąć notatkę, która nie jest już potrzebna w mojej wycieczce.
- Kryteria akceptacji:
  1. Użytkownik może wybrać notatkę do usunięcia
  2. System wyświetla prośbę o potwierdzenie
  3. Po potwierdzeniu, notatka jest usuwana z wycieczki
  4. Widok wycieczki jest aktualizowany

### US-009: Zmiana kolejności notatek
- Tytuł: Zmiana kolejności notatek w wycieczce
- Opis: Jako użytkownik, chcę zmienić kolejność moich notatek, aby dopasować chronologię wycieczki.
- Kryteria akceptacji:
  1. Użytkownik może przesuwać notatki w górę lub w dół listy
  2. System zapisuje nową kolejność notatek
  3. Widok wycieczki odzwierciedla zaktualizowaną kolejność

### US-010: Generowanie opinii AI
- Tytuł: Generowanie opinii AI o wycieczce
- Opis: Jako użytkownik, chcę wygenerować opinię AI o mojej wycieczce, aby otrzymać sugestie usprawnień.
- Kryteria akceptacji:
  1. Użytkownik może zainicjować analizę AI poprzez kliknięcie przycisku
  2. System przekazuje dane notatek i preferencje użytkownika do API Perplexity PRO
  3. System wyświetla wygenerowane sugestie (np. zmiana daty wizyty w muzeum, które jest zamknięte w zaplanowanym dniu)
  4. Użytkownik może zaakceptować lub odrzucić sugestie

### US-011: Przeglądanie wycieczek
- Tytuł: Przeglądanie listy wycieczek
- Opis: Jako użytkownik, chcę przeglądać listę moich wycieczek, aby wybrać tę, nad którą chcę pracować.
- Kryteria akceptacji:
  1. System wyświetla listę wszystkich wycieczek użytkownika
  2. Lista zawiera nazwy wycieczek i podstawowe informacje
  3. Użytkownik może wybrać wycieczkę, aby zobaczyć jej szczegóły

### US-012: Wyszukiwanie wycieczek
- Tytuł: Wyszukiwanie wycieczek po nazwie i lokalizacji
- Opis: Jako użytkownik, chcę wyszukiwać wycieczki po nazwie i lokalizacji, aby szybko znaleźć potrzebne informacje.
- Kryteria akceptacji:
  1. Użytkownik może wprowadzić tekst wyszukiwania
  2. System filtruje wycieczki na podstawie nazwy i lokalizacji
  3. Wyniki wyszukiwania są wyświetlane w czasie rzeczywistym
  4. Brak wyników wyszukiwania jest odpowiednio komunikowany

### US-013: Usuwanie wycieczki
- Tytuł: Usunięcie wycieczki
- Opis: Jako użytkownik, chcę usunąć wycieczkę, która nie jest mi już potrzebna.
- Kryteria akceptacji:
  1. Użytkownik może wybrać wycieczkę do usunięcia
  2. System wyświetla prośbę o potwierdzenie
  3. Po potwierdzeniu, wycieczka i wszystkie jej notatki są usuwane
  4. Lista wycieczek jest aktualizowana

### US-014: Wyświetlanie notatek w formie listy/osi czasu
- Tytuł: Wyświetlanie notatek w formie listy lub osi czasu
- Opis: Jako użytkownik, chcę przeglądać moje notatki w formie listy lub osi czasu, aby lepiej zrozumieć chronologię wycieczki.
- Kryteria akceptacji:
  1. System wyświetla notatki w porządku chronologicznym
  2. Użytkownik może przełączać się między widokiem listy a osią czasu (jeśli dostępne)
  3. Widok jasno pokazuje daty i lokalizacje

### US-015: Sumowanie kosztów wycieczki
- Tytuł: Sumowanie kosztów atrakcji z notatek
- Opis: Jako użytkownik, chcę zobaczyć całkowity koszt mojej wycieczki na podstawie cen z notatek.
- Kryteria akceptacji:
  1. System sumuje wszystkie koszty z notatek w ramach wycieczki
  2. Całkowity koszt jest wyświetlany w widoku wycieczki
  3. Suma jest aktualizowana automatycznie przy zmianach w notatkach

### US-016: Eksport planu wycieczki
- Tytuł: Eksport planu wycieczki do prostego formatu
- Opis: Jako użytkownik, chcę wyeksportować moje notatki z wycieczki w formacie markdown/JSON, aby móc je udostępnić lub wykorzystać poza aplikacją.
- Kryteria akceptacji:
  1. Użytkownik może wybrać opcję eksportu wycieczki
  2. Użytkownik może wybrać format eksportu (markdown/JSON)
  3. System generuje plik w wybranym formacie
  4. Użytkownik może pobrać wygenerowany plik

### US-017: Edycja wycieczki
- Tytuł: Edycja nazwy wycieczki
- Opis: Jako użytkownik, chcę edytować nazwę mojej wycieczki, aby lepiej odzwierciedlała jej zawartość.
- Kryteria akceptacji:
  1. Użytkownik może wybrać opcję edycji wycieczki
  2. System wyświetla formularz z aktualną nazwą wycieczki
  3. Użytkownik może wprowadzić nową nazwę
  4. Zmiany są zapisywane po zatwierdzeniu

### US-018: Wylogowanie z aplikacji
- Tytuł: Wylogowanie z aplikacji
- Opis: Jako zalogowany użytkownik, chcę wylogować się z aplikacji, aby zabezpieczyć moje dane.
- Kryteria akceptacji:
  1. Użytkownik może wybrać opcję wylogowania
  2. System kończy sesję użytkownika
  3. Użytkownik jest przekierowany do strony logowania
  4. Ponowny dostęp do danych wymaga zalogowania

### US-019: Obsługa błędów logowania
- Tytuł: Obsługa nieprawidłowych danych logowania
- Opis: Jako użytkownik, chcę otrzymać jasną informację, gdy wprowadzę nieprawidłowe dane logowania.
- Kryteria akceptacji:
  1. System weryfikuje wprowadzone dane logowania
  2. W przypadku nieprawidłowych danych, system wyświetla zrozumiały komunikat o błędzie
  3. Użytkownik może ponowić próbę logowania
  4. System oferuje opcję resetowania hasła

### US-020: Resetowanie hasła
- Tytuł: Resetowanie zapomnianego hasła
- Opis: Jako użytkownik, chcę zresetować moje hasło, gdy je zapomnę.
- Kryteria akceptacji:
  1. Użytkownik może wybrać opcję "Zapomniałem hasła" na stronie logowania
  2. System prosi o podanie adresu email
  3. System wysyła link do resetowania hasła na podany adres
  4. Użytkownik może ustawić nowe hasło po kliknięciu w link

## 6. Metryki sukcesu

### 6.1 Metryki produktowe
- Liczba wycieczek przypadająca na użytkownika - podstawowy KPI
- Średnia liczba notatek na wycieczkę
- Procent wycieczek, dla których wygenerowano opinię AI
- Procent wycieczek, które zostały wyeksportowane
- 90% użytkowników posiada wypełnione preferencje turystyczne w swoim profilu
- 75% użytkowników generuje 3 lub więcej planów wycieczek na rok

### 6.2 Metryki biznesowe
- Współczynnik retencji użytkowników na poziomie 10%
- Liczba aktywnych użytkowników (dziennie/miesięcznie)
- Średni czas spędzony w aplikacji

### 6.3 Kryteria sukcesu MVP
- Użytkownicy mogą skutecznie tworzyć i zarządzać wycieczkami
- Integracja z AI dostarcza wartościowe sugestie
- Użytkownicy mogą organizować notatki w chronologicznej kolejności
- Aplikacja pozwala na szacowanie kosztów wycieczki
- Użytkownicy mogą eksportować swoje plany
