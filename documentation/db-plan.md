# Schemat bazy danych PostgreSQL dla VibeTravels

## 1. Tabele

### 1.1. Tabele użytkowników

#### users
| Kolumna | Typ | Ograniczenia | Opis |
|---------|-----|--------------|------|
| id | UUID | PRIMARY KEY | Unikalny identyfikator |
| email | VARCHAR(255) | UNIQUE NOT NULL | Adres email użytkownika |
| encrypted_password | VARCHAR(255) | NOT NULL | Zaszyfrowane hasło |
| confirmed_at | TIMESTAMPTZ | | Data potwierdzenia konta |
| confirmation_token | VARCHAR(255) | | Token potwierdzenia konta |
| confirmation_sent_at | TIMESTAMPTZ | | Data wysłania tokenu potwierdzenia |
| recovery_token | VARCHAR(255) | | Token resetu hasła |
| recovery_sent_at | TIMESTAMPTZ | | Data wysłania tokenu resetu hasła |
| email_change_token | VARCHAR(255) | | Token zmiany adresu email |
| email_change | VARCHAR(255) | | Nowy adres email |
| email_change_sent_at | TIMESTAMPTZ | | Data wysłania tokenu zmiany adresu email |
| last_sign_in_at | TIMESTAMPTZ | | Data ostatniego logowania |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | Data utworzenia konta |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | Data ostatniej aktualizacji |

> **Uwaga:** Tabela `users` jest zarządzana przez Supabase Auth i nie powinna być modyfikowana bezpośrednio. Jest ona hostowana w schemacie `auth` i dostępna przez widok `auth.users`. W aplikacji powinna być używana głównie do odczytu i poprzez API Supabase Auth.

#### user_details
| Kolumna | Typ | Ograniczenia | Opis |
|---------|-----|--------------|------|
| id | UUID | PRIMARY KEY DEFAULT uuid_generate_v4() | Unikalny identyfikator |
| user_id | UUID | NOT NULL UNIQUE REFERENCES auth.users(id) | Klucz obcy do Supabase Auth |
| preferred_transport_type | transport_type | DEFAULT 'CAR' | Preferowany rodzaj transportu |
| preferred_activity_level | VARCHAR(10) | DEFAULT 'MEDIUM' | Preferowany poziom aktywności (LOW, MEDIUM, HIGH) |
| preferred_attractions | VARCHAR[] | DEFAULT '{}' | Tablica preferowanych typów atrakcji |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | Data utworzenia rekordu |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | Data ostatniej aktualizacji |

### 1.2. Tabele wycieczek

#### trips
| Kolumna | Typ | Ograniczenia | Opis |
|---------|-----|--------------|------|
| id | UUID | PRIMARY KEY DEFAULT uuid_generate_v4() | Unikalny identyfikator |
| user_id | UUID | NOT NULL | Klucz obcy do Supabase Auth |
| name | VARCHAR(255) | NOT NULL | Nazwa wycieczki |
| description | TEXT | | Opis wycieczki |
| start_date | DATE | | Data początku wycieczki |
| stop_date  | DATE | | Data końca wycieczki |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | Data utworzenia rekordu |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | Data ostatniej aktualizacji |

#### notes
| Kolumna | Typ | Ograniczenia | Opis |
|---------|-----|--------------|------|
| id | UUID | PRIMARY KEY DEFAULT uuid_generate_v4() | Unikalny identyfikator |
| trip_id | UUID | NOT NULL REFERENCES trips(id) ON DELETE CASCADE | Powiązana wycieczka |
| position | INTEGER | NOT NULL | Pozycja w kolejności |
| title | VARCHAR(255) | NOT NULL | Tytuł notatki |
| content | TEXT | | Treść notatki |
| note_type | note_type | DEFAULT 'ATTRACTION' | Typ notatki |
| start_date | TSTZRANGE | | Data startu atrakcji(format: 2025-05-05 01:01:01:000) |
| duration   | INTERVAL | | Data trwania atrakcji ('1 h') |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | Data utworzenia rekordu |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | Data ostatniej aktualizacji |

