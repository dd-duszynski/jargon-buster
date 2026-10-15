---
project: "jargon-buster"
version: 1
status: draft
created: 2026-10-14
context_type: greenfield
product_type: web-app
target_scale:
  users: small
timeline_budget:
  mvp_weeks: 8
  hard_deadline: 2026-12-06
  after_hours_only: true
---

# PRD: jargon-buster

## Vision & Problem Statement

Samoucy i inżynierowie eksplorujący nowe dziedziny nauki i technologii zderzają się z barierą hermetycznego żargonu w źródłach akademickich i na Wikipedii, a doraźne korzystanie z ogólnych asystentów AI wymaga każdorazowego, żmudnego instruowania o poziom trudności i analogie. Dodatkowo ogólne wyszukiwarki i modele mieszają konteksty przy hasłach wieloznacznych (np. port, wektor, transformator) oraz rzucają użytkownika na głęboką wodę bez wskazania pojęć elementarnych, bez których zrozumienie zaawansowanego zagadnienia jest niemożliwe.

Rozwiązaniem jest aplikacja wymuszająca rygor Metody Feynmana: trójstopniową progresję poznawczą (od intuicyjnej metafory dla 10-latka, przez inżynierię praktyczną, po formalizm akademicki) poprzedzoną obowiązkowym krokiem ujednoznacznienia dziedziny oraz grafem pojęć bazowych. Połączenie ustrukturyzowanego szablonu z leniwym dociąganiem warstwy akademickiej i globalnym rejestrem wiedzy gwarantuje natychmiastowe budowanie zrozumienia przy minimalnym koszcie zewnętrznym.

## User & Persona

### Primary Persona
- **Nazwa roli:** Dociekliwy inżynier / samouk (self-directed technical learner).
- **Kontekst:** Doświadczony technicznie specjalista, który regularnie wchodzi w obce dla siebie domeny naukowe (fizyka, chemia, biologia) lub technologiczne (sieci, architektura, niskopoziomowe systemy) i potrzebuje szybko zbudować solidną intuicję mentalną.
- **Moment sięgnięcia po narzędzie:** Trafienie na nowe, niezrozumiałe pojęcie w artykule, dokumentacji lub rozmowie, gdy Wikipedia jest zbyt sucha i formalna, a ogólny czat generuje nieuporządkowaną ścianę tekstu.

## Success Criteria

### Primary
- Użytkownik wpisuje pojęcie naukowe lub techniczne, wybiera właściwą dziedzinę (w przypadku wieloznaczności) i otrzymuje precyzyjną analogię ze świata codziennego (Poziom I) oraz zastosowanie praktyczne/inżynieryjne (Poziom II) w czasie poniżej 3 sekund (dla wcześniej opracowanych haseł natychmiastowo).

### Secondary
- Użytkownik może jednym kliknięciem zakładki doczytać Poziom III (formalno-akademicki), zapisać opracowane pojęcie do tematycznej kolekcji oraz jednym kliknięciem przejść do wyjaśnienia pojęcia bazowego z wygenerowanego grafu wymagań wstępnych.

### Guardrails
- Żadne zapytanie nie generuje nowego kosztu zewnętrznego, jeśli tożsame pojęcie w danej dziedzinie zostało już wcześniej opracowane i zapisane w rejestrze wiedzy.
- Pojęcia o wieloznacznym charakterze nigdy nie generują definicji przed jawnym ujednoznacznieniem dziedziny przez użytkownika.
- Awarie sieci lub niedostępność zewnętrznych usług nie przerywają sesji użytkownika i prezentują przejrzysty komunikat o błędzie z możliwością ponowienia.

## User Stories

### US-01: Wyjaśnienie pojęcia wieloznacznego w rygorze Metody Feynmana
- **Given** Zalogowany użytkownik na ekranie głównym aplikacji z polem wyszukiwania
- **When** Wpisuje hasło wieloznaczne (np. „Port”) i wybiera dziedzinę techniczną („Sieci komputerowe”) w kroku ujednoznacznienia
- **Then** Otrzymuje wyrenderowane wyjaśnienie Poziomu I (metafora codzienna) i Poziomu II (praktyka inżynieryjna), listę pojęć bazowych (np. „Adres IP”, „Gniazdo sieciowe”) oraz zakładkę umożliwiającą leniwe dociągnięcie Poziomu III

