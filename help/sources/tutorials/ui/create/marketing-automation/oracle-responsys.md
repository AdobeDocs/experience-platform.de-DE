---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Oracle;
title: (Beta) Erstellen einer Oracle Responsys-Quellverbindung mithilfe der Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Platform-Benutzeroberfläche mit Oracle Responsys verbinden.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 97%

---

# (Beta) Erstellen einer [!DNL Oracle Responsys]-Quellverbindung mithilfe der Platform-Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Oracle Responsys]-Quelle befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../../../home.md#terms-and-conditions) Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren.

In diesem Tutorial werden die Schritte zum Erstellen einer [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md)-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Platform voraus:

* [Quellen](../../../../home.md): Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Wenn Sie bereits über ein authentifiziertes [!DNL Oracle Responsys]-Konto in Platform verügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung in Platform aufzunehmen](../../dataflow/marketing-automation.md) fortfahren.

### Sammeln erforderlicher Anmeldeinformationen

Um eine Verbindung zwischen [!DNL Oracle Responsys] und Platform herzustellen, müssen Sie Werte für die folgenden Authentifizierungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Endpunkt | Die REST-Authentifizierungsendpunkt-URL Ihrer [!DNL Oracle Responsys]-Instanz. |
| Client-ID | Die Client-ID Ihrer [!DNL Oracle Responsys]-Instanz. |
| Client-Geheimnis | Das Client-Geheimnis Ihrer [!DNL Oracle Responsys]-Instanz. |

Weitere Informationen zu Authentifizierungsdaten für [!DNL Oracle Responsys] finden Sie im [[!DNL Oracle Responsys] Authentifizierungshandbuch](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Oracle Responsys]-Konto mit Platform zu verknüpfen.

## Verbinden Sie Ihr [!DNL Oracle Responsys]-Konto

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie in der Kategorie [!UICONTROL Marketing-Automatisierung] die Option **[!UICONTROL Oracle Responsys]** und anschließend **[!UICONTROL Daten hinzufügen]** aus.

![Der Adobe Experience Platform-Quellkatalog mit hervorgehobener Oracle Responsys-Quelle.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

Die Seite **[!UICONTROL Oracle Responsys-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Oracle Responsys]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Der Bildschirm zur Authentifizierung eines vorhandenen Kontos für Oracle Responsys.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Neues Konto

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** aus und geben Sie dann einen Namen, eine optionale Beschreibung und die entsprechenden Werte für Ihre [!DNL Oracle Responsys]-Anmeldeinformationen an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Der Bildschirm für die Authentifizierung eines neuen Kontos für Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Quellverbindung zwischen Ihrem [!DNL Oracle Responsys]-Konto und Platform authentifiziert und hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen [Datenfluss erstellen, um Daten zur Marketing-Automatisierung in Platform aufzunehmen](../../dataflow/marketing-automation.md).
