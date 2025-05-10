
<conversation_summary>
<decisions>
1. Konta użytkowników będą zarządzane przez Supabase Auth, a preferencje podróżne w oddzielnej tabeli USER_DETAILS.
2. Wycieczka będzie zawierać nazwę i datę informacyjną (niezwiązaną z datami w notatkach).
3. Nie będzie współdzielenia wycieczek między użytkownikami.
4. Notatki będą uporządkowane według kolejności, nie będą przypisane do konkretnego dnia.
5. Jedna notatka może mieć wiele atrakcji (relacja 1:N), każda atrakcja należy do jednej notatki.
6. Historia zmian nie jest wymagana.
7. Koszty będą przechowywane jako prosta wartość i waluta.
8. Aplikacja będzie obsługiwać tylko linki zewnętrzne jako załączniki (bez plików).
9. Kontekst dla AI będzie budowany dynamicznie na podstawie preferencji użytkownika i notatek.
10. Aplikacja będzie obsługiwać tylko język polski.
11. Lokalizacje będą przechowywane szczegółowo z dokładnym adresem i możliwym identyfikatorem teryt_id.
12. Wycieczki będą filtrowane tylko po dacie.
13. Atrakcje będą oceniane w skali 1-10.
14. Godziny otwarcia atrakcji są kluczowe dla analizy AI.
15. Transport między lokalizacjami będzie modelowany jako specjalny rodzaj notatki.
16. Kategorie atrakcji będą predefiniowane, nie tworzone przez użytkownika.
17. Czas zwiedzania atrakcji będzie szacowany przez użytkownika.
18. Aplikacja będzie wspierać planowanie budżetu podróży.
19. Będzie obsługa prostej ikony/emoji dla atrakcji.
20. Historia wygenerowanych planów wycieczek będzie przechowywana.
21. Pojedyncza tabela notatek z informacją o dacie będzie wystarczająca.
22. Budżet będzie ograniczony do sumowania kosztów całej wycieczki.
</decisions>

<matched_recommendations>
1. Wykorzystanie struktury tabel: USER_DETAILS, TRIPS, NOTES, ATTRACTIONS, LOCATIONS, TRANSPORT_DETAILS i EXTERNAL_LINKS.
2. Implementacja relacji 1:N między notatkami a atrakcjami.
3. Przechowywanie godzin otwarcia i dni tygodnia dla atrakcji.
4. Wdrożenie Row Level Security dla zapewnienia bezpieczeństwa danych.
5. Modelowanie transportu jako specjalnego rodzaju notatki z dedykowaną tabelą TRANSPORT_DETAILS.
6. Zastosowanie typów ENUM dla kategoryzacji notatek, transportu i walut.
7. Implementacja wyzwalaczy dla automatycznego ustawiania kolejności notatek.
8. Funkcje do walidacji planu wycieczki (sprawdzanie godzin otwarcia atrakcji).
9. Funkcja generująca kontekst dla AI na podstawie danych użytkownika i notatek.
10. Zmaterializowane widoki dla efektywnej analizy kosztów wycieczek.
11. Przechowywanie kategorii atrakcji z mapowaniem wiele-do-wielu.
12. Funkcjonalność eksportu danych wycieczki do formatu JSON.
13. Typowanie danych z odpowiednimi ograniczeniami CHECK.
14. Funkcja automatycznego generowania notatek transportowych między lokalizacjami.
15. Przechowywanie linków zewnętrznych dla atrakcji i notatek.
</matched_recommendations>

<database_planning_summary>
# Podsumowanie planowania bazy danych dla VibeTravels MVP

## Główna struktura bazy danych

Baza danych dla aplikacji VibeTravels będzie oparta na PostgreSQL z integracją z Supabase dla uwierzytelniania. Struktura bazy obejmuje następujące główne encje:

### Użytkownicy i preferencje
- **Użytkownicy**: Zarządzani przez Supabase Auth
- **Preferencje użytkowników**: Przechowywane w tabeli USER_DETAILS
  - Preferowany transport
  - Poziom aktywności
  - Preferowane typy atrakcji

### Wycieczki i organizacja
- **Wycieczki**: Podstawowa encja grupująca notatki
  - Nazwa, opis, data informacyjna
  - Relacja 1:N z użytkownikiem (każdy użytkownik może mieć wiele wycieczek)