#### Acceptance Criteria
- Czas do wyświetlenia Poziomu I i II wynosi < 3 s przy nowym zapytaniu i < 500 ms przy pojęciu wcześniej opracowanym.
- Krok ujednoznacznienia blokuje dalsze generowanie dopóki użytkownik nie wskaże dziedziny.
- Pojęcia bazowe są klikalne i natychmiast uruchamiają proces wyjaśniania wybranego pojęcia podrzędnego.

## Functional Requirements

### Uwierzytelnianie i profil użytkownika
- FR-001: Użytkownik może zarejestrować się i zalogować przez email/hasło lub zewnętrznego dostawcę tożsamości (OAuth). Priority: must-have
  > Socrates: Brak kontrargumentu; zostaje w obecnym brzmieniu.

- FR-002: Użytkownik może przeglądać oraz usuwać wpisy ze swojej osobistej historii wyszukiwań. Priority: must-have
  > Socrates: Rozważono ryzyko zaśmiecenia i obaw o prywatność. Rozstrzygnięcie: użytkownik otrzymuje możliwość usuwania pojedynczych zapytań lub wyczyszczenia całej historii.

### Wyszukiwanie i detekcja wieloznaczności
- FR-003: Użytkownik może wprowadzić pojęcie naukowe lub techniczne do wyjaśnienia. Priority: must-have
  > Socrates: Rozważono ryzyko wpisywania całych zdań/pytań utrudniających deduplikację. Rozstrzygnięcie: normalizacja wejścia (usuwanie białych znaków, małe litery) oraz weryfikacja zwięzłości hasła.

- FR-004: Użytkownik musi wybrać dziedzinę pojęcia w dedykowanym kroku ujednoznacznienia (disambiguation), jeśli termin posiada wiele znaczeń. Priority: must-have
  > Socrates: Brak kontrargumentu; krok wyboru dziedziny to rdzenny wyróżnik aplikacji zapobiegający pomyłkom kontekstowym.

### Silnik Feynmana i graf wiedzy
- FR-005: Użytkownik otrzymuje wyjaśnienie Poziomu I (metafora ze świata codziennego, zero żargonu) oraz Poziomu II (praktyka inżynieryjna i biznesowa). Priority: must-have
  > Socrates: Rozważono ryzyko spłycania trudnych pojęć przez metaforę dla 10-latka. Rozstrzygnięcie: Poziom I służy jedynie szybkiej intuicji, a rygor merytoryczny natychmiast dopełnia Poziom II i III.

- FR-006: Użytkownik może leniwie wywołać wygenerowanie i wyświetlenie Poziomu III (formalizm akademicki i aparat pojęciowy) poprzez kliknięcie dedykowanej zakładki. Priority: must-have
  > Socrates: Rozważono dodatkowy stan ładowania w UI. Rozstrzygnięcie: czytelny indykator postępu i natychmiastowa dostępność Poziomów I i II gwarantują brak poczucia bezczynności.

- FR-007: Użytkownik widzi listę pojęć bazowych („Wymagania wstępne”) i może jednym kliknięciem przejść do wyjaśnienia wybranego pojęcia. Priority: must-have
  > Socrates: Brak kontrargumentu; tworzy naturalną ścieżkę edukacyjną rodzic-dziecko.

- FR-008: Użytkownik może zażądać alternatywnej analogii dla Poziomu I na żądanie. Priority: nice-to-have
  > Socrates: Brak kontrargumentu; pozostaje jako nice-to-have omijające rejestr na życzenie użytkownika.

### Rejestr wiedzy i organizacja danych
- FR-009: Użytkownik otrzymuje natychmiastową definicję z globalnego rejestru wiedzy, jeśli para (hasło, dziedzina) została już wcześniej opracowana. Priority: must-have
  > Socrates: Brak kontrargumentu; krytyczny element ochrony budżetu i szybkości odpowiedzi.

- FR-010: Użytkownik może zapisywać wyjaśnione pojęcia w autorskich, jednopoziomowych kolekcjach/folderach tematycznych. Priority: must-have
  > Socrates: Rozważono narzut CRUD-owy. Rozstrzygnięcie: zachowanie płaskiej struktury kolekcji/tagów bez wielopoziomowego zagnieżdżania.

## Non-Functional Requirements