#### locations
| Kolumna | Typ | Ograniczenia | Opis |
|---------|-----|--------------|------|
| id | UUID | PRIMARY KEY DEFAULT uuid_generate_v4() | Unikalny identyfikator |
| address | TEXT | | Dokładny adres |
| city | VARCHAR(100) | | Miasto |
| country | VARCHAR(100) | DEFAULT 'Polska' | Kraj |
| teryt_id | VARCHAR(20) | | Identyfikator TERYT |
| coordinates | POINT | | Współrzędne geograficzne |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | Data utworzenia rekordu |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | Data ostatniej aktualizacji |

### 1.3. Tabele atrakcji i transportu

#### attractions
| Kolumna | Typ | Ograniczenia | Opis |
|---------|-----|--------------|------|
| id | UUID | PRIMARY KEY DEFAULT uuid_generate_v4() | Unikalny identyfikator |
| note_id | UUID | NOT NULL REFERENCES notes(id) ON DELETE CASCADE | Powiązana notatka |
| name | VARCHAR(255) | NOT NULL | Nazwa atrakcji |
| description | TEXT | | Opis atrakcji |
| location_id | UUID | REFERENCES locations(id) | Powiązana lokalizacja |
| cost_value | DECIMAL(10,2) | NOT NULL DEFAULT 0 CHECK (cost_value >= 0) | Wartość kosztu |
| cost_currency | currency_code | DEFAULT 'PLN' | Waluta kosztu |
| rating | INTEGER | CHECK (rating BETWEEN 1 AND 10) | Ocena (1-10) |
| opening_time | TIME | | Godzina otwarcia |
| closing_time | TIME | | Godzina zamknięcia |
| days_open | VARCHAR(7) | | Dni tygodnia otwarcia (np. '1234567') |
| visit_duration | INTEGER | CHECK (visit_duration > 0) | Czas zwiedzania w minutach |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | Data utworzenia rekordu |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | Data ostatniej aktualizacji |

#### attraction_categories
| Kolumna | Typ | Ograniczenia | Opis |
|---------|-----|--------------|------|
| id | UUID | PRIMARY KEY DEFAULT uuid_generate_v4() | Unikalny identyfikator |
| name | VARCHAR(100) | NOT NULL | Nazwa kategorii |
| description | TEXT | | Opis kategorii |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | Data utworzenia rekordu |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | Data ostatniej aktualizacji |

#### attraction_category_mapping
| Kolumna | Typ | Ograniczenia | Opis |
|---------|-----|--------------|------|
| attraction_id | UUID | NOT NULL REFERENCES attractions(id) ON DELETE CASCADE | Powiązana atrakcja |
| category_id | UUID | NOT NULL REFERENCES attraction_categories(id) | Powiązana kategoria |
| PRIMARY KEY | | (attraction_id, category_id) | Klucz złożony |

#### transport_details
| Kolumna | Typ | Ograniczenia | Opis |
|---------|-----|--------------|------|
| id | UUID | PRIMARY KEY DEFAULT uuid_generate_v4() | Unikalny identyfikator |
| note_id | UUID | NOT NULL REFERENCES notes(id) ON DELETE CASCADE UNIQUE | Powiązana notatka transportowa |
| from_location_id | UUID | REFERENCES locations(id) | Lokalizacja początkowa |
| to_location_id | UUID | REFERENCES locations(id) | Lokalizacja docelowa |
| distance | DECIMAL(10,2) | CHECK (distance > 0) | Dystans w kilometrach |
| duration | INTEGER | CHECK (duration > 0) | Czas przejazdu w minutach |
| cost_value | DECIMAL(10,2) | NOT NULL DEFAULT 0 CHECK (cost_value >= 0) | Wartość kosztu |
| cost_currency | currency_code | DEFAULT 'PLN' | Waluta kosztu |
| transport_type | transport_type | DEFAULT 'CAR' | Rodzaj transportu |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | Data utworzenia rekordu |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | Data ostatniej aktualizacji |

### 1.4. Tabele dodatkowe

