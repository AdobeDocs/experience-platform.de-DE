---
title: Ansicht des Validierungs-Editors
description: Dieses Handbuch enthält Informationen zur Ansicht „Validierungs-Editor“ in Adobe Experience Platform Assurance.
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 5%

---

# Ansicht des Validierungs-Editors

Mit dem Validierungs-Editor können Sie JavaScript-Funktionen schnell und einfach verwalten, um Ereignisse in einer Adobe Experience Platform Assurance-Sitzung zu validieren. Jede Funktion empfängt die Ereignisse in einer Assurance-Sitzung. Sie können Funktionen schreiben, um Ihre Client-Konfiguration, Ereignisbedingungen, Tests und Anwendungsfälle zu validieren.

## Erste Schritte mit dem Validierungs-Editor

Assurance Wählen [ nach dem Einrichten von ](../tutorials/implement-assurance.md) in der **[!UICONTROL Home]** Ansicht **[!UICONTROL Validation Editor]** aus.

![validation-editor-screen-shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Erstellen einer Validierungsfunktion

Mit dieser Funktion können Sie Validierungsfunktionen für Ihre Adobe Experience Platform Assurance-Sitzungen erstellen, bearbeiten oder löschen.

1. Wählen Sie **[!UICONTROL Create a New Validation]** aus.
2. Geben Sie einen **Namen** ein, um die Validierung zu identifizieren, und geben Sie dann eine **Kategorie** und eine **Beschreibung** an.
3. Bearbeiten Sie den Code im Editor, um die Ereignisse für Ihre Assurance-Sitzung zu validieren.

Wählen Sie nach Abschluss der Funktionstests die Option **[!UICONTROL Publish]** aus, um die Validierung zu speichern.

### Ereignisdefinition

| Schlüssel | Typ | Beschreibung |
| :--- | :--- | :--- |
| `uuid` | Zeichenfolge | Eindeutige Kennung des Ereignisses. |
| `timestamp` | Zahl | Zeitstempel des Clients, wann das Ereignis an Assurance gesendet wurde. |
| `eventNumber` | Zahl | Wird verwendet, um zu bestellen, wann das Ereignis gesendet wurde. Dieser Schlüssel ist nützlich, wenn Ereignisse denselben Zeitstempel haben. |
| `vendor` | String | Kennungszeichenfolge des Anbieters im umgekehrten Domain-Namensformat (z. B. com.adobe.assurance) |
| `type` | String | Wird verwendet, um den Ereignistyp zu kennzeichnen. |
| `payload` | Objekt | Definiert die Daten für das Ereignis und enthält eindeutige und allgemeine Eigenschaften. Zu den gebräuchlichen Eigenschaften gehören `ACPExtensionEventSource` und `ACPExtensionEventType`. |
| `annotations` | Array | Ein Array von Anmerkungsobjekten. |

### Definition der Anmerkung

| Schlüssel | Typ | Beschreibung |
| :--- | :--- | :--- |
| `uuid` | Zeichenfolge | Eindeutige Kennung der Anmerkung. |
| `type` | String | Wird verwendet, um den Anmerkungstyp zu kennzeichnen und ist normalerweise der Name des Plug-ins (z. B. Analytics). |
| `payload` | Objekt | Definiert die Daten, die das Ereignis ergänzen sollen. Bei Adobe Analytics sind hier die nachverarbeiteten Trefferdaten enthalten. |

### Validierungsergebnisse

Von der Validierungsfunktion wird erwartet, dass sie ein -Objekt zurückgibt, das Folgendes enthält:

| Schlüssel | Typ | Beschreibung |
| :--- | :--- | :--- |
| `message` | Zeichenfolge | Die Validierungsmeldung, die in der Ergebniszusammenfassung angezeigt werden soll. |
| `events` | Array | Ein Array von Ereignis-UUIDs, die als übereinstimmend oder nicht übereinstimmend gemeldet werden. |
| `links` | Array | Ein Array von `ValidationResultLink`-Objekten, um auf die Dokumentation und andere Ressourcen `{( type: 'doc'`&amp;vert;`'product', url: String )}` zu verweisen |
| `result` | String | Dies ist das Validierungsergebnis. Es wird erwartet, dass es eine der Aufzählungszeichenfolgen ist: „angewandt“, „nicht zugeordnet“, „unbekannt“ |

## Validierungsergebnisse anzeigen

Die Ergebnisse der -Funktion werden im Ergebnisabschnitt unter dem Code-Editor angezeigt. Wenn das Validierungsergebnis `unknown` oder `not matched` ist und das `events`-Array einen oder mehrere `uuids` aufweist, werden die Ereignisse in der Zeitleiste in den folgenden Farben hervorgehoben:

* Grün - übereinstimmend
* Orange - unbekannt
* Rot: keine Übereinstimmung

![timeling-validation-highlights-screen-shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Fehlerbehebung

Sie können `console.log()` in Ihrer Funktion hinzufügen, um Elemente in der Entwicklerkonsole zu drucken. Alternativ können Sie die Message-Eigenschaft des Ergebnisobjekts verwenden, um Meldungen im Ergebnisbereich zu debuggen.

Wenn im JavaScript-Code-Editor ein Fehler auftritt, wird ein Fehlerstatus zusammen mit dem Grund angezeigt.

Weitere Informationen zu Validierungen finden Sie auf dem [GitHub für Adobe Experience Platform Assurance](https://github.com/adobe/griffon-validation-plugins)Validierungen. Dort finden Sie Beispiele für Validierungen, die Adobe gehören. Ausführlichere Beschreibungen der Validierungen finden Sie [Wiki](https://github.com/adobe/griffon-validation-plugins/wiki).