- **Notatki**: Chronologiczna lista elementów wycieczki
  - Pozycja określająca kolejność
  - Typ notatki (atrakcja, transport, nocleg, inne)
  - Zakres dat (TSTZRANGE)
  - Relacja 1:N z wycieczką

### Atrakcje i lokalizacje
- **Atrakcje**: Główne punkty zwiedzania
  - Nazwa, opis
  - Koszt (wartość + waluta)
  - Rating (1-10)
  - Godziny otwarcia i dni tygodnia
  - Szacowany czas zwiedzania
  - Ikona/emoji
  - Relacja N:1 z notatką (jedna notatka może mieć wiele atrakcji)
- **Lokalizacje**: Miejsca geograficzne
  - Dokładny adres
  - Miasto, kraj
  - Identyfikator teryt_id (dla lokalizacji w Polsce)

### Transport i połączenia
- **Szczegóły transportu**: Dane o przejazdach
  - Dystans
  - Czas trwania
  - Koszt
  - Typ transportu (samochód, pociąg, autobus, samolot, etc.)
  - Relacja 1:1 z notatką typu transport

### Dodatkowe elementy
- **Linki zewnętrzne**: Odnośniki do stron z dodatkowymi informacjami
  - URL, tytuł, opis
  - Relacja z notatkami lub atrakcjami
- **Kategorie atrakcji**: Predefiniowane typy atrakcji
  - Relacja N:M z atrakcjami
- **Budżet wycieczki**: Suma kosztów wszystkich elementów

## Relacje między encjami

1. Użytkownik (1) -> (N) Wycieczki
2. Wycieczka (1) -> (N) Notatki
3. Notatka (1) -> (N) Atrakcje
4. Notatka (1) -> (0..1) Szczegóły transportu
5. Atrakcja (N) -> (1) Lokalizacja
6. Atrakcja (N) <-> (M) Kategorie atrakcji
7. Atrakcja/Notatka (1) -> (N) Linki zewnętrzne

## Bezpieczeństwo i integralność danych

- **Row Level Security**: Każdy użytkownik ma dostęp tylko do swoich danych
- **Ograniczenia CHECK**: 
  - Koszty >= 0
  - Rating między 1 a 10
  - Czas zwiedzania > 0
  - Dystans > 0
- **Relacje CASCADE DELETE**: Usunięcie wycieczki usuwa wszystkie powiązane dane
- **Wyzwalacze**:
  - Automatyczne ustawianie i aktualizacja pozycji notatek
  - Aktualizacja pola updated_at

## Funkcjonalności specjalne

1. **Walidacja planu wycieczki**:
   - Sprawdzanie godzin otwarcia atrakcji
   - Weryfikacja dostępności w dane dni tygodnia
   - Kontrola realistyczności czasów przejazdów

2. **Generowanie kontekstu dla AI**:
   - Dynamiczne budowanie kontekstu z preferencji, notatek i atrakcji
   - Format tekstowy gotowy do przekazania do API OpenRouter.ai

3. **Analiza kosztów**:
   - Zmaterializowane widoki dla szybkiego sumowania wydatków
   - Podział na koszty atrakcji i transportu

4. **Eksport danych**:
   - Funkcja eksportująca wycieczkę do formatu JSON
   - Przygotowanie danych do generowania PDF (poza MVP)

5. **Automatyczne notatki transportowe**:
   - Generowanie notatek transportowych między lokalizacjami
   - Szacowanie dystansu, czasu i kosztu przejazdu
</database_planning_summary>

<unresolved_issues>
1. Dokładny format i sposób przechowywania historii wygenerowanych planów wycieczek przed zatwierdzeniem.
2. Szczegóły implementacji generowania dokumentów PDF w przyszłych wersjach.
3. Sposób implementacji i przechowywania ikon/emoji dla atrakcji.
4. Dokładny algorytm/API do automatycznego szacowania dystansu i czasu przejazdu między lokalizacjami.
5. Strategie optymalizacji wydajności dla złożonych zapytań w przypadku dużej liczby wycieczek i notatek.
</unresolved_issues>
</conversation_summary>
