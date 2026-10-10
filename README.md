# MLXEdit
Low-Level-Maximalist: Hinterfragt jedes Byte, verweigert Standard-Pfade und holt 90% des theoretischen Hardware-Maximums heraus.
# MLXEdit — MultiLineExtendedEdit

[DEUTSCH]
* **Native Unicode-Engine:** MLXEdit wird ausschließlich für **UNICODE (`wchar_t` / UTF-16)** kompiliert. Es kommuniziert ohne Performance-Verluste direkt mit den nativen Wide-Character-Schnittstellen der Win32-API (Keine trägen String-Konvertierungen im Hintergrund).
* **Hinweis zur Integration:** MLXEdit ist von Grund auf als hochperformantes Unterprogramm (Core Engine) für ein übergeordnetes **Datenbankprogramm** konzipiert. Die vollständige Steuerung (wie das Laden/Speichern von Dateien und die Menüführung) wird nativ im Hauptprogramm verankert. Aus diesem Grund sind diese Benutzeroberflächen-Elemente in diesem isolierten Performance-Release bewusst nicht implementiert.

[ENGLISH]
* **Native Unicode Engine:** MLXEdit is compiled exclusively for **UNICODE (`wchar_t` / UTF-16)**. It communicates directly with the native wide-character interfaces of the Win32 API, eliminating any hidden string conversion overhead.
* **Integration Note:** MLXEdit is engineered from the ground up to serve as an ultra-high-performance sub-component (core engine) embedded within a larger **database application**. All high-level control flows (such as file I/O operations and menu navigation) are natively handled by the main host application. Consequently, these UI elements are intentionally omitted from this standalone performance showcase.



## ⚠️ Antivirus Note / Hinweis zu Virenscannern
[DEUTSCH]
Da diese Engine ohne typischen Framework-Ballast direkt mit der Win32-API kommuniziert und bei großen Dateien (ab 131.072 Zeilen) alle CPU-Kerne über hocheffizientes Multithreading voll auslastet, schlagen einige Virenscanner aufgrund dieser unüblichen Verhaltens-Heuristik (False Positive) an. Die Standalone-EXE ist absolut sauber und sicher.

[ENGLISH]
Because this engine communicates directly with the Win32 API without heavy framework bloat and utilizes high-efficiency multithreading across all CPU cores for large files (above 131,072 lines), some antivirus scanners may trigger a false positive based on behavioral heuristics. The standalone EXE is completely clean and safe.


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

## 🕹️ Quick Start / Bedienung
[DEUTSCH]
Da sich MLXEdit aktuell in der Core-Entwicklungsphase befindet, besitzt das erste Release kein klassisches Datei-Menü. Sie können die Engine wie folgt testen:
1. Öffnen Sie MLXEdit.
2. Kopieren Sie einen beliebigen Text (für den Härtetest eine große Datei wie `sqlite3.c` mit Strg+A und Strg+C).
3. Fügen Sie den Text per **Strg+V (Paste)** in MLXEdit ein und beobachten Sie die Zeitmessung in der Titelleiste!
4. Tippen Sie Text ein oder klicken Sie mit der Maus, um die Sub-Millisekunden-Latenzen live zu sehen.

## Bedienungshinweise & Features

### Multiblock-Funktionen (Mehrfachauswahl)
MLXEdit unterstützt fortschrittliche Multiblock-Operationen, mit denen Sie mehrere Textblöcke gleichzeitig bearbeiten können:
* **Auswahl & Zwischenablage:** Wählen Sie mehrere separate Textblöcke mit der Maus aus. Diese können gemeinsam in die Zwischenablage kopiert werden.
* **Einfügen(Einzeln):** Ersetzen Sie einzelne markierte Blöcke gezielt über das Kontextmenü mit den Daten aus der Zwischenablage.
* **Einfügen(Global):** Nutzen Sie `Strg + V`, um alle ausgewählten Blöcke im aktuellen Sichtbereich (Scope) gleichzeitig durch den Inhalt der Zwischenablage zu ersetzen.
* **Löschen:** Die `Entf`-Taste (Delete) löscht alle aktuell ausgewählten Blöcke gleichzeitig oder individuell mit Kontextmenu.

### Suchfunktion
* **Suchen:** Markieren Sie einfach ein Wort mit der Maus, machen Sie einen Rechtsklick und wählen Sie im Kontextmenü **„Suchen“**.
* **Fundliste zurücksetzen:** Die optisch hervorgehobenen Suchergebnisse können Sie jederzeit über den Kontextmenü-Eintrag **„Fundliste leeren“** wieder entfernen.

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

## Usage Notes & Features

[ENGLISH]
Since MLXEdit is currently in its core development phase, this initial release does not feature a traditional file menu. You can test the engine's raw performance using these steps:
1. Launch MLXEdit.
2. Copy any text (for a true stress test, copy a massive file like `sqlite3.c` using Ctrl+A and Ctrl+C).
3. Press **Ctrl+V (Paste)** inside MLXEdit and watch the execution time explode in the title bar!
4. Type freely or click around with your mouse to observe the sub-millisecond latencies live.


### Multiblock Operations (Multiple Selection)
MLXEdit supports advanced multi-block editing, allowing you to manipulate multiple text selections simultaneously:
* **Selection & Clipboard:** Select multiple separate blocks of text using your mouse and copy them all to the clipboard at once.
* **Paste / Replace (Individual):** Replace specific selected blocks one by one using the context menu and clipboard data.
* **Paste / Replace (Global):** Press `Ctrl + V` to globally replace all selected blocks within the current scope with your clipboard content.
* **Delete:** Press the `Delete` key (Entf) to clear all currently selected blocks simultaneously, or remove them individually using the context menu.


### Search Tool
* **Search:** Simply highlight a word with your mouse, right-click, and select **"Suchen"** (Search) from the context menu.
* **Clear Highlights:** You can easily remove all highlighted search results at any time by selecting **"Fundliste leeren"** (Clear search results) from the context menu.


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
