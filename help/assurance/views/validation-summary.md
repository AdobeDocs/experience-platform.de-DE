---
title: Ansicht des Validierungs-Editors
description: Dieses Handbuch enthält Informationen zur Ansicht des Validierungs-Editors in Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 4%

---


# Ansicht &quot;Validation Editor&quot;

Mit dem Validation Editor können Sie JavaScript-Funktionen schnell und einfach verwalten, um Ereignisse in einer Adobe Experience Platform Assurance-Sitzung zu validieren. Jede Funktion empfängt die Ereignisse in einer Assurance-Sitzung. Sie können Funktionen schreiben, um Ihre Client-Konfiguration, Ereignisbedingungen, Tests und Anwendungsfälle zu überprüfen.

## Erste Schritte mit dem Validierungs-Editor

Nachher [Einrichten der Sicherheit](../tutorials/implement-assurance.md)auf **[!UICONTROL Startseite]** Ansicht, wählen Sie **[!UICONTROL Validierungs-Editor]**.

![validation-editor-screen-shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Überprüfungsfunktion schreiben

Mit dieser Funktion können Sie Validierungsfunktionen für Ihre Adobe Experience Platform Assurance-Sitzungen erstellen, bearbeiten oder löschen.

1. Auswählen **[!UICONTROL Erstellen einer neuen Validierung]**.
2. Geben Sie einen **name** , um die Validierung zu identifizieren, und geben Sie dann eine **category** und **description**.
3. Bearbeiten Sie den Code im Editor, um die Ereignisse für Ihre Zuverlässigkeitssitzung zu validieren.

Nachdem die Funktionstests abgeschlossen sind, wählen Sie **[!UICONTROL Veröffentlichen]** , um Ihre Validierung zu speichern.

### Ereignisdefinition

| Schlüssel | Typ | Beschreibung |
| :--- | :--- | :--- |
| `uuid` | Zeichenfolge | Universally Unique Identifier für das Ereignis. |
| `timestamp` | Zahl | Zeitstempel vom Client, zu dem das Ereignis an Assurance gesendet wurde. |
| `eventNumber` | Zahl | Wird verwendet, um beim Senden des Ereignisses zu ordnen. Dieser Schlüssel ist nützlich, wenn Ereignisse denselben Zeitstempel haben. |
| `vendor` | Zeichenfolge | Identifizierungszeichenfolge des Anbieters im Format des umgekehrten Domänennamens (z. B. com.adobe.assurance). |
| `type` | Zeichenfolge | Wird verwendet, um den Ereignistyp zu kennzeichnen. |
| `payload` | Objekt | Definiert die Daten für das Ereignis und enthält eindeutige und allgemeine Eigenschaften. Zu den gebräuchlichen Eigenschaften gehören `ACPExtensionEventSource` und `ACPExtensionEventType`. |
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
| `links` | Array | Ein Array von `ValidationResultLink` Objekte zum Referenzieren der Dokumentation und anderer Ressourcen `{( type: 'doc'|'product', url: String )}` |
| `result` | Zeichenfolge | Dies ist das Überprüfungsergebnis und muss eine der aufgezählten Zeichenfolgen sein: &quot;match&quot;, &quot;not match&quot;, &quot;unknown&quot; |

## Überprüfungsergebnisse anzeigen

Die Ergebnisse der Funktion werden im Ergebnisabschnitt unter dem Code-Editor angezeigt. Wenn das Überprüfungsergebnis `unknown` oder `not matched` und `events` Array hat eine oder mehrere `uuids`, werden die Ereignisse in der Timeline mit den folgenden Farben hervorgehoben:

* Grün - Übereinstimmung
* Orange - unbekannt
* Rot - nicht abgeglichen

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Fehlerbehebung

Sie können `console.log()` in Ihrer -Funktion, um Elemente in die Entwicklerkonsole zu drucken. Alternativ können Sie die message -Eigenschaft des result -Objekts verwenden, um Nachrichten im Ergebnisbereich zu debuggen.

Tritt im JavaScript-Code-Editor ein Fehler auf, wird zusammen mit dem Grund ein Fehlerstatus angezeigt.

Weitere Informationen zu Validierungen finden Sie unter [Adobe Experience Platform Assurance-Überprüfungen](https://github.com/adobe/griffon-validation-plugins) GitHub. Hier finden Sie Beispiele für Überprüfungen, die der Adobe gehören. Siehe [Wiki](https://github.com/adobe/griffon-validation-plugins/wiki) für detailliertere Beschreibungen der Validierungen.
