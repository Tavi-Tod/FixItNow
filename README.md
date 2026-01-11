
# 🛠️ FixItNow - Sistem de Gestiune Service Electrocasnice

**FixItNow** este o aplicație complexă C++ (OOP) care simulează activitatea unui service de electrocasnice. Aplicația gestionează angajați, un catalog de aparate și procesează cereri de reparație în timp real, utilizând algoritmi de alocare inteligentă a resurselor.

---

## 🚀 Funcționalități Principale

### 1. 👥 Gestiune Personal (HR)
- **Tipuri de angajați:** Tehnicieni, Recepționeri, Supervizori (ierarhie polimorfică).
- **Calcul Salarial:** Salariu de bază + spor vechime + spor funcție + **bonus de performanță** (2% din reparațiile efectuate de tehnicieni).
- **Competențe:** Tehnicienii au specializări multiple (ex: "Frigider Samsung", "Televizor LG"), încărcate dinamic din fișiere CSV.

### 2. 📺 Gestiune Electrocasnice (Catalog)
- Suport pentru diverse tipuri de aparate: **Frigidere** (cu/fără congelator), **Televizoare** (diagonală), **Mașini de Spălat** (capacitate).
- Gestionarea stocului de modele suportate și afișarea detaliată a specificațiilor.

### 3. ⚙️ Simulare & Load Balancing (Core Feature)
- **Simulare în Timp Real:** Sistemul rulează "ticuri" de timp (1 secundă reală = 1 unitate de timp simulată).
- **Alocare Inteligentă:** Cererile sunt distribuite automat tehnicienilor pe baza unui algoritm complex:
  1. Verifică **competența** tehnică.
  2. Verifică **disponibilitatea** (max 3 sarcini active).
  3. **Load Balancing:** Alege tehnicianul cu cea mai mică încărcare de timp (suma duratelor rămase), nu doar cel cu puține sarcini.
- **Queue Management:** Cererile care nu pot fi preluate rămân în starea `PENDING` și sunt re-evaluate la următorul tic.

### 4. 📊 Raportare
Generare automată de rapoarte în format `.csv`:
- `raport_top_salarii.csv`: Top 3 angajați după venit.
- `raport_top_tehnician.csv`: Performanța tehnicianului cu cea mai grea reparație.
- `raport_asteptare.csv`: Lista cererilor nepreluate, grupate și sortate.
- **Statistici Defecțiuni:** Raport cu aparatele care nu au putut fi reparate (complexitate 0).

---

## 🏗️ Arhitectură și Tehnologii

Proiectul este scris în **Modern C++** și respectă principiile **SOLID**.

### Design Patterns Utilizate
- **Singleton:** Clasa `Service` asigură o instanță unică a controller-ului principal.
- **Factory Method:** Clasa `AngajatFactory` gestionează crearea dinamică a tipurilor de angajați pe baza datelor din fișiere.

### Elemente Tehnice
- **STL (Standard Template Library):** Utilizare extensivă de `std::vector`, `std::map` (pentru statistici), `std::sort` cu funcții lambda.
- **RTTI (Run-Time Type Information):** Utilizarea `dynamic_cast` pentru gestionarea polimorfismului (ex: atribuirea competențelor doar tehnicienilor).
- **Multi-threading:** Utilizarea `std::this_thread::sleep_for` și `std::chrono` pentru simularea vizuală a timpului.
- **Robust Parsing:** Citirea fișierelor CSV cu gestionarea erorilor (`try-catch`) pentru a preveni oprirea aplicației la date corupte.

---

## 📂 Structura Proiectului

```text
├── src/
│   ├── main.cpp            # Punctul de intrare
│   ├── service.cpp/.h      # Logică Singleton & Simulare
│   ├── menu.cpp/.h         # Interfața cu utilizatorul
│   ├── angajat.cpp/.h      # Clasa de bază Angajat
│   ├── tehnician.cpp/.h    # Derivată Tehnician
│   ├── ... (alte clase derivate)
│   ├── utils.cpp/.h        # Funcții auxiliare (CNP, Split, Time)
│   └── raport_generator... # Logică scriere CSV
├── tests/
│   ├── angajati.csv        # Baza de date inițială (50 angajați)
│   └── cereri.txt          # Scenariu de test (200 cereri)
└── README.md

```

---

## 💻 Cum se rulează

### 1. Compilare

Proiectul nu are dependențe externe. Se poate compila cu orice compiler standard C++ (G++, Clang, MSVC).

**Exemplu (Terminal/Linux/MacOS):**

```bash
g++ *.cpp -o fixitnow

```

### 2. Rulare

Asigurați-vă că folderul `tests/` conține fișierele `angajati.csv` și `cereri.txt` în același director cu executabilul.

```bash
./fixitnow

```

---

## 🧪 Testare

Proiectul include un set de date pentru **Stress Test** în folderul `tests/`:

* **50 Angajați:** Acoperă toate rolurile și o gamă largă de competențe pentru tehnicieni.
* **200 Cereri:** Include cazuri valide, aparate nereparabile (Complexitate 0) și linii invalide pentru testarea parser-ului.

Pentru a rula testul:

1. Porniți aplicația.
2. Datele se încarcă automat la pornire.
3. Selectați opțiunea **3 (Simulare)** din meniu.
4. Introduceți un număr de ticuri (ex: 50) pentru a vedea cum sunt procesate cele 200 de cereri.

---

## 📝 Autor

**Nume:** Toderașc Octavian-Gabriel

**Grupa:** 323AA

Proiect realizat pentru cursul de Programare Orientată pe Obiecte (POO), 2026.

```

```
