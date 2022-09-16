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
ht-degree: 16%

---

# Aktualisieren der Kontodetails in der Benutzeroberfläche

Unter bestimmten Umständen kann es erforderlich sein, die Details eines vorhandenen Quellenkontos zu aktualisieren. Die [!UICONTROL Quellen] Workspace bietet Ihnen die Möglichkeit, Details einer vorhandenen Batch- oder Streaming-Verbindung, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.

Dieses Tutorial enthält Schritte zum Aktualisieren der Details und Anmeldedaten eines vorhandenen Kontos über die [!UICONTROL Quellen] Arbeitsbereich.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
- [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Aktualisieren von Konten

Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com) und wählen Sie **[!UICONTROL Quellen]** über die linke Navigationsleiste auf [!UICONTROL Quellen] Arbeitsbereich. Auswählen **[!UICONTROL Konten]** aus der oberen Kopfzeile, um vorhandene Konten anzuzeigen.

![Katalog](../../images/tutorials/update/catalog.png)

Die **[!UICONTROL Konten]** angezeigt. Auf dieser Seite finden Sie eine Liste sichtbarer Konten, einschließlich Informationen zu ihrer Quelle, Benutzername, Anzahl der Datenflüsse und Erstellungsdatum.

Filtersymbol auswählen ![filter](../../images/tutorials/update/filter.png) oben links, um das Sortierungsfenster zu öffnen.

![accounts-list](../../images/tutorials/update/accounts-list.png)

Das Sortierungsfenster bietet eine Liste aller Quellen. Sie können mehrere Quellen aus der Liste auswählen, um auf eine gefilterte Auswahl von Konten zuzugreifen, die verschiedenen Quellen zugeordnet sind.

Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, um eine Liste der vorhandenen Konten anzuzeigen. Nachdem Sie das Konto identifiziert haben, das Sie aktualisieren möchten, wählen Sie die Auslassungszeichen (`...`) neben dem Kontonamen.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

Ein Dropdown-Menü wird angezeigt, in dem Sie Optionen zum **[!UICONTROL Daten hinzufügen]**, **[!UICONTROL Details bearbeiten]** und **[!UICONTROL Löschen]**. Auswählen **[!UICONTROL Details bearbeiten]** aus dem Menü, um Ihr Konto zu aktualisieren.

![Aktualisieren](../../images/tutorials/update/update.png)

Die **[!UICONTROL Kontodetails bearbeiten]** können Sie den Namen, die Beschreibung und die Authentifizierungsdaten eines Kontos aktualisieren. Nachdem Sie die gewünschten Informationen aktualisiert haben, wählen Sie **[!UICONTROL Speichern]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Nach einigen Augenblicken wird unten im Bildschirm ein Bestätigungsfeld angezeigt, um eine erfolgreiche Aktualisierung zu bestätigen.

![update-bestätigte](../../images/tutorials/update/update-confirmed.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich die [!UICONTROL Quellen] Arbeitsbereich zum Aktualisieren der Informationen eines vorhandenen Quellkontos.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mit dem [!DNL Flow Service] API, siehe Tutorial zu [Aktualisieren von Verbindungsinformationen mithilfe der Flow Service-API](../../tutorials/api/update.md).