#### external_links
| Kolumna | Typ | Ograniczenia | Opis |
|---------|-----|--------------|------|
| id | UUID | PRIMARY KEY DEFAULT uuid_generate_v4() | Unikalny identyfikator |
| note_id | UUID | REFERENCES notes(id) ON DELETE CASCADE | Powiązana notatka |
| attraction_id | UUID | REFERENCES attractions(id) ON DELETE CASCADE | Powiązana atrakcja |
| url | TEXT | NOT NULL | Adres URL |
| title | VARCHAR(255) | | Tytuł linku |
| description | TEXT | | Opis linku |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | Data utworzenia rekordu |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | Data ostatniej aktualizacji |
| | | CHECK ((note_id IS NOT NULL AND attraction_id IS NULL) OR (note_id IS NULL AND attraction_id IS NOT NULL)) | Link musi być powiązany albo z notatką, albo z atrakcją |

#### trip_budget
| Kolumna | Typ | Ograniczenia | Opis |
|---------|-----|--------------|------|
| id | UUID | PRIMARY KEY DEFAULT uuid_generate_v4() | Unikalny identyfikator |
| trip_id | UUID | NOT NULL REFERENCES trips(id) ON DELETE CASCADE UNIQUE | Powiązana wycieczka |
| total_budget | DECIMAL(10,2) | NOT NULL CHECK (total_budget > 0) | Całkowity budżet |
| currency | currency_code | DEFAULT 'PLN' | Waluta budżetu |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | Data utworzenia rekordu |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | Data ostatniej aktualizacji |

#### ai_suggestions_history
| Kolumna | Typ | Ograniczenia | Opis |
|---------|-----|--------------|------|
| id | UUID | PRIMARY KEY DEFAULT uuid_generate_v4() | Unikalny identyfikator |
| trip_id | UUID | NOT NULL REFERENCES trips(id) ON DELETE CASCADE | Powiązana wycieczka |
| suggestion_text | TEXT | NOT NULL | Treść sugestii AI |
| is_applied | BOOLEAN | DEFAULT FALSE | Czy sugestia została zastosowana |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | Data utworzenia rekordu |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | Data ostatniej aktualizacji |

### 1.5. Typy wyliczeniowe (ENUM)

```sql
CREATE TYPE note_type AS ENUM ('ATTRACTION', 'TRANSPORT', 'ACCOMMODATION', 'OTHER');
CREATE TYPE transport_type AS ENUM ('CAR', 'TRAIN', 'BUS', 'PLANE', 'BIKE', 'WALK', 'OTHER');
CREATE TYPE currency_code AS ENUM ('PLN', 'EUR', 'USD', 'GBP');
```

## 2. Relacje między tabelami

1. **Użytkownik ⟷ user_details**: Relacja 1:1 poprzez `user_id` w tabeli `user_details`
2. **Użytkownik ⟷ trips**: Relacja 1:N, użytkownik może mieć wiele wycieczek
3. **trips ⟷ notes**: Relacja 1:N, wycieczka może mieć wiele notatek
4. **notes ⟷ attractions**: Relacja 1:N, notatka może mieć wiele atrakcji
5. **notes ⟷ transport_details**: Relacja 1:1, notatka typu transport ma jedne szczegóły transportu
6. **attractions ⟷ locations**: Relacja N:1, wiele atrakcji może odnosić się do jednej lokalizacji
7. **attractions ⟷ attraction_categories**: Relacja N:M poprzez tabelę łączącą `attraction_category_mapping`
8. **trips ⟷ trip_budget**: Relacja 1:1, wycieczka ma jeden budżet
9. **trips ⟷ ai_suggestions_history**: Relacja 1:N, wycieczka może mieć wiele sugestii AI
10. **external_links ⟷ notes/attractions**: Relacja 1:N, link może być powiązany z notatką lub atrakcją

## 3. Indeksy

