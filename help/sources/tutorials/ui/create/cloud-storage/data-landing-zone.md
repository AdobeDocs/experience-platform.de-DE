---
keywords: Experience Platform; Startseite; beliebte Themen; Data Landing Zone; Daten-Landingzone
solution: Experience Platform
title: Data Landing Zone über die Benutzeroberfläche mit Platform verbinden
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche von Platform einen Quell-Connector für die Data Landing Zone erstellen.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: b007cdf92811b453df5b5d005456a05cd845b769
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 9%

---

# Verbinden [!DNL Data Landing Zone] zur Plattform mithilfe der Benutzeroberfläche

[!DNL Data Landing Zone] ist eine Cloud-basierte Datenspeicheranlage für temporäre Dateispeicher, die mit Adobe Experience Platform bereitgestellt wird. Daten werden automatisch aus der [!DNL Data Landing Zone] nach sieben Tagen.

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Data Landing Zone] Quellverbindung über die Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Dateien aus [!DNL Data Landing Zone] Platform

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über die linke Navigationsleiste auf [!UICONTROL Quellen] Arbeitsbereich. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Unter dem [!UICONTROL Cloud-Speicher] category, select [!DNL Data Landing Zone] und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/dlz/catalog.png)

Die [!UICONTROL Daten hinzufügen] angezeigt werden. Sie erhalten eine Oberfläche, über die Sie die Daten auswählen und eine Vorschau der Daten anzeigen können, die Sie in Platform laden möchten.

![add-data](../../../../images/tutorials/create/dlz/add-data.png)

Eine detaillierte, schrittweise Anleitung zum Erstellen eines Datenflusses für eine Cloud-Speicherquelle finden Sie im Tutorial unter [Erstellen eines Cloud-Speicher-Datenflusses zum Übertragen von Daten an Platform](../../dataflow/batch/cloud-storage.md).

## Abrufen und Aktualisieren Ihrer [!DNL Data Landing Zone] Anmeldeinformationen

[!DNL Data Landing Zone] ist eine native Quelle, die im Lieferumfang Ihrer Adobe Experience Platform Sources-Lizenz enthalten ist. [!DNL Data Landing Zone] verwendet eine SAS-URI- und SAS-Token-basierte Authentifizierung. Sie können Ihre Authentifizierungsberechtigungen über die [!UICONTROL Quellen-Katalog] Seite.

Im [!UICONTROL Quellen-Katalog]unter [!UICONTROL Cloud-Speicher] -Kategorie, wählen Sie die Auslassungszeichen (**...**) aus dem **[!UICONTROL Data Landing Zone]** Karte. Wählen Sie im angezeigten Dropdown-Menü die Option **[!UICONTROL Anmeldedaten anzeigen]**.

![options](../../../../images/tutorials/create/dlz/options.png)

Es wird ein Popup angezeigt, in dem Ihr Containername, Ihr SAS-Token, der Name des Speicherkontos und Ihr SAS-URI angezeigt werden.

Auswählen **[!UICONTROL Anmeldeinformationen aktualisieren]** und einige Sekunden Zeit in Anspruch nehmen, damit Ihre aktualisierten Anmeldedaten verarbeitet werden.

>[!TIP]
>
>Ihre [!DNL Data Landing Zone] Die Anmeldedaten laufen nach 90 Tagen automatisch ab und Sie müssen neue Anmeldedaten verwenden, um eine erneute Verbindung zu [!DNL Data Landing Zone] nach Ablauf. Ihre Datenflüsse in Platform sind nicht durch das Ablaufen von Anmeldeinformationen betroffen. Sie können weiterhin mit neuen und vorhandenen Datenflüssen mit Ihren neuen Anmeldedaten arbeiten.

![view-credentials](../../../../images/tutorials/create/dlz/credentials.png)

## Nächste Schritte

In diesem Tutorial haben Sie auf Ihre [!DNL Data Landing Zone] Container hinzugefügt und erfahren, wie Sie Ihre Anmeldedaten abrufen und aktualisieren können. Sie können jetzt mit dem nächsten Tutorial zum [Erstellen eines Datenflusses zum Übertragen von Daten aus einem Cloud-Speicher in Platform](../../dataflow/batch/cloud-storage.md).
