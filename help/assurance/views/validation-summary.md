---
title: Ansicht des Validierungs-Editors
description: Dieses Handbuch enthält Informationen zur Ansicht des Validierungs-Editors in Adobe Experience Platform Assurance.
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 4%

---

# Ansicht &quot;Validierungs-Editor&quot;

Mit dem Validierungseditor können Sie JavaScript-Funktionen schnell und einfach verwalten, um Ereignisse in einer Adobe Experience Platform Assurance-Sitzung zu validieren. Jede Funktion empfängt die Ereignisse in einer Assurance-Sitzung. Sie können Funktionen schreiben, um Ihre Client-Konfiguration, Ereignisbedingungen, Tests und Anwendungsfälle zu überprüfen.

## Erste Schritte mit dem Validierungseditor

Wählen Sie nach [ Einrichten von Assurance](../tutorials/implement-assurance.md) in der Ansicht **[!UICONTROL Home]** die Option **[!UICONTROL Validation Editor]**.

![validation-editor-screen-shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Überprüfungsfunktion schreiben

Mit dieser Funktion können Sie Validierungsfunktionen für Ihre Adobe Experience Platform Assurance-Sitzungen erstellen, bearbeiten oder löschen.

1. Wählen Sie **[!UICONTROL Neue Validierung erstellen]** aus.
2. Geben Sie einen **Namen** ein, um die Validierung zu identifizieren, und geben Sie dann eine **Kategorie** und eine **Beschreibung** ein.
3. Bearbeiten Sie den Code im Editor, um die Ereignisse für Ihre Zuverlässigkeitssitzung zu validieren.

Nachdem die Funktionstests abgeschlossen sind, wählen Sie **[!UICONTROL Publish]** aus, um Ihre Validierung zu speichern.

### Ereignisdefinition

| Schlüssel | Typ | Beschreibung |
| :--- | :--- | :--- |
| `uuid` | Zeichenfolge | Universell eindeutige Kennung für das Ereignis. |
| `timestamp` | Zahl | Zeitstempel vom Client, zu dem das Ereignis an Assurance gesendet wurde. |
| `eventNumber` | Zahl | Wird verwendet, um beim Senden des Ereignisses zu ordnen. Dieser Schlüssel ist nützlich, wenn Ereignisse denselben Zeitstempel haben. |
| `vendor` | Zeichenfolge | Identifizierungszeichenfolge des Anbieters im Format des umgekehrten Domänennamens (z. B. com.adobe.assurance). |
| `type` | Zeichenfolge | Wird zur Bezeichnung des Ereignistyps verwendet. |
| `payload` | Objekt | Definiert die Daten für das Ereignis und enthält eindeutige und allgemeine Eigenschaften. Zu den allgemeinen Eigenschaften gehören `ACPExtensionEventSource` und `ACPExtensionEventType`. |
| `annotations` | Array | Ein Array von Anmerkungsobjekten. |

### Anmerkungsdefinition

| Schlüssel | Typ | Beschreibung |
| :--- | :--- | :--- |
| `uuid` | Zeichenfolge | Universally Unique Identifier für die Anmerkung. |
| `type` | Zeichenfolge | Dient zur Bezeichnung des Anmerkungstyps und ist normalerweise der Name des Plug-ins (z. B. Analytics). |
| `payload` | Objekt | Definiert die Daten, die das Ereignis ergänzen sollen. Bei Adobe Analytics sind hier die nachbearbeiteten Trefferdaten enthalten. |

### Überprüfungsergebnisse

Von der Validierungsfunktion wird erwartet, dass sie ein Objekt zurückgibt, das Folgendes enthält:

| Schlüssel | Typ | Beschreibung |
| :--- | :--- | :--- |
| `message` | Zeichenfolge | Die Validierungsmeldung, die in den Zusammenfassungsergebnissen angezeigt werden soll. |
| `events` | Array | Ein Array von Ereignis-UUIDs, die als abgeglichen oder nicht abgeglichen gemeldet werden. |
| `links` | Array | Ein Array von `ValidationResultLink` -Objekten, die auf Dokumentation und andere Ressourcen verweisen `{( type: 'doc'|'product', url: String )}` |
| `result` | Zeichenfolge | Dies ist das Überprüfungsergebnis und sollte eine der aufgezählten Zeichenfolgen sein: &quot;match&quot;, &quot;not match&quot;, &quot;unknown&quot; |

## Überprüfungsergebnisse anzeigen

Die Ergebnisse der Funktion werden im Ergebnisabschnitt unter dem Code-Editor angezeigt. Wenn das Überprüfungsergebnis `unknown` oder `not matched` lautet und das Array `events` mindestens ein `uuids` aufweist, werden die Ereignisse in der Timeline mit den folgenden Farben hervorgehoben:

* Grün - Übereinstimmung
* Orange - unbekannt
* Rot - nicht abgeglichen

![timeling-validation-Highlights-screen-shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Fehlerbehebung

Sie können `console.log()` in Ihrer Funktion hinzufügen, um Elemente in der Entwicklerkonsole zu drucken. Alternativ können Sie die message -Eigenschaft des result -Objekts verwenden, um Nachrichten im Ergebnisbereich zu debuggen.

Tritt im Code-Editor von JavaScript ein Fehler auf, wird neben dem Grund ein Fehlerstatus angezeigt.

Weitere Informationen zu Validierungen finden Sie auf dem GitHub [Adobe Experience Platform Assurance Validations](https://github.com/adobe/griffon-validation-plugins) . Hier finden Sie Beispiele für Validierungen im Besitz von Adobe. Detailliertere Beschreibungen der Überprüfungen finden Sie im [Wiki](https://github.com/adobe/griffon-validation-plugins/wiki) .