```sql
-- Indeksy dla wycieczek
CREATE INDEX idx_trips_user_id ON trips(user_id);
CREATE INDEX idx_trips_dates ON trips(start_date, stop_date);

-- Indeksy dla notatek
CREATE INDEX idx_notes_trip_id ON notes(trip_id);
CREATE INDEX idx_notes_position ON notes(position);
CREATE INDEX idx_notes_start_date ON notes(start_date);
CREATE INDEX idx_notes_trip_position ON notes(trip_id, position);

-- Indeksy dla atrakcji
CREATE INDEX idx_attraction_note_id ON attractions(note_id);
CREATE INDEX idx_attraction_location_id ON attractions(location_id);
CREATE INDEX idx_attraction_rating ON attractions(rating);

-- Indeksy dla transportu
CREATE INDEX idx_transport_note_id ON transport_details(note_id);
CREATE INDEX idx_transport_locations ON transport_details(from_location_id, to_location_id);

-- Indeksy dla linków
CREATE INDEX idx_external_links_note_id ON external_links(note_id);
CREATE INDEX idx_external_links_attraction_id ON external_links(attraction_id);

-- Indeksy dla mapowań kategorii
CREATE INDEX idx_attraction_category_mapping_attraction ON attraction_category_mapping(attraction_id);
CREATE INDEX idx_attraction_category_mapping_category ON attraction_category_mapping(category_id);

-- Indeksy dla sugestii AI
CREATE INDEX idx_ai_suggestions_trip_id ON ai_suggestions_history(trip_id);
```

## 4. Zasady Row Level Security (RLS)

```sql
-- Włączenie RLS na tabelach
ALTER TABLE user_details ENABLE ROW LEVEL SECURITY;
ALTER TABLE trips ENABLE ROW LEVEL SECURITY;
ALTER TABLE notes ENABLE ROW LEVEL SECURITY;
ALTER TABLE attractions ENABLE ROW LEVEL SECURITY;
ALTER TABLE transport_details ENABLE ROW LEVEL SECURITY;
ALTER TABLE external_links ENABLE ROW LEVEL SECURITY;
ALTER TABLE trip_budget ENABLE ROW LEVEL SECURITY;
ALTER TABLE ai_suggestions_history ENABLE ROW LEVEL SECURITY;

-- Polityki dostępu
CREATE POLICY user_details_policy ON user_details
  USING (user_id = auth.uid());

CREATE POLICY trips_policy ON trips
  USING (user_id = auth.uid());

CREATE POLICY notes_policy ON notes
  USING (trip_id IN (SELECT id FROM trips WHERE user_id = auth.uid()));

CREATE POLICY attractions_policy ON attractions
  USING (note_id IN (SELECT n.id FROM notes n JOIN trips t ON n.trip_id = t.id WHERE t.user_id = auth.uid()));

CREATE POLICY transport_details_policy ON transport_details
  USING (note_id IN (SELECT n.id FROM notes n JOIN trips t ON n.trip_id = t.id WHERE t.user_id = auth.uid()));

CREATE POLICY external_links_policy ON external_links
  USING (
    (note_id IN (SELECT n.id FROM notes n JOIN trips t ON n.trip_id = t.id WHERE t.user_id = auth.uid())) OR
    (attraction_id IN (SELECT a.id FROM attractions a JOIN notes n ON a.note_id = n.id JOIN trips t ON n.trip_id = t.id WHERE t.user_id = auth.uid()))
  );

CREATE POLICY trip_budget_policy ON trip_budget
  USING (trip_id IN (SELECT id FROM trips WHERE user_id = auth.uid()));

CREATE POLICY ai_suggestions_history_policy ON ai_suggestions_history
  USING (trip_id IN (SELECT id FROM trips WHERE user_id = auth.uid()));
```

## 5. Wyzwalacze i funkcje

