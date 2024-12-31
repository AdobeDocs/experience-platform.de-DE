---
title: Ansicht „Ereignistransaktionen“
description: Dieses Handbuch enthält Informationen zur Ansicht „Ereignistransaktionen“ in Adobe Experience Platform Assurance.
exl-id: ad97f2c1-5bbc-49e2-8378-edcb8af149a3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# Ansicht „Ereignistransaktionen“

Mit der Ansicht „Ereignistransaktionen“ in Adobe Experience Platform Assurance können Sie Ihre Edge Network-Client-Implementierung validieren und debuggen und die Ergebnisse der vorgelagerten Validierung nahezu in Echtzeit sehen.

## Einrichten von Assurance für den Edge Network-Workflow

Stellen [ nach dem „Einrichten von Assurance](../tutorials/implement-assurance.md) sicher, dass Sie die neuesten Versionen der Assurance- und Edge Network-Erweiterungen in Ihrer App implementiert haben.

Um Ihre Ereignisse anzuzeigen, wählen Sie im Menü links **[!UICONTROL Abschnitt {]**}Adobe Experience Platform Edge ]**die Option „Ereignistransaktionen“ aus.**[!UICONTROL 

Wenn diese Option nicht angezeigt wird, wählen **[!UICONTROL unten links im Fenster]** Konfigurieren“ aus, fügen Sie die Ansicht **[!UICONTROL Ereignistransaktionen]** hinzu und klicken Sie auf **[!UICONTROL Speichern]**.

## Erste Schritte mit der Ansicht „Ereignistransaktionen“

In diesem Abschnitt machen Sie sich mit der Ansicht „Ereignistransaktion“ vertraut und erfahren, wie Sie sie effizient für die End-to-End-Validierung in Edge Network-Workflows verwenden.

### Ereignisverarbeitungsablauf

![Ansicht „Ereignistransaktionen“](./images/event-transactions/event-transactions-view.png)

Die Ansicht Ereignistransaktionen zeigt drei Spalten in der Reihenfolge des Ereignisverarbeitungsflusses an:

- **[!UICONTROL Client-seitig]**: Diese Spalte zeigt die Client-seitig verarbeiteten oder empfangenen Ereignisse an, auf die die Mobile SDK zugreifen kann. Dazu gehören die Ereignisse, die mit einem API-Aufruf erstellt wurden, z. B. `Edge.sendEvent`, und die Antwortereignisse, die vom Client vom Edge Network-Server empfangen wurden, falls vorhanden. Beispiele für Client-seitige Ereignisse:
   - Das AEP-Anfrageereignis ist das Ereignis, das über die Edge-Erweiterung gesendet wird und die XDM- und optionalen Freiformdaten enthält.
   - AEP Response Event Handle ist der Ereignishandler, der vom Edge Network als Antwort auf ein AEP Request-Ereignis empfangen wird. Ein Anfrageereignis erhält möglicherweise keinen, einen oder mehrere Antwortereignis-Handler.
   - Die AEP-Fehlerantwort kann im Falle eines Fehlers angezeigt werden, z. B. wenn die XDM-Payload nicht verarbeitet werden konnte oder wenn einer der Upstream-Services einen Fehler oder eine Warnung zurückgab.
- **[!UICONTROL Edge Network]**: In dieser Spalte werden das Ereignis, das vom Edge Network über eine Netzwerkanfrage Server-seitig empfangen wurde, und die im Ereignis enthaltenen Daten und Metadaten angezeigt.
- **[!UICONTROL Upstream]**: Diese Spalte zeigt die Ereignisse an, die von den konfigurierten Upstream-Services empfangen wurden, einschließlich detaillierter Informationen zu den Verarbeitungs- und/oder Validierungsergebnissen für das eingehende Ereignis.
Beachten Sie, dass diese Spalte dynamisch ist und je nach zwei Hauptfaktoren unterschiedliche Arten von Informationen anzeigen kann:
   - Die Datenstromkonfiguration und die dafür aktivierten Services.
   - Der Ereignistyp, der an das Edge Network gesendet wird.

### Inspect-Ereignisse

Die in der Ansicht Ereignistransaktionen angezeigten Ereignisse bieten Informationen über das Format und den Inhalt der Daten, die in jedem Status verarbeitet werden, sowie aufschlussreiche Details zu allen Warnungen oder Fehlern, die auftreten, wenn die Daten zuvor verarbeitet werden. Die Ansicht hilft dabei, die Debugging-Informationen auf der Ereignis-/Anfrageebene einzugrenzen und Fehler frühzeitig im Entwicklungszyklus zu identifizieren.

#### Ereignisdetails erweitern

Um ein Ereignis zu untersuchen, wählen Sie das gewünschte Ereignis aus der Ansicht aus. Diese Aktion erweitert die **[!UICONTROL Ereignisdetails]** auf der rechten Seite des Bildschirms.
Verschachtelte Daten werden im Baumstrukturformat angezeigt. Sie können verschachtelte Schlüsselwerte überprüfen, indem Sie auf die Schaltfläche **+** (plus) links neben dem Schlüsselnamen klicken.

![Ereignisdetails](./images/event-transactions/event-details.png)

#### Inspect-Warnungen oder -Fehler

Jedem Ereignisnamen ist ein Symbol vorangestellt, das den allgemeinen Status der Verarbeitung für dieses Ereignis angibt:

- Wenn das Ereignis erfolgreich verarbeitet wurde, wird ein grünes Häkchen angezeigt.
- Wenn Warnmeldungen oder Fehler erkannt wurden, wird ein Warnzeichen angezeigt. Wählen Sie das entsprechende Ereignis aus, um mehr über die Ursache der Warnung oder des Fehlers in der Ansicht **[!UICONTROL Ereignisdetails]** zu erfahren.

### Konfigurationseinstellungen

Sie können die aktuell verwendete Datenstromkennung überprüfen, indem Sie die Info-QuickInfo neben der Spaltenüberschrift **[!UICONTROL Edge Network]** auswählen.

![Anzeigen der Datenstrom-ID](./images/event-transactions/show-datastream-id.png)

>[!INFO]
>
>Wenn mehrere Clients eine Verbindung mit derselben Assurance-Sitzung herstellen und verschiedene Datenstrom-IDs verwendet werden, werden alle hier angezeigt. Dies bedeutet jedoch nicht, dass Ihre aktuelle Implementierung mehrere Datenströme verwendet. Nur die aktuelle Datenstrom-ID, die in dem von der App verwendeten Tag (Eigenschaft für Mobilgeräte) festgelegt ist, wird für die Verarbeitung neuer Ereignisse von diesem Client verwendet. Beim Testen komplizierterer Anwendungsfälle mit unterschiedlichen Konfigurationseinstellungen und mehreren verbundenen Clients kann es hilfreich sein, separate Assurance-Sitzungen zu verwenden, um den Validierungsprozess zu vereinfachen.
