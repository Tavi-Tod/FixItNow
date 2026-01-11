🛠️ FixItNow - Sistem de Gestiune Service Electrocasnice

FixItNow este o aplicație complexă dezvoltată în Modern C++ care simulează activitatea unui service de electrocasnice. Proiectul demonstrează utilizarea principiilor OOP, SOLID și a Design Patterns pentru a gestiona un flux de lucru în timp real.

🚀 Funcționalități Cheie

1. 👥 Gestiune Resurse Umane (HR)

Polimorfism: Ierarhie de clase pentru Tehnician, Receptioner, Supervizor derivate din clasa abstractă Angajat.

Salarizare Dinamică: - Salariu de bază + Spor vechime + Spor funcție.

Bonus de Performanță: Tehnicienii primesc automat 2% din valoarea fiecărei reparații finalizate.

Competențe Tehnice: Tehnicienii au o listă de specializări (ex: "Frigider Samsung", "Televizor LG"), încărcate dinamic din CSV (format Competenta1|Competenta2).

2. 📺 Catalog Electrocasnice

Suport pentru diverse tipuri de echipamente, fiecare cu atribute specifice:

Frigidere: (Congelator Da/Nu)

Televizoare: (Diagonala)

Mașini de Spălat: (Capacitate cuvă)

Validare automată a cererilor în funcție de modelele existente în catalog.

3. ⚙️ Simulare & Load Balancing (Core Engine)

Sistemul rulează o simulare bazată pe "ticuri" de timp (1 secundă reală = 1 unitate de timp simulată).

Algoritm de Alocare Inteligentă:
Cererile nu sunt distribuite aleatoriu, ci pe baza unui scor de optimizare:

Competență: Tehnicianul trebuie să știe să repare Marca și Tipul aparatului.

Disponibilitate: Maxim 3 sarcini simultane per tehnician.

Time-Based Load Balancing: Dintre candidații eligibili, este ales cel cu cea mai mică încărcare totală de timp (suma orelor rămase de muncă), asigurând o distribuție echitabilă a efortului.

Queue Management: Cererile care nu pot fi preluate imediat rămân în starea PENDING și sunt re-procesate la fiecare tic.

4. 📊 Raportare Avansată

Generare de rapoarte CSV pentru analiză:

raport_top_salarii.csv: Top 3 angajați, ordonați după venit (include bonusurile acumulate).

raport_top_tehnician.csv: Tehnicianul care a gestionat cea mai complexă reparație.

raport_asteptare.csv: Lista cererilor în așteptare, grupate pe categorii și sortate alfabetic.

Istoric Reparații: Vizualizarea aparatelor reparate cu succes și a celor declarate INVALID (nereparabile).

🏗️ Arhitectură și Tehnologii

Proiectul este construit modular, respectând standardele C++11/14.

Design Patterns

Singleton: Clasa Service acționează ca un controller unic care gestionează starea globală a aplicației.

Factory Method: Clasa AngajatFactory abstractizează crearea instanțelor de angajați, permițând extensibilitatea ușoară a tipurilor de personal.

Elemente Tehnice

STL Containers: Utilizare extensivă de std::vector, std::map (pentru statistici de frecvență), std::pair.

Lambda Expressions: Folosite pentru algoritmi de sortare complecși (criterii multiple).

RTTI (dynamic_cast): Identificarea tipului de angajat la runtime pentru atribuirea sarcinilor specifice.

Multi-threading: Utilizarea std::this_thread::sleep_for pentru a crea efectul de simulare în timp real.

Robust Parsing: Citirea fișierelor este protejată la erori; liniile corupte sunt raportate în consolă fără a opri execuția programului (try-catch blocks).

📂 Structura Fișierelor

FixItNow/
├── main.cpp                # Punctul de intrare
├── service.cpp/.h          # Logică Singleton & Simulare
├── menu.cpp/.h             # Interfața utilizator (Consolă)
├── angajat_factory.cpp/.h  # Design Pattern Factory
├── raport_generator.cpp/.h # Logică generare CSV
├── Entitati/
│   ├── angajat.cpp/.h      # Clasa de bază
│   ├── tehnician.cpp/.h    # Derivată
│   ├── receptioner.cpp/.h  # Derivată
│   ├── supervizor.cpp/.h   # Derivată
│   ├── electrocasnic.cpp/.h 
│   └── cerere_reparatie.cpp/.h
├── Utils/
│   └── utils.cpp/.h        # Validare CNP, String Split, Timestamp
└── tests/                  # Folder obligatoriu pentru rulare
    ├── angajati.csv        # Baza de date inițială (50+ angajați)
    ├── cereri.txt          # Scenariu de test (200+ cereri)
    └── README.md           # Documentația testelor


💻 Instrucțiuni de Rulare

1. Compilare

Proiectul nu are dependențe externe. Se poate compila cu orice compiler standard C++ (G++, Clang, MSVC).

Comandă (Terminal):

g++ *.cpp -o fixitnow


2. Rulare

Asigurați-vă că folderul tests/ este prezent în același director cu executabilul și conține fișierele de date.

Windows:

fixitnow.exe


Linux/MacOS:

./fixitnow


🧪 Scenariu de Test (Stress Test)

Proiectul vine pre-configurat cu un set masiv de date în folderul tests/ pentru a demonstra stabilitatea:

50 Angajați: Inclusiv 40 de tehnicieni cu diverse competențe.

200 Cereri: Un mix de cereri valide, cereri imposibil de reparat (Complexitate 0) și date eronate pentru testarea parser-ului.

Cum să testați:

Porniți aplicația.

Alegeți opțiunea 3 (Simulare) din meniu.

Introduceți un număr de ticuri (ex: 60) și urmăriți în consolă cum cele 200 de cereri sunt alocate dinamic tehnicienilor.

📝 Autor

Student: [Numele Tau]

Grupa: [Grupa Ta]

Proiect realizat pentru cursul de **Programare Orientată pe Obiecte
