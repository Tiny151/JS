# Bezugspreis-Kalkulation (Dentaldepot GmbH)

Dieses Projekt enthält die JavaScript-Funktion `calculateBezugspreis`, mit der der **Bezugspreis (Einstandspreis)** für puderfreie Nitrilhandschuhe nach dem kaufmännischen Kalkulationsschema automatisch berechnet werden kann. Grundlage ist das Angebot der **Dentaldepot GmbH** (Aufgabe 1.4 – *Bereich Praxisorganisation und -verwaltung*).

## Angebotskonditionen

* **Listenpreis:** 14,95 € pro Box (zzgl. 19 % MwSt.)
* **Staffelrabatt:**
  * ab 10 Boxen: 5 %
  * ab 40 Boxen: 10 %
  * ab 200 Boxen: 20 %
* **Skonto:** 2 % bei Zahlung innerhalb von 10 Tagen (Zahlungsziel: 30 Tage)
* **Versandkosten:** pauschal 4,99 € pro Bestellung; ab 40 Boxen Lieferung **frei Haus**
* **Mindermengenzuschlag:** 5,00 € unter einem Bestellwert von 35,00 €

## Funktionen

* **Eingabeprüfung (Guard Clause):** Lehnt ungültige Bestellmengen (`0`, negative Zahlen oder Kommazahlen) mit einer Fehlermeldung ab.
* **Kaufmännisches Runden:** Nutzt `roundEuro` mit `Number.EPSILON`, um Gleitkommafehler in JavaScript zu vermeiden und jeden Zwischenschritt exakt auf 2 Nachkommastellen zu runden.
* **Vollständige Konditionslogik:** Berücksichtigt automatisch Staffelrabatte, Mehrwertsteuer, optionalen Skonto, Versandkosten sowie den Mindermengenzuschlag.

## Verwendung

```javascript
const result = calculateBezugspreis(10, true);
console.log(result);
```

### Parameter

| Parameter | Typ | Standard | Beschreibung |
| :--- | :--- | :--- | :--- |
| `boxes` | `number` | – | Anzahl der bestellten Boxen (positive Ganzzahl) |
| `payWithin10Days` | `boolean` | `true` | `true`, wenn innerhalb von 10 Tagen mit 2 % Skonto gezahlt wird |

### Beispielausgabe (10 Boxen, mit Skonto)

```json
{
  "listenEinkaufspreis": 149.5,
  "rabatt": 7.48,
  "zielEinkaufspreisNetto": 142.02,
  "mehrwertsteuer": 26.98,
  "zielEinkaufspreisBrutto": 169,
  "skonto": 3.38,
  "barEinkaufspreis": 165.62,
  "bezugskosten": 4.99,
  "bezugspreis": 170.61
}
```