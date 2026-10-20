# Vulkan C++ Lernprojekt

Ein modernes C++-Grafikprojekt auf Basis des offiziellen [Vulkan Tutorials](https://vulkan.org/learn) (Alexander Overvoorde), das die Low-Level-API von Vulkan von Grund auf implementiert.

---

## 🚀 Bisheriger Stand (Implementierte Features)

Das Projekt wurde schrittweise von Grund auf aufgebaut und deckt mittlerweile folgende Kernkomponenten ab:

* **Initialisierung & Geräte:**
  * Erstellung der Vulkan-Instanz und Konfiguration von Validierungs-Layern (inkl. Debug Messenger) zur Fehlersuche.
  * Auswahl und Validierung geeigneter physischer GPUs sowie Erstellung logischer Geräte.
  * Verwaltung von Queue-Familien (Graphics & Presentation Queues).
* **Fenster & Swapchain:**
  * Plattformunabhängige Fenstererstellung via GLFW und Einbindung der Window System Integration (WSI) über `VkSurfaceKHR`.
  * Vollständige Swapchain-Verwaltung inklusive Format-, Präsentationsmodus- und Extent-Auswahl sowie Image Views und Framebuffers.
  * Robustes Resize-Handling und Neugenerierung der Swapchain bei Fenstergrößenänderungen oder Minimierung.
* **Pipeline & Shader:**
  * Kompilierung von GLSL-Shadern zu SPIR-V-Bytecode.
  * Laden von Shader-Modulen und Konfiguration der Grafik-Pipeline (inkl. Input Assembly, Rasterisierung, Viewports/Scissors, Multisampling und Color Blending).
  * Render-Pass-Konfiguration und Subpass-Abhängigkeiten.
* **Zeichnen & Synchronisation:**
  * Erstellung von Command Pools und Command Buffers.
  * Multi-Buffering ("Frames in Flight") mittels Fences und Semaphoren für eine saubere CPU-GPU-Synchronisation.
  * Geometrie-Rendering (Zeichnen von Dreiecken und Rechtecken).
* **Speicher & Ressourcen:**
  * Effizientes Vertex- und Index-Buffer-Management unter Verwendung von Staging-Buffern und Device-Local Memory.
  * Uniform Buffer Objects (UBOs) für Transformationsmatrizen (Modell-, View-, Projektions-Matrix) inklusive Descriptor Set Layouts, Descriptor Pools und Descriptor Sets.

---

## 📋 Noch Geplante Features & Meilensteine

Die folgenden Abschnitte des Tutorials und erweiterte Features stehen als Nächstes auf der Agenda:

* [ ] **Textur-Mapping:**
  * Laden von Bilddateien (mittels `stb_image`).
  * Erstellung von Vulkan-Images, Image Views und Samplern.
  * Layout-Transitionen (Image Memory Barriers) und Verknüpfung über Combined Image Sampler Descriptors.
* [ ] **Tiefenpufferung (Depth Buffering):**
  * Erstellung und Handhabung eines Depth-Images und -Views für korrektes 3D-Rendering.
* [ ] **Laden von 3D-Modellen:**
  * Integration einer Bibliotheken wie `tinyobjloader` zum Laden externer 3D-Modelle.
  * Vertex-Deduplizierung zur Optimierung des Index-Buffers.
* [ ] **Erweiterte Grafikeffekte:**
  * Mipmap-Generierung für Texturen.
  * Multisampling (MSAA) für Anti-Aliasing.
  * Compute Shaders (z.B. für Partikelsysteme).

---

## 🛠️ Voraussetzungen & Build

* **C++ Compiler** mit C++17 Unterstützung (z.B. GCC 7+, Clang 5+, MSVC 2017+)
* **Vulkan SDK** (LunarG)
* **GLFW** (für das Erstellen des Fensters)
* **GLM** (für Vektor- und Matrizenberechnungen)