# Whale Activity Index (WAI)

## Überblick
Der **Whale Activity Index (WAI)** ist ein Open-Source-On-Chain-Indikator, der darauf ausgelegt ist, ungewöhnliche Aktivitäten großer Bitcoin-Marktteilnehmer („Wale“) zu quantifizieren.  
Er transformiert rohe Blockchain-Daten in einen robusten, normalisierten Index von **0 bis 100** und ermöglicht so einen konsistenten Vergleich über verschiedene Marktphasen hinweg.

---

## Motivation
Einfache On-Chain-Metriken wie die reine Transaktionsanzahl oder das Volumen leiden oft unter mangelndem historischem Kontext und einer hohen Anfälligkeit für Ausreißer.  

Der WAI löst diese Probleme, indem er die **relative Aktivität** anstelle von Absolutwerten misst und adaptive Normalisierungen sowie Gewichtungen anwendet.

---

## Methodik (High-Level)

### Eingangsmetriken
* **Whale Transaction Count:** Anzahl der Wal-Transaktionen.
* **Whale Transaction Volume (BTC):** Volumen der Wal-Transaktionen in BTC.  
Die Daten werden auf täglicher Basis aggregiert.

### Adaptive Normalisierung
Die Metriken werden gegen eine rollierende Baseline (SMA, EWMA oder Median) normalisiert, um langfristige Trends und strukturelle Marktveränderungen zu berücksichtigen.

### Volatilitätsadaptive Gewichtung
Die Gewichtung der einzelnen Metriken wird dynamisch an die beobachtete Volatilität angepasst. Dies reduziert das Rauschen durch instabile Eingabedaten (z. B. extreme Volumenspitzen).

### Historische Skalierung
Der kombinierte Aktivitätswert wird über ein rollierendes Perzentil-Fenster eingestuft und linear auf den Bereich [0, 100] skaliert. Dies gewährleistet eine interpretationsfähige Kennzahl, die unabhängig vom aktuellen Marktregime funktioniert.

---

## Interpretation

| WAI Bereich | Interpretation |
| :--- | :--- |
| **0–20** | Sehr geringe Wal-Aktivität |
| **20–40** | Unterdurchschnittlich |
| **40–60** | Normalbereich |
| **60–80** | Erhöhte Aktivität |
| **80–100** | Extreme, seltene Aktivität |

> **Hinweis:** Der WAI ist ein Kontext-Indikator, kein eigenständiges Handelssignal.

---

## Architektur (Konzeptuell)
* **Collector Service:** Extrahiert und aggregiert Wal-Transaktionen von der Blockchain.
* **Backend API:** Berechnet den WAI, verwaltet die Historie und stellt Parameter bereit.
* **Visualization Layer:** Dashboards und Charts zur grafischen Aufbereitung.

Alle Komponenten sind modular aufgebaut und containerisiert.

---

## Umfang & Grenzen
* Misst die **Aktivität**, nicht die Preisrichtung.
* Keine Vorhersagegarantien.
* Die Parameterwahl ist empirisch motiviert.
* Reduzierte statistische Aussagekraft in frühen Datenfenstern.

---

## Open Source
Der WAI ist vollständig Open Source und auf Auditierbarkeit, Erweiterbarkeit sowie für den akademischen und praktischen Einsatz ausgelegt.

---

## Status
* **Index-Spezifikation:** Stabil
* **Backend:** Einsatzbereit
* **Validierung & Erweiterungen:** Laufend