```sql
-- Wyzwalacz dla aktualizacji updated_at
CREATE OR REPLACE FUNCTION update_modified_column()
RETURNS TRIGGER AS $$
BEGIN
  NEW.updated_at = NOW();
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Zastosowanie wyzwalacza do wszystkich tabel
CREATE TRIGGER tr_user_details_updated_at BEFORE UPDATE ON user_details FOR EACH ROW EXECUTE FUNCTION update_modified_column();
CREATE TRIGGER tr_trips_updated_at BEFORE UPDATE ON trips FOR EACH ROW EXECUTE FUNCTION update_modified_column();
CREATE TRIGGER tr_notes_updated_at BEFORE UPDATE ON notes FOR EACH ROW EXECUTE FUNCTION update_modified_column();
CREATE TRIGGER tr_attractions_updated_at BEFORE UPDATE ON attractions FOR EACH ROW EXECUTE FUNCTION update_modified_column();
CREATE TRIGGER tr_locations_updated_at BEFORE UPDATE ON locations FOR EACH ROW EXECUTE FUNCTION update_modified_column();
CREATE TRIGGER tr_transport_details_updated_at BEFORE UPDATE ON transport_details FOR EACH ROW EXECUTE FUNCTION update_modified_column();
CREATE TRIGGER tr_external_links_updated_at BEFORE UPDATE ON external_links FOR EACH ROW EXECUTE FUNCTION update_modified_column();
CREATE TRIGGER tr_trip_budget_updated_at BEFORE UPDATE ON trip_budget FOR EACH ROW EXECUTE FUNCTION update_modified_column();
CREATE TRIGGER tr_ai_suggestions_history_updated_at BEFORE UPDATE ON ai_suggestions_history FOR EACH ROW EXECUTE FUNCTION update_modified_column();

-- Wyzwalacz dla automatycznego ustawiania position dla notatek
CREATE OR REPLACE FUNCTION set_note_position()
RETURNS TRIGGER AS $$
BEGIN
  IF NEW.position IS NULL THEN
    NEW.position := (SELECT COALESCE(MAX(position), 0) + 1 FROM notes WHERE trip_id = NEW.trip_id);
  ELSE
    -- Przesuń notatki, jeśli nowa pozycja już istnieje
    UPDATE notes 
    SET position = position + 1
    WHERE trip_id = NEW.trip_id 
      AND position >= NEW.position 
      AND id != NEW.id;
  END IF;
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER tr_note_position
BEFORE INSERT OR UPDATE OF position ON notes
FOR EACH ROW EXECUTE FUNCTION set_note_position();

-- Funkcja obliczająca czas zakończenia atrakcji
CREATE OR REPLACE FUNCTION calculate_end_time(p_start_date TSTZRANGE, p_duration INTERVAL)
RETURNS TIMESTAMP WITH TIME ZONE AS $$
BEGIN
  RETURN lower(p_start_date) + p_duration;
END;
$$ LANGUAGE plpgsql;
```

## 6. Widoki zmaterializowane

```sql
-- Widok do analizy kosztów wycieczek
CREATE MATERIALIZED VIEW trip_cost_analysis AS
SELECT 
  t.id AS trip_id,
  t.user_id,
  t.name AS trip_name,
  t.start_date,
  t.stop_date,
  SUM(CASE WHEN n.note_type = 'ATTRACTION' THEN a.cost_value ELSE 0 END) AS attractions_cost,
  SUM(CASE WHEN n.note_type = 'TRANSPORT' THEN td.cost_value ELSE 0 END) AS transport_cost,
  SUM(CASE 
        WHEN n.note_type = 'ATTRACTION' THEN a.cost_value 
        WHEN n.note_type = 'TRANSPORT' THEN td.cost_value
        ELSE 0 
      END) AS total_cost,
  STRING_AGG(DISTINCT CASE 
               WHEN n.note_type = 'ATTRACTION' THEN a.cost_currency::text
               WHEN n.note_type = 'TRANSPORT' THEN td.cost_currency::text
               ELSE NULL
             END, ',') AS currencies
FROM trips t
JOIN notes n ON t.id = n.trip_id
LEFT JOIN attractions a ON n.id = a.note_id AND n.note_type = 'ATTRACTION'
LEFT JOIN transport_details td ON n.id = td.note_id AND n.note_type = 'TRANSPORT'
GROUP BY t.id, t.user_id, t.name, t.start_date, t.stop_date;

CREATE INDEX idx_trip_cost_analysis_user_id ON trip_cost_analysis(user_id);
CREATE INDEX idx_trip_cost_analysis_trip_id ON trip_cost_analysis(trip_id);
CREATE INDEX idx_trip_cost_analysis_dates ON trip_cost_analysis(start_date, stop_date);

-- Widok do harmonogramu wycieczki
CREATE MATERIALIZED VIEW trip_schedule AS
SELECT
  t.id AS trip_id,
  t.name AS trip_name,
  n.id AS note_id,
  n.position,
  n.title,
  n.note_type,
  lower(n.start_date) AS start_time,
  calculate_end_time(n.start_date, n.duration) AS end_time,
  n.duration,
  a.name AS attraction_name,
  l.city,
  COALESCE(a.cost_value, td.cost_value, 0) AS cost
FROM trips t
JOIN notes n ON t.id = n.trip_id
LEFT JOIN attractions a ON n.id = a.note_id AND n.note_type = 'ATTRACTION'
LEFT JOIN transport_details td ON n.id = td.note_id AND n.note_type = 'TRANSPORT'
LEFT JOIN locations l ON a.location_id = l.id
ORDER BY t.id, n.position;

CREATE INDEX idx_trip_schedule_trip_id ON trip_schedule(trip_id);
CREATE INDEX idx_trip_schedule_times ON trip_schedule(start_time, end_time);

-- Widok do statystyk użytkowników
CREATE MATERIALIZED VIEW user_trip_stats AS
SELECT
  t.user_id,
  COUNT(DISTINCT t.id) AS total_trips,
  COUNT(DISTINCT n.id) AS total_notes,
  COUNT(DISTINCT a.id) AS total_attractions,
  AVG(a.rating) AS avg_attraction_rating
FROM trips t
LEFT JOIN notes n ON t.id = n.trip_id
LEFT JOIN attractions a ON n.id = a.note_id
GROUP BY t.user_id;

CREATE INDEX idx_user_trip_stats_user_id ON user_trip_stats(user_id);
```

## 7. Początkowe dane

```sql
-- Początkowe kategorie atrakcji
INSERT INTO attraction_categories (name, description) VALUES 
  ('Muzeum', 'Muzea, galerie i wystawy'),
  ('Zabytek', 'Historyczne budynki, pomniki i miejsca'),
  ('Park', 'Parki, ogrody i tereny zielone'),
  ('Plaża', 'Plaże i miejsca nadmorskie'),
  ('Gastronomia', 'Restauracje, kawiarnie i lokalne przysmaki'),
  ('Wydarzenie kulturalne', 'Koncerty, festiwale i imprezy kulturalne'),
  ('Zakupy', 'Centra handlowe, targi i lokalne sklepy'),
  ('Rozrywka', 'Parki rozrywki, kina i inne atrakcje'),
  ('Sport', 'Aktywności sportowe i rekreacyjne'),
  ('Transport', 'Środki transportu i punkty przesiadkowe');
```

## 8. Uwagi

1. **Skalowalność**:
   - Schemat został zaprojektowany z uwzględnieniem wzrostu danych, z indeksami na najczęściej przeszukiwanych kolumnach.
   - Materialized Views przyspieszają złożone zapytania, szczególnie przy sumowaniu kosztów i statystykach.
   - Dodatkowe indeksy na kolumnach dat umożliwiają szybkie wyszukiwanie po zakresach czasowych.

2. **Bezpieczeństwo**:
   - Row Level Security zapewnia, że użytkownicy mają dostęp tylko do swoich danych.
   - Ograniczenia CHECK zapewniają integralność danych (np. koszty >= 0, oceny 1-10).

3. **Zarządzanie czasem**:
   - Użycie typu TSTZRANGE dla start_date w notatkach umożliwia precyzyjne określenie początku zdarzenia.
   - Typ INTERVAL dla duration umożliwia elastyczne określanie czasu trwania (np. '4 hours', '1 day 2 hours').
   - Funkcja calculate_end_time umożliwia obliczenie czasu zakończenia zdarzenia.
   - Widok trip_schedule zapewnia kompleksowy harmonogram wycieczki z uporządkowanymi zdarzeniami.

4. **Integracja**:
   - Tabela `user_details` jest powiązana z systemem autentykacji Supabase Auth.
   - Planowane eksporty do JSON/PDF są obsługiwane przez strukturę.

5. **Nierozwiązane kwestie**:
   - Implementacja dokładnego algorytmu szacowania dystansu i czasu przejazdu między lokalizacjami będzie wymagać integracji z zewnętrznym API w kodzie aplikacji.
   - Optymalizacja dla bardzo dużej liczby wycieczek może wymagać dodatkowych strategii, takich jak partycjonowanie tabel.
