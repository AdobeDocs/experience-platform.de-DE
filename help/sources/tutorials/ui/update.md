---
keywords: Experience Platform; Homepage; beliebte Themen; Konten aktualisieren
description: Unter bestimmten Umständen kann es erforderlich sein, die Details eines vorhandenen Quellenkontos zu aktualisieren. Der Arbeitsbereich "Quellen"bietet Ihnen die Möglichkeit, Details zu einem vorhandenen Batch oder einer Streaming-Verbindung hinzuzufügen, zu bearbeiten und zu löschen, einschließlich Name, Beschreibung und Anmeldeinformationen.
solution: Experience Platform
title: Aktualisieren der Source-Verbindungskontodetails in der Benutzeroberfläche
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 16%

---

# Aktualisieren der Kontodetails in der Benutzeroberfläche

Unter bestimmten Umständen kann es erforderlich sein, die Details eines vorhandenen Quellenkontos zu aktualisieren. Der Arbeitsbereich [!UICONTROL Quellen] bietet Ihnen die Möglichkeit, Details zu einem vorhandenen Batch oder einer Streaming-Verbindung hinzuzufügen, zu bearbeiten und zu löschen, einschließlich Name, Beschreibung und Anmeldeinformationen.

In diesem Tutorial werden Schritte zum Aktualisieren der Details und Anmeldeinformationen eines vorhandenen Kontos im Arbeitsbereich [!UICONTROL Quellen] beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
- [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Aktualisieren von Konten

Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com) an und wählen Sie dann im linken Navigationsbereich **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Wählen Sie in der oberen Kopfzeile **[!UICONTROL Konten]** aus, um vorhandene Konten anzuzeigen.

![Katalog](../../images/tutorials/update/catalog.png)

Die Seite **[!UICONTROL Konten]** wird angezeigt. Auf dieser Seite finden Sie eine Liste sichtbarer Konten, einschließlich Informationen zu ihrer Quelle, Benutzername, Anzahl der Datenflüsse und Erstellungsdatum.

Wählen Sie oben links das Filtersymbol ![filter](/help/images/icons/filter.png) aus, um das Sortierfeld zu starten.

![accounts-list](../../images/tutorials/update/accounts-list.png)

Das Sortierungsfenster bietet eine Liste aller Quellen. Sie können mehrere Quellen aus der Liste auswählen, um auf eine gefilterte Auswahl von Konten zuzugreifen, die verschiedenen Quellen zugeordnet sind.

Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, um eine Liste der vorhandenen Konten anzuzeigen. Nachdem Sie das Konto identifiziert haben, das Sie aktualisieren möchten, wählen Sie die Auslassungszeichen (`...`) neben dem Kontonamen aus.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

Es wird ein Dropdown-Menü angezeigt, in dem Sie Optionen zu **[!UICONTROL Daten hinzufügen]**, **[!UICONTROL Details bearbeiten]** und **[!UICONTROL Löschen]** auswählen können. Wählen Sie **[!UICONTROL Details bearbeiten]** aus dem Menü aus, um Ihr Konto zu aktualisieren.

![-Aktualisierung](../../images/tutorials/update/update.png)

Im Dialogfeld **[!UICONTROL Kontodetails bearbeiten]** können Sie den Namen, die Beschreibung und die Authentifizierungsdaten eines Kontos aktualisieren. Nachdem Sie die gewünschten Informationen aktualisiert haben, wählen Sie **[!UICONTROL Speichern]** aus.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Nach einigen Augenblicken wird unten im Bildschirm ein Bestätigungsfeld angezeigt, um eine erfolgreiche Aktualisierung zu bestätigen.

![update-bestätigte](../../images/tutorials/update/update-confirmed.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich [!UICONTROL Quellen] verwendet, um die Informationen eines vorhandenen Quellkontos zu aktualisieren.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Flow Service] -API finden Sie im Tutorial zum Aktualisieren der Verbindungsinformationen mithilfe der Flow Service-API](../../tutorials/api/update.md).[
