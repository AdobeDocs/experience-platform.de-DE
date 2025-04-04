---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Oracle;
title: (Beta) Erstellen einer Oracle Responsys-Quellverbindung mithilfe der Experience Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Experience Platform-Benutzeroberfläche mit Oracle Responsys verbinden.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 54%

---

# (Beta) Erstellen einer [!DNL Oracle Responsys] Quellverbindung mithilfe der Experience Platform-Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Oracle Responsys]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Connectoren finden Sie ](../../../../home.md#terms-and-conditions) „Quellen - Übersicht“ .

In diesem Tutorial werden die Schritte zum Erstellen einer [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md)-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Wenn Sie bereits über ein authentifiziertes [!DNL Oracle Responsys]-Konto in Experience Platform verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung in Experience Platform aufzunehmen“ ](../../dataflow/marketing-automation.md).

### Sammeln erforderlicher Anmeldedaten

Um [!DNL Oracle Responsys] mit Experience Platform zu verbinden, müssen Sie Werte für die folgenden Authentifizierungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Endpunkt | Die REST-Authentifizierungsendpunkt-URL Ihrer [!DNL Oracle Responsys]-Instanz. |
| Client-ID | Die Client-ID Ihrer [!DNL Oracle Responsys]-Instanz. |
| Client-Geheimnis | Das Client-Geheimnis Ihrer [!DNL Oracle Responsys]-Instanz. |

Weitere Informationen zu Authentifizierungs-Anmeldedaten für [!DNL Oracle Responsys] finden Sie im [[!DNL Oracle Responsys] Authentifizierungshandbuch](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Oracle Responsys]-Konto mit Experience Platform zu verknüpfen.

## Verbinden Ihres [!DNL Oracle Responsys]-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie in der Kategorie [!UICONTROL Marketing-Automatisierung] die Option **[!UICONTROL Oracle Responsys]** und anschließend **[!UICONTROL Daten hinzufügen]** aus.

![Der Adobe Experience Platform-Quellkatalog mit hervorgehobener Oracle Responsys-Quelle.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

Die Seite **[!UICONTROL Oracle Responsys-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Oracle Responsys]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Der Bildschirm zur Authentifizierung eines vorhandenen Kontos für Oracle Responsys.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Neues Konto

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** aus und geben Sie dann einen Namen, eine optionale Beschreibung und die entsprechenden Werte für Ihre [!DNL Oracle Responsys]-Anmeldedaten an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Der Bildschirm für die Authentifizierung eines neuen Kontos für Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Quellverbindung zwischen Ihrem [!DNL Oracle Responsys]-Konto und Experience Platform authentifiziert und hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Datenfluss erstellen, um Daten zur Marketing-Automatisierung in Experience Platform zu übertragen](../../dataflow/marketing-automation.md).
