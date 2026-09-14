# website/ — strona produktowa GS1 ScanVortex

Mała strona produktowa z podstroną polityki prywatności. Statyczny HTML + CSS,
**bez frameworka, bez JavaScriptu, bez czcionek z CDN, bez analityki i trackerów**.
Jedyne odwołania na zewnątrz to linki, które użytkownik może kliknąć: Google Play,
polityka prywatności Google i adres e‑mail.

## Struktura

```
website/
├─ index.html            strona główna (PL)
├─ privacy.html          polityka prywatności (PL)  ← ADRES DLA GOOGLE PLAY
├─ en/
│  ├─ index.html         strona główna (EN)
│  └─ privacy.html       polityka prywatności (EN)
├─ assets/
│  ├─ style.css          jeden arkusz dla wszystkich podstron
│  └─ favicon.svg        favicon (kod kreskowy z linią skanowania)
└─ README.md
```

## Nazewnictwo — reguła, której nie wolno złamać

| Rola | Nazwa | Pokazywane na stronie |
|---|---|---|
| Produkt, marka, podmiot polityki prywatności | **GS1 ScanVortex** | tak |
| Nazwa listingu w Google Play | **GS1 Scanner & Generator** | tak |
| Identyfikator pakietu | `com.scanvertex.gs1` | **nie** — tylko w adresie odnośnika do sklepu |

Obie nazwy występują na stronie **równolegle**: marka w nagłówkach i treści, nazwa
sklepowa jako informacja „w Google Play dostępna jako…". Nazwa sklepowa **nie jest**
przedstawiana jako druga nazwa techniczna produktu, a marka **nie jest** zastępowana
nazwą sklepową. Podstrona polityki prywatności niesie obie w wydzielonym bloku
identyfikacji, żeby powiązanie było jednoznaczne dla Google Play.

**Strona nie podaje numeru wersji ani identyfikatora pakietu** i nie wolno ich dokładać.
Strona opisuje produkt, a nie konkretny build: gdyby niosła `versionCode` albo numer
wydania, każda publikacja w Google Play wymuszałaby jej aktualizację, a pierwsze
przeoczenie zamieniłoby ją w źródło nieprawdy. Aktualizujemy ją wtedy, gdy zmienia się
aplikacja — funkcje, uprawnienia, treść polityki — a nie wtedy, gdy zmienia się numer.

Forma **„ScanVertex"** (przez „e") nie występuje w treści strony. Pojawia się wyłącznie
wewnątrz identyfikatora pakietu `com.scanvertex.gs1`, bo to rzeczywisty identyfikator
aplikacji i nie wolno go zmienić.

## Skąd pochodzi treść polityki — i czego NIE WOLNO zrobić

Tekst polityki **nie został napisany na potrzeby strony**. Pochodzi w całości z zasobu
`PrivacyBody` w `Resources/Languages/AppResources.pl.resx`
i `Resources/Languages/AppResources.resx` — z tego samego ciągu, który aplikacja
pokazuje w nakładce prawnej przy pierwszym uruchomieniu oraz w
**Ustawienia → Polityka prywatności**.

Zgodność jest mierzona znak po znaku: po usunięciu znaczników `[b]`/`[url]`/`[email]`
i normalizacji odstępów tekst zasobu i tekst podstrony są **identyczne**
(3076 znaków PL, 2928 znaków EN). Zmieniona jest wyłącznie prezentacja: nagłówki
sekcji, spis treści, typografia i blok identyfikacji produktu.

> **Zmieniając politykę prywatności, zmień OBA miejsca.** Rozjazd między tym, co widzi
> użytkownik w aplikacji, a tym, co stoi pod publicznym adresem podanym w Google Play,
> jest problemem prawnym, nie kosmetycznym.

Podstrony polityki powstały skryptem czytającym `PrivacyBody`. Skrypt **nie jest**
częścią repozytorium — jeżeli okaże się, że politykę zmieniamy częściej niż raz na
wydanie, warto dołożyć go do `tools/`, żeby synchronizacja przestała zależeć od pamięci.

## Hosting

Strona nie wymaga builda ani środowiska uruchomieniowego — wystarczy wystawić katalog
jako pliki statyczne. Adres do podania w Google Play Console to **`…/privacy.html`**.

**Uwaga bezpieczeństwa:** tego repozytorium nie wolno upublicznić — w historii gita
znajduje się keystore i hasło podpisu (ustalenie `SEC‑01` w `CLAUDE.md`), a przyjęte
tam ryzyko opiera się wyłącznie na prywatności repozytorium. Stronę należy więc wystawić
z osobnego publicznego repozytorium albo z hostingu plików statycznych.

## Czego na stronie świadomie nie ma

- **Etykiet PDF i druku** — w wydaniu Release są ukryte (`AppConfig.LabelsExposed`,
  `KD‑68`), więc reklamowanie ich byłoby obietnicą funkcji, której użytkownik nie dostanie.
- **Deklaracji zgodności ze standardem, certyfikacji i weryfikacji jakości druku** —
  aplikacja tego nie robi i strona mówi o tym wprost w sekcji o GS1.
- **Numeru wersji i identyfikatora pakietu** — powód wyżej.
- **Nazwy administratora danych** — tekst polityki mówi o „Twórcy" i podaje adres
  kontaktowy, ale nie wskazuje podmiotu z nazwy; nie dopisano jej, bo byłoby to
  oświadczenie prawne wymyślone poza źródłem.
