---
keywords: Experience Platform; Startseite; beliebte Themen; Konten aktualisieren
description: Unter bestimmten Umständen kann es erforderlich sein, die Details eines vorhandenen Quellenkontos zu aktualisieren. Der Arbeitsbereich "Quellen"bietet Ihnen die Möglichkeit, Details zu einem vorhandenen Batch oder einer Streaming-Verbindung hinzuzufügen, zu bearbeiten und zu löschen, einschließlich Name, Beschreibung und Anmeldeinformationen.
solution: Experience Platform
title: Aktualisieren der Kontodetails der Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 9%

---

# Aktualisieren der Kontodetails in der Benutzeroberfläche

Unter bestimmten Umständen kann es erforderlich sein, die Details eines vorhandenen Quellenkontos zu aktualisieren. Der Arbeitsbereich [!UICONTROL Quellen] bietet Ihnen die Möglichkeit, Details eines vorhandenen Batch- oder Streaming-Verbindungs, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.

Dieses Tutorial enthält Schritte zum Aktualisieren der Details und Anmeldeinformationen eines vorhandenen Kontos im Arbeitsbereich [!UICONTROL Quellen].

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
- [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Konten aktualisieren

Melden Sie sich bei [Experience Platform UI](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Sources]** aus dem linken Navigationsbereich aus, um auf den Arbeitsbereich [!UICONTROL Sources] zuzugreifen. Wählen Sie **[!UICONTROL Konten]** in der oberen Kopfzeile aus, um vorhandene Konten anzuzeigen.

![Katalog](../../images/tutorials/update/catalog.png)

Die Seite **[!UICONTROL Konten]** wird angezeigt. Auf dieser Seite finden Sie eine Liste sichtbarer Konten, einschließlich Informationen zu ihrer Quelle, Benutzername, Anzahl der Datenflüsse und Erstellungsdatum.

Wählen Sie oben links das Filtersymbol ![filter](../../images/tutorials/update/filter.png) aus, um das Sortierungsfenster zu öffnen.

![accounts-list](../../images/tutorials/update/accounts-list.png)

Das Sortierungsfenster bietet eine Liste aller Quellen. Sie können mehrere Quellen aus der Liste auswählen, um auf eine gefilterte Auswahl von Konten zuzugreifen, die verschiedenen Quellen zugeordnet sind.

Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, um eine Liste der vorhandenen Konten anzuzeigen. Nachdem Sie das Konto identifiziert haben, das Sie aktualisieren möchten, wählen Sie die Auslassungszeichen (`...`) neben dem Kontonamen aus.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

Es wird ein Dropdown-Menü mit Optionen für **[!UICONTROL Daten hinzufügen]**, **[!UICONTROL Details bearbeiten]** und **[!UICONTROL Löschen]** angezeigt. Wählen Sie **[!UICONTROL Details bearbeiten]** aus dem Menü aus, um Ihr Konto zu aktualisieren.

![update](../../images/tutorials/update/update.png)

Im Dialogfeld **[!UICONTROL Kontodetails bearbeiten]** können Sie den Namen, die Beschreibung und die Authentifizierungsdaten eines Kontos aktualisieren. Nachdem Sie die gewünschten Informationen aktualisiert haben, wählen Sie **[!UICONTROL Speichern]** aus.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Nach einigen Augenblicken wird unten im Bildschirm ein Bestätigungsfeld angezeigt, um eine erfolgreiche Aktualisierung zu bestätigen.

![update-bestätigte](../../images/tutorials/update/update-confirmed.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich [!UICONTROL Quellen] verwendet, um die Informationen eines vorhandenen Quellkontos zu aktualisieren.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Flow Service]-API finden Sie im Tutorial zum Aktualisieren der Verbindungsinformationen mithilfe der Flow Service-API](../../tutorials/api/update.md).[
