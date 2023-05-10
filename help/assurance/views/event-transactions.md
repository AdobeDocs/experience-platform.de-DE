---
title: Ansicht "Event Transactions"
description: Dieses Handbuch enthält Informationen zur Ansicht "Event Transactions"in Adobe Experience Platform Assurance.
exl-id: ad97f2c1-5bbc-49e2-8378-edcb8af149a3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# Ansicht &quot;Event Transactions&quot;

Mit der Ansicht &quot;Event Transactions&quot;in Adobe Experience Platform Assurance können Sie Ihre Edge Network-Client-Implementierung validieren und debuggen und die vorgelagerten Validierungsergebnisse nahezu in Echtzeit anzeigen.

## Einrichten der Sicherheit für den Edge Network-Workflow

Nachher [Einrichten der Sicherheit](../tutorials/implement-assurance.md)müssen Sie sicherstellen, dass Sie die neuesten Versionen der Assurance- und Edge Network-Erweiterungen in Ihrer App implementiert haben.

Um Ihre Ereignisse anzuzeigen, wählen Sie im Menü links die Option **[!UICONTROL Ereignistransaktionen]** unter **[!UICONTROL Adobe Experience Platform Edge]** Abschnitt.

Wenn diese Option nicht angezeigt wird, wählen Sie **[!UICONTROL Konfigurieren]** Fügen Sie links unten im Fenster den **[!UICONTROL Ereignistransaktionen]** Ansicht und wählen Sie **[!UICONTROL Speichern]**.

## Erste Schritte mit der Ansicht &quot;Event Transactions&quot;

In diesem Abschnitt lernen Sie die Ansicht &quot;Event Transaction&quot;kennen und erfahren, wie Sie sie effizient verwenden können, um die Validierung in Edge-Netzwerk-Workflows zu beenden.

### Ereignisverarbeitungsfluss

![Ansicht &quot;Ereignistransaktionen&quot;](./images/event-transactions/event-transactions-view.png)

In der Ansicht &quot;Event Transactions&quot;werden drei Spalten in der Reihenfolge des Ereignisverarbeitungsablaufs angezeigt:

- **[!UICONTROL Client-seitig]**: In dieser Spalte werden die Ereignisse angezeigt, die Client-seitig verarbeitet oder empfangen wurden und auf die das Mobile SDK zugreifen kann. Dazu gehören die Ereignisse, die mit einem API-Aufruf erstellt wurden, z. B. `Edge.sendEvent`und die Antwort-Ereignisbehandlung, die vom Client vom Edge Network-Server empfangen wurde, sofern vorhanden. Beispiele für clientseitige Ereignisse:
   - Das AEP-Anforderungsereignis ist das Ereignis, das über die Edge-Erweiterung gesendet wird und die XDM- und optionalen Freiformdaten enthält.
   - AEP Response Event Handle ist der Ereignishandler, der vom Edge Network als Antwort auf ein AEP Request Event empfangen wurde. Ein Anfrageereignis kann keine, eine oder mehrere Antwortereignis-Handles empfangen.
   - AEP-Fehlerantwort kann im Fall eines Fehlers angezeigt werden, z. B. wenn die XDM-Payload nicht verarbeitet werden konnte oder wenn einer der Upstream-Dienste einen Fehler oder eine Warnung zurückgab.
- **[!UICONTROL Edge Network]**: In dieser Spalte wird das Ereignis angezeigt, das vom Edge-Netzwerk über eine Netzwerkanforderung serverseitig empfangen wurde, sowie die Daten und Metadaten, die das Ereignis enthalten hat.
- **[!UICONTROL Upstream]**: In dieser Spalte werden die Ereignisse angezeigt, die von den konfigurierten Upstream-Diensten empfangen wurden, einschließlich detaillierter Informationen zu den Verarbeitungs- und/oder Validierungsergebnissen für das eingehende Ereignis.
Beachten Sie, dass diese Spalte dynamisch ist und je nach zwei Hauptfaktoren unterschiedliche Arten von Informationen anzeigen kann:
   - Die Konfiguration des Datenspeichers und die darin aktivierten Dienste.
   - Der Typ des Ereignisses, das an das Edge-Netzwerk gesendet wird.

### Inspect-Ereignisse

Die in der Ansicht &quot;Event Transactions&quot;angezeigten Ereignisse enthalten Informationen über Format und Inhalt der Daten, die in jedem Status verarbeitet werden, sowie aufschlussreiche Informationen zu Warnungen oder Fehlern, die bei der Verarbeitung der Daten in der vorgelagerten Phase aufgetreten sind. Die Ansicht hilft dabei, die Debugging-Informationen auf Ereignis-/Anfrageebene einzuschränken und Fehler frühzeitig im Entwicklungszyklus zu identifizieren.

#### Erweitern der Ereignisdetails

Um ein Ereignis zu überprüfen, wählen Sie das gewünschte Ereignis aus der Ansicht aus. Diese Aktion erweitert die **[!UICONTROL Ereignisdetails]** Ansicht auf der rechten Seite des Bildschirms.
Verschachtelte Daten werden in einem Baumstrukturformat angezeigt. Sie können verschachtelte Schlüsselwerte überprüfen, indem Sie die **+** (Plus) auf der linken Seite des Schlüsselnamens.

![Ereignisdetails](./images/event-transactions/event-details.png)

#### Warnungen und Fehler in Inspect

Jedem Ereignisnamen wird ein Symbol vorangestellt, das den allgemeinen Status der Verarbeitung für dieses Ereignis anzeigt:

- Wenn das Ereignis erfolgreich verarbeitet wurde, wird ein grünes Häkchen angezeigt.
- Wenn Warnungen oder Fehler erkannt wurden, wird ein Warnzeichen angezeigt. Wählen Sie das zugehörige Ereignis aus, um mehr über die Ursache der Warnung oder des Fehlers im **[!UICONTROL Ereignisdetails]** anzeigen.

### Konfigurationseinstellungen

Sie können die derzeit verwendete Kennung des Datastreams überprüfen, indem Sie die Info-QuickInfo neben dem **[!UICONTROL Edge Network]** Spaltenüberschrift.

![Anzeigen der Datensatz-ID](./images/event-transactions/show-datastream-id.png)

>[!INFO]
>
>Wenn mehrere Clients mit derselben Assurance-Sitzung verbunden sind und unterschiedliche Datastream-IDs verwendet werden, werden hier alle angezeigt. Dies bedeutet jedoch nicht, dass Ihre aktuelle Implementierung mehrere Datenspeicher verwendet. Zur Verarbeitung neuer Ereignisse von diesem Client wird nur die aktuelle Datastraam-ID verwendet, die im -Tag (mobile Eigenschaft) festgelegt ist, das von der App verwendet wird. Beim Testen komplexerer Anwendungsfälle mit unterschiedlichen Konfigurationseinstellungen und mehreren Clients, die verbunden sind, kann es hilfreich sein, separate Zuverlässigkeitssitzungen zu verwenden, um den Validierungsprozess zu vereinfachen.
