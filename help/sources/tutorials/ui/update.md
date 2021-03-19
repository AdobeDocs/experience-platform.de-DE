---
keywords: Experience Platform;Startseite;beliebte Themen;Aktualisieren von Konten
description: Unter bestimmten Umständen kann es erforderlich sein, die Details eines Kontos mit vorhandenen Quellen zu aktualisieren. Der Quellenarbeitsbereich bietet Ihnen die Möglichkeit, Details zu einer vorhandenen Stapel- oder Streaming-Verbindung, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.
solution: Experience Platform
title: Kontodetails der Quellverbindung in der Benutzeroberfläche aktualisieren
topic: Übersicht
type: Tutorial
translation-type: tm+mt
source-git-commit: 4a7405e2c8c97442d2781295dd827c6940aa33eb
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 10%

---


# Kontodetails in der Benutzeroberfläche aktualisieren

Unter bestimmten Umständen kann es erforderlich sein, die Details eines Kontos mit vorhandenen Quellen zu aktualisieren. Der Arbeitsbereich [!UICONTROL Quellen] bietet Ihnen die Möglichkeit, Details zu einer vorhandenen Stapel- oder Streaming-Verbindung, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.

Dieses Lernprogramm enthält Schritte zum Aktualisieren der Details und Anmeldeinformationen eines vorhandenen Kontos im Arbeitsbereich [!UICONTROL Quellen].

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
- [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Konten aktualisieren

Melden Sie sich bei der Benutzeroberfläche [Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** aus der linken Navigation, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Wählen Sie **[!UICONTROL Konten]** aus der oberen Kopfzeile, um vorhandene Konten Ansicht.

![Katalog](../../images/tutorials/update/catalog.png)

Die Seite **[!UICONTROL Konten]** wird angezeigt. Auf dieser Seite finden Sie eine Liste von anzeigbaren Konten, einschließlich Informationen zu deren Quelle, Benutzername, Anzahl der Datenflüsse und Erstellungsdatum.

Wählen Sie oben links das Filtersymbol ![filter](../../images/tutorials/update/filter.png) aus, um das Sortierfeld zu starten.

![accounts-Liste](../../images/tutorials/update/accounts-list.png)

Der Sortierbereich bietet eine Liste aller Quellen. Sie können mehrere Quellen aus der Liste auswählen, um auf eine gefilterte Auswahl von Konten zuzugreifen, die verschiedenen Quellen zugeordnet sind.

Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, um eine Liste der vorhandenen Konten anzuzeigen. Nachdem Sie das Konto identifiziert haben, das Sie aktualisieren möchten, wählen Sie die Auslassungspunkte (`...`) neben dem Kontonamen aus.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

Es wird ein Dropdown-Menü angezeigt, das die Optionen für **[!UICONTROL Hinzufügen Daten]**, **[!UICONTROL Details bearbeiten]** und **[!UICONTROL Löschen]** bereitstellt. Wählen Sie **[!UICONTROL Details bearbeiten]** aus dem Menü, um Ihr Konto zu aktualisieren.

![update](../../images/tutorials/update/update.png)

Im Dialogfeld **[!UICONTROL Kontodetails bearbeiten]** können Sie den Namen, die Beschreibung und die Authentifizierungsdaten eines Kontos aktualisieren. Nachdem Sie die gewünschten Informationen aktualisiert haben, wählen Sie **[!UICONTROL Speichern]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Nach einigen Augenblicken wird unten im Bildschirm ein Bestätigungsfeld angezeigt, um eine erfolgreiche Aktualisierung zu bestätigen.

![update-bestätigte](../../images/tutorials/update/update-confirmed.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich den Arbeitsbereich [!UICONTROL Quellen] verwendet, um die Informationen eines vorhandenen Quellkontos zu aktualisieren.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mit der API [!DNL Flow Service] finden Sie im Lehrgang [zum Aktualisieren der Verbindungsinformationen mit der Flow Service API](../../tutorials/api/update.md).