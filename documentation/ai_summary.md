# Podsumowanie rozmowy na temat planowania PRD dla VibeTravels

## Decyzje
1. Głównym problemem użytkowników jest efektywne planowanie podróży między miejscami, tak aby zoptymalizować trasę wycieczki.
2. Docelową grupą są turyści amatorzy.
3. Notatki o wycieczkach będą zawierać: datę, lokalizację, atrakcje i ceny.
4. Relacja między notatkami a wycieczkami to jeden do jednego - jedna notatka przypisana do jednej wycieczki.
5. W profilu użytkownika będą przechowywane preferencje: rodzaj transportu, preferowane atrakcje i poziom aktywności.
6. Aplikacja będzie integrować się z API Perplexity PRO.
7. Użytkownicy będą mogli edytować wygenerowane przez AI plany.
8. Aplikacja będzie dostępna tylko w wersji webowej.
9. Plany nie muszą być bardzo szczegółowe.
10. UI będzie prosty - wprowadzanie tekstu i zatwierdzanie przyciskami.
11. Miarą sukcesu będzie liczba wycieczek na użytkownika, z celem retencji na poziomie 10%.
12. Użytkownik może utworzyć pustą wycieczkę (tylko z nazwą) i stopniowo wypełniać ją notatkami.
13. AI będzie generować opinie i zalecenia dla użytkownika, a nie tworzyć nowe plany.
14. Wyświetlanie notatek będzie w formie listy lub osi czasu z możliwością zmiany kolejności.
15. Aplikacja będzie umożliwiać eksport notatek do formatu markdown/JSON.
16. Aplikacja będzie sumować koszty z wszystkich notatek dla całkowitego budżetu wycieczki.

## Dopasowane rekomendacje
1. Zaprojektowanie prostego i intuicyjnego interfejsu użytkownika dla oszczędności czasu implementacji.
2. Skoncentrowanie się na przepływie: tworzenie wycieczki → dodawanie notatek → generowanie opinii przez AI.
3. Implementacja widoku wycieczki jako oś czasu lub lista, z możliwością łatwej zmiany kolejności notatek.
4. Zaprojektowanie czytelnego formatu prezentacji notatek w porządku chronologicznym.
5. Umożliwienie eksportu wycieczki w formacie markdown/JSON.
6. Efektywne wykorzystanie API Perplexity PRO poprzez dobrze przygotowane prompty.
7. Implementacja podstawowej autoryzacji użytkowników.
8. Tworzenie prostej struktury bazy danych obejmującej użytkowników, wycieczki i notatki.
9. Dodanie dedykowanego pola w notatce na informacje o zakwaterowaniu.
10. Minimalizacja liczby ekranów w aplikacji i uproszczenie przepływu pracy użytkownika.

## Podsumowanie planowania PRD

### Główne wymagania funkcjonalne
1. System kont użytkowników z profilem zawierającym preferencje podróżnicze
2. Możliwość tworzenia, edycji, przeglądania i usuwania wycieczek
3. Możliwość dodawania, edycji, przeglądania i usuwania notatek w ramach wycieczki
4. Integracja z AI (Perplexity PRO) do analizy notatek i generowania sugestii
5. Prezentacja notatek w formie listy/osi czasu z możliwością zmiany kolejności
6. Wyszukiwanie wycieczek po nazwie i lokalizacji
7. Pole dla informacji o zakwaterowaniu w notatkach
8. Sumowanie kosztów atrakcji z notatek
9. Eksport wycieczki do prostego formatu (markdown/JSON)

### Kluczowe historie użytkownika
1. Jako nowy użytkownik, chcę utworzyć konto, aby móc korzystać z aplikacji.
2. Jako użytkownik, chcę określić moje preferencje podróżnicze, aby AI lepiej analizowało moje wycieczki.
3. Jako użytkownik, chcę utworzyć nową wycieczkę z samą nazwą, aby rozpocząć proces planowania.
4. Jako użytkownik, chcę dodać notatkę do wycieczki zawierającą informacje o dacie, lokalizacji i atrakcjach.
5. Jako użytkownik, chcę dodać informacje o zakwaterowaniu do mojej notatki.
6. Jako użytkownik, chcę zmienić kolejność moich notatek, aby dopasować chronologię wycieczki.
7. Jako użytkownik, chcę wygenerować opinię AI o mojej wycieczce, aby otrzymać sugestie usprawnień (np. zmiana daty wizyty w muzeum, które jest zamknięte w zaplanowanym dniu).
8. Jako użytkownik, chcę zobaczyć całkowity koszt mojej wycieczki na podstawie cen z notatek.
9. Jako użytkownik, chcę wyeksportować moje notatki z wycieczki w prostym formacie.

### Kryteria sukcesu
1. Liczba wycieczek przypadająca na użytkownika - podstawowy KPI
2. Współczynnik retencji użytkowników na poziomie 10%
3. Skuteczna implementacja funkcji sugestii AI
4. Możliwość tworzenia kompletnych planów podróży przy minimalnym wysiłku użytkownika

### Ścieżka korzystania z produktu
1. Rejestracja i ustawienie preferencji podróżniczych
2. Utworzenie nowej wycieczki
3. Dodanie notatek z informacjami o atrakcjach, datach i cenach
4. Organizacja notatek w chronologicznej kolejności
5. Wygenerowanie opinii AI o spójności planu
6. Wprowadzenie zmian zgodnie z sugestiami AI
7. Zatwierdzenie planu wycieczki
8. Eksport planu w wybranym formacie

## Nierozwiązane kwestie
1. Stos technologiczny zostanie określony w kolejnych sesjach planistycznych.
2. Brak szczegółowych informacji o integracji z API Perplexity PRO (konkretne prompty, format danych).
3. Dokładna specyfikacja interfejsu użytkownika (układ, style, komponenty UI).
4. Szczegółowy plan testowania aplikacji przed wdrożeniem.

Citations:
[1] https://www.reddit.com/r/LocalLLaMA/comments/1dkx3e5/llm_for_summarizing_long_conversations/
[2] https://inspeerity.com/blog/how-to-write-a-comprehensive-project-requirements-document-for-software-development/
[3] https://www.aha.io/roadmapping/guide/requirements-management/what-is-a-good-product-requirements-document-template
[4] https://fireflies.ai/blog/summarize-a-meeting/
[5] https://www.notion.com/blog/how-to-write-a-prd
[6] https://www.atlassian.com/agile/product-management/requirements
[7] https://www.altexsoft.com/blog/product-requirements-document/
[8] https://dasycenter.org/ebp-tip-sheets/4-summarizing/
[9] https://blog.type.ai/post/how-to-write-a-product-requirements-document-prd-in-2024-with-examples-and-tips
[10] https://productschool.com/blog/product-strategy/product-template-requirements-document-prd
[11] https://blog.box.com/ai-summarization-definition-and-best-practices
[12] https://theproductmanager.com/topics/product-requirements-document/
[13] https://www.claap.io/blog/prd-template
[14] https://blog.promptlayer.com/ai-prompts-for-summarizing-long-reports-quickly-2/
[15] https://formlabs.com/blog/product-requirements-document-prd-with-template/
[16] https://www.hustlebadger.com/what-do-product-teams-do/prd-template-examples/
[17] https://www.readingrockets.org/sites/default/files/2023-08/summarizing_Strategies.pdf
[18] https://blog.wiseone.io/best-prompts-for-text-summarization/
[19] https://www.joinglyph.com/blog/summarizing-meetings-in-3-simple-steps
[20] https://aclanthology.org/2023.eacl-tutorials.3.pdf

---
Odpowiedź od Perplexity: pplx.ai/share