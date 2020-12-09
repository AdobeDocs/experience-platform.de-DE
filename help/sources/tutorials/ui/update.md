---
keywords: Experience Platform;home;popular topics;update accounts
description: Unter bestimmten Umständen kann es erforderlich sein, die Details eines Kontos mit vorhandenen Quellen zu aktualisieren. Der Quellenarbeitsbereich bietet Ihnen die Möglichkeit, Details zu einer vorhandenen Stapel- oder Streaming-Verbindung, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.
solution: Experience Platform
title: Kontodetails in der Benutzeroberfläche aktualisieren
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 9b48bc1426e6259ea0b2cf9b420b55b92712f7c2
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 4%

---


# Kontodetails in der Benutzeroberfläche aktualisieren

Unter bestimmten Umständen kann es erforderlich sein, die Details eines Kontos mit vorhandenen Quellen zu aktualisieren. Der [!UICONTROL Quellenarbeitsbereich] bietet Ihnen die Möglichkeit, Details zu einer vorhandenen Stapel- oder Streaming-Verbindung, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.

Dieses Lernprogramm enthält Schritte zum Aktualisieren der Details und Anmeldeinformationen eines vorhandenen Kontos im [!UICONTROL Sources] -Arbeitsbereich.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md): Die DNL-Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu beschriften und zu verbessern.
- [Sandboxen](../../../sandboxes/home.md): DNL Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

## Konten aktualisieren

Melden Sie sich bei der Benutzeroberfläche [der](https://platform.adobe.com) Experience Platform an und wählen Sie dann im linken Navigationsbereich die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den [!UICONTROL Quellarbeitsbereich] zuzugreifen. Wählen Sie **[!UICONTROL Konten]** aus der oberen Kopfzeile zur Ansicht vorhandener Konten.

![Katalog](../../images/tutorials/update/catalog.png)

Die Seite &quot; **[!UICONTROL Konten]** &quot;wird angezeigt. Auf dieser Seite finden Sie eine Liste von anzeigbaren Konten, einschließlich Informationen zu deren Quelle, Benutzername, Anzahl der Datenflüsse und Erstellungsdatum.

Wählen Sie oben links den ![Filter](../../images/tutorials/update/filter.png) für das Filtersymbol aus, um den Sortierbereich zu starten.

![accounts-Liste](../../images/tutorials/update/accounts-list.png)

Der Sortierbereich bietet eine Liste aller Quellen. Sie können mehrere Quellen aus der Liste auswählen, um auf eine gefilterte Auswahl von Konten zuzugreifen, die verschiedenen Quellen zugeordnet sind.

Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, um eine Liste der vorhandenen Konten anzuzeigen. Nachdem Sie das Konto identifiziert haben, das Sie aktualisieren möchten, wählen Sie die Auslassungspunkte (`...`) neben dem Kontonamen aus.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

Es wird ein Dropdown-Menü mit Optionen zum **[!UICONTROL Hinzufügen von Daten]**, zum **[!UICONTROL Bearbeiten von Details]** und zum **[!UICONTROL Löschen]** angezeigt. Wählen Sie Details **[!UICONTROL bearbeiten]** aus dem Menü, um Ihr Konto zu aktualisieren.

![update](../../images/tutorials/update/update.png)

Im Dialogfeld Kontodetails **[!UICONTROL bearbeiten]** können Sie den Namen, die Beschreibung und die Authentifizierungsdaten eines Kontos aktualisieren. Nachdem Sie die gewünschten Informationen aktualisiert haben, wählen Sie **[!UICONTROL Speichern]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Nach einigen Augenblicken wird am unteren Bildschirmrand ein grünes Bestätigungsfeld angezeigt, um eine erfolgreiche Aktualisierung zu bestätigen.

![update-bestätigte](../../images/tutorials/update/update-confirmed.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie die Kontoinformationen erfolgreich im Arbeitsbereich &quot; [!UICONTROL Quellen] &quot;aktualisiert.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Flow Service] API finden Sie im Lernprogramm zum [Aktualisieren der Verbindungsinformationen mithilfe der Flow Service API](../../tutorials/api/update.md).