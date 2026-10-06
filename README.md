# MLXEdit
Low-Level-Maximalist: Hinterfragt jedes Byte, verweigert Standard-Pfade und holt 90% des theoretischen Hardware-Maximums heraus.
# MLXEdit — MultiLineExtendedEdit

[DEUTSCH]
MLXEdit ist eine ultra-performante, hardware-nahe Text-Editor-Engine, die von Grund auf in C++ geschrieben wurde. Das Projekt verzichtet komplett auf träge Frameworks und kommuniziert direkt mit der Win32-API. Der Fokus liegt auf maximaler CPU-Cache-Effizienz und Echtzeit-Performance-Messung.

## Tech-Highlights & Performance-Kennzahlen
* **Live-Performance-Dashboard:** Die exakten Ausführungszeiten kritischer Operationen werden in Echtzeit direkt in der Fenster-Titelleiste angezeigt.
* **Tipp-Latenz (`OnChar`):** ~1,4 ms — Eingaben fühlen sich absolut verzögerungsfrei an.
* **Massive Pastes (`Paste`):** Schluckt gigantische Textblöcke (wie die massive `sqlite3.c` mit ~9,4 Millionen Zeichen und über 240.000 Zeilen) in gerade einmal ~502 ms.
* **Maus-Positionierung (`WM_LBUTTONDOWN`):** Sub-Millisekunden-Bereich beim mathematischen Auflösen von X/Y-Pixelkoordinaten in die exakte Array-Position.

## Low-Level Architektur-Geheimnisse
1. **64-Byte Cache-Line Alignment:** Die zentrale `LINEDATA`-Struktur ist exakt 64 Byte groß. Dadurch landet bei jedem RAM-Zugriff genau eine vollständige Zeilenstruktur ohne Verschnitt im ultraschnellen L1/L2-Cache der CPU (Keine Cache Line Splits).
2. **STL-Reverse-Trick:** Statt bei Einfügevorgängen Millionen von Elementen träge im Speicher nach hinten zu verschieben, nutzt MLXEdit eine hochoptimierte `std::reverse()`-Spiegelungslogik.
---

[ENGLISH]
MLXEdit is an ultra-high-performance, hardware-aware text editor engine written from scratch in C++. This project completely bypasses heavy frameworks, communicating directly with the Win32 API. It is engineered for maximum CPU cache efficiency and real-time performance telemetry.

## 🚀 Tech Highlights & Performance Metrics
* **Live Performance Dashboard:** Exact execution times for critical operations are measured and displayed in real time directly within the window title bar.
* **Typing Latency (`OnChar`):** ~1.4 ms — input feels instantaneous.
* **Massive Pastes (`Paste`):** Swallows massive text blocks (such as the huge `sqlite3.c` source with ~9.4M characters and over 240,000 lines) in just ~502 ms.
* **Mouse Positioning (`WM_LBUTTONDOWN`):** Sub-millisecond calculation when mapping raw X/Y pixel coordinates to the exact array index.

## Low-Level Architecture Highlights
1. **64-Byte Cache-Line Alignment:** The core `LINEDATA` structure is sized at exactly 64 bytes. This ensures that every memory access fetches precisely one full line structure into the CPU's ultra-fast L1/L2 cache, completely avoiding Cache Line Splits.
2. **The STL Reverse Trick:** Instead of shifting millions of elements backward during a paste operation, MLXEdit utilizes a highly optimized `std::reverse()` mirroring strategy. This converts expensive mid-array insertions into lightning-fast appends.

## Requirements / Voraussetzungen
* Windows OS (Win32 API)
* C++17 Compiler (Visual Studio / MSVC recommended)


## Tech-Highlights & Performance-Kennzahlen
* **Live-Performance-Dashboard:** Die exakten Ausführungszeiten kritischer Operationen werden in Echtzeit direkt in der Fenster-Titelleiste angezeigt.
* **Tipp-Latenz (`OnChar`):** 
  * **~300 µs (Mikrosekunden)** in einer normalen 1,5 MB Datei — absolut jenseits der menschlichen Wahrnehmungsgrenze.
  * **~1,4 ms** selbst am extremen Anfang der gigantischen `sqlite3.c` (~9,4 Mio. Zeichen).
* **Massive Pastes (`Paste`):** Schluckt die massive `sqlite3.c` mit über 240.000 Zeilen in gerade einmal ~502 ms.

---

## Tech Highlights & Performance Metrics
* **Live Performance Dashboard:** Exact execution times for critical operations are measured and displayed in real time directly within the window title bar.
* **Typing Latency (`OnChar`):**
  * **~300 µs (microseconds)** in a standard 1.5 MB file — well beyond the limit of human perception.
  * **~1.4 ms** even at the absolute top of the gigantic `sqlite3.c` (~9.4M characters).
* **Massive Pastes (`Paste`):** Swallows the massive `sqlite3.c` source with over 240,000 lines in just ~502 ms.