- **Integralność wiedzy:** Każde zapytanie ma przypisaną dokładnie jedną zweryfikowaną dziedzinę; brak możliwości wygenerowania wyjaśnienia w zawieszeniu kontekstowym lub przy niejednoznacznym haśle.
- **Prywatność danych:** Prywatna historia wyszukiwań oraz autorskie kolekcje użytkownika są w 100% odizolowane i niedostępne dla innych kont; usunięcie hasła z historii trwale usuwa rekord z profilu użytkownika.
- **Wydajność i percepcja:** Dla wcześniej opracowanych haseł użytkownik otrzymuje definicję w czasie < 500 ms; przy generowaniu nowej definicji pierwsze informacje zwrotne pojawiają się w < 1 s, a Poziomy I i II są w pełni czytelne w czasie < 3 s p95.
- **Dostępność i urządzenia:** Pełna responsywność interfejsu (desktop i urządzenia mobilne) zachowana na dwóch ostatnich głównych wydaniach popularnych przeglądarek internetowych.

## Business Logic

Aplikacja przekształca pojęcie techniczne lub naukowe w trzystopniową drabinę poznawczą Feynmana oraz graf pojęć elementarnych, wymuszając jednoznaczność dziedziny i serwując definicje z globalnego rejestru wiedzy.

Reguła operacyjna przyjmuje jako wejście ciąg znaków reprezentujący poszukiwane pojęcie. Jeśli termin występuje w wielu odrębnych dziedzinach wiedzy (np. fizyka, programowanie, żegluga), system wstrzymuje proces wyjaśniania i wymusza na użytkowniku wskazanie jednej, konkretnej domeny. Dopiero jednoznaczna para (pojęcie, dziedzina) stanowi klucz wyszukiwania.

Dla zatwierdzonego klucza aplikacja w pierwszej kolejności sprawdza obecność definicji w globalnym rejestrze. W przypadku braku wpisu tworzona jest struktura trójpoziomowa: Poziom I (obrazowa analogia ze świata codziennego), Poziom II (konkretne zastosowanie inżynieryjne lub biznesowe) oraz Poziom III (formalna definicja akademicka). Równolegle wyodrębniane są pojęcia elementarne tworzące graf wymagań wstępnych („zanim zrozumiesz X, poznaj Y i Z”). Użytkownik otrzymuje natychmiast poziomy I i II, podczas gdy poziom III pozostaje w stanie uśpionym do momentu jawnego zażądania przez użytkownika.

## Access Control

- **Model użytkownika:** Płaski model uprawnień. Każdy zarejestrowany użytkownik ma takie same uprawnienia w systemie; brak ról administracyjnych w MVP.
- **Uwierzytelnianie:** Standardowe logowanie (kombinacja email + hasło lub dostawca tożsamości OAuth) oraz rejestracja nowego konta.
- **Izolacja danych:** Każdy użytkownik ma wyłączny, odizolowany dostęp do swojej historii wyszukiwań, zakładek i autorskich kolekcji/folderów haseł.
- **Dostęp publiczny vs chroniony:**
  - Niezalogowany gość próbujący wejść w chronione zasoby (historia, kolekcje) jest przekierowywany do ekranu logowania/rejestracji.
  - Wyjaśnienia haseł i globalny rejestr definicji są odpytywane w ramach uwierzytelnionej sesji.

## Non-Goals

### Funkcjonalne cele wykluczone (Functional non-goals)
- **Brak modułu społecznościowego „Explore”:** Aplikacja w MVP nie udostępnia publicznego katalogu opracowań ani mechanizmów dzielenia się hasłami między użytkownikami (priorytetem jest prywatne narzędzie nauki).
- **Brak eksportu do binariów / Anki:** MVP nie generuje plików PDF ani paczek `.apkg` pod fiszki Anki (uniknięcie skomplikowanych parserów binarnych w przeglądarce).
- **Brak współdzielonych folderów i ról zespołowych:** System nie wspiera workspace'ów wieloosobowych ani udostępniania kolekcji (prosty model pojedynczego użytkownika).
- **Brak własnego/lokalnego modelu inferencyjnego:** Aplikacja nie hostuje modeli na własnej infrastrukturze, lecz korzysta z zewnętrznych usług modeli językowych.

### Niefunkcjonalne cele wykluczone (Non-functional non-goals)
- **Brak trybu offline-first:** Aplikacja nie działa w trybie pełnej gotowości bez połączenia sieciowego (wymagane stałe połączenie do bazy danych i usług zewnętrznych).

## Open Questions

1. **Jaki zestaw domyślnych kategorii/dziedzin będzie predefiniowany w kroku disambiguation?** — Owner: dev / sesja implementacyjna. Status: do rozstrzygnięcia przed opracowaniem promptów.
2. **Jaka jest maksymalna liczba pojęć bazowych (prerequisites) generowanych per hasło?** — Sugestia: 2–4 pojęcia kluczowe, aby zachować czytelność widoku.
