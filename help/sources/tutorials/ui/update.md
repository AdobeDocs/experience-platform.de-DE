---
keywords: Experience Platform;Startseite;beliebte Themen;Konten aktualisieren
description: Unter bestimmten Umständen kann es erforderlich sein, die Details eines vorhandenen Quellenkontos zu aktualisieren. Der Arbeitsbereich Quellen bietet Ihnen die Möglichkeit, Details einer vorhandenen Batch- oder Streaming-Verbindung, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.
solution: Experience Platform
title: Aktualisieren der Details des Source-Verbindungskontos in der Benutzeroberfläche
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 5%

---

# Aktualisieren von Kontodetails in der Benutzeroberfläche

Unter bestimmten Umständen kann es erforderlich sein, die Details eines vorhandenen Quellenkontos zu aktualisieren. Der Arbeitsbereich [!UICONTROL Quellen] bietet Ihnen die Möglichkeit, Details einer vorhandenen Batch- oder Streaming-Verbindung, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.

In diesem Tutorial finden Sie Schritte zum Aktualisieren der Details und Anmeldeinformationen eines vorhandenen Kontos aus dem Arbeitsbereich [!UICONTROL Quellen].

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
- [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

## Aktualisieren von Konten

Melden Sie sich bei der Benutzeroberfläche von [Experience Platform ](https://platform.adobe.com) und wählen Sie **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Wählen Sie **[!UICONTROL Konten]** in der oberen Kopfzeile aus, um vorhandene Konten anzuzeigen.

![Katalog](../../images/tutorials/update/catalog.png)

Die **[!UICONTROL Konten]** wird angezeigt. Auf dieser Seite finden Sie eine Liste der sichtbaren Konten, einschließlich Informationen über ihre Quelle, ihren Benutzernamen, die Anzahl der Datenflüsse und das Erstellungsdatum.

Wählen Sie das Filtersymbol ![filter](/help/images/icons/filter.png) oben links aus, um das Sortier-Bedienfeld zu starten.

![accounts-list](../../images/tutorials/update/accounts-list.png)

Das Sortier-Bedienfeld bietet eine Liste aller Quellen. Sie können mehrere Quellen aus der Liste auswählen, um auf eine gefilterte Auswahl von Konten zuzugreifen, die mit verschiedenen Quellen verknüpft sind.

Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, um eine Liste der vorhandenen Konten anzuzeigen. Nachdem Sie das Konto identifiziert haben, das Sie aktualisieren möchten, wählen Sie die Auslassungspunkte (`...`) neben dem Kontonamen aus.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

Es wird ein Dropdown-Menü angezeigt, das Optionen für **[!UICONTROL Daten hinzufügen]**, **[!UICONTROL Details bearbeiten]** und **[!UICONTROL Löschen]** enthält. Wählen Sie **[!UICONTROL Details bearbeiten]** aus dem Menü aus, um Ihr Konto zu aktualisieren.

![-Aktualisierung](../../images/tutorials/update/update.png)

Im **[!UICONTROL Kontodetails bearbeiten]** können Sie den Namen, die Beschreibung und die Authentifizierungsdaten eines Kontos aktualisieren. Nachdem Sie die gewünschten Informationen aktualisiert haben, klicken Sie auf **[!UICONTROL Speichern]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Nach einigen Augenblicken wird ein Bestätigungsfeld am unteren Bildschirmrand angezeigt, um eine erfolgreiche Aktualisierung zu bestätigen.

![update-confirmed](../../images/tutorials/update/update-confirmed.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich [!UICONTROL Quellen] verwendet, um die Informationen eines vorhandenen Quellkontos zu aktualisieren.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Flow Service]-API finden Sie im Tutorial zum [Aktualisieren von Verbindungsinformationen mithilfe der Flow Service-API](../../tutorials/api/update.md).
