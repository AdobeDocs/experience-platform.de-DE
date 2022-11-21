---
keywords: Experience Platform; Startseite; beliebte Themen; Quellen; Connectoren; oracle;
title: (Beta) Erstellen einer Oracle Responsys-Quellverbindung über die Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie Adobe Experience Platform über die Platform-Benutzeroberfläche mit Oracle Responsys verbinden.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: 784ec5f799c591185620e8376a6980b4930d914a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 40%

---

# (Beta) Erstellen Sie eine [!DNL Oracle Responsys] Quellverbindung über die Platform-Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Oracle Responsys] -Quelle befindet sich in der Beta-Phase. Siehe [Quellen – Übersicht](../../../../home.md#terms-and-conditions), um weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren zu erhalten.

In diesem Tutorial erfahren Sie, wie Sie eine [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Platform voraus:

* [Quellen](../../../../home.md): Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Wenn Sie bereits über eine authentifizierte [!DNL Oracle Responsys] -Konto in Platform verwenden, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zu [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung an Platform zu bringen](../../dataflow/marketing-automation.md).

### Sammeln erforderlicher Anmeldeinformationen

Um eine Verbindung herzustellen [!DNL Oracle Responsys] in Platform angeben, müssen Sie Werte für die folgenden Authentifizierungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Endpunkt | Die REST-Authentifizierungsendpunkt-URL Ihrer [!DNL Oracle Responsys] -Instanz. |
| Client-ID | Die Client-ID Ihrer [!DNL Oracle Responsys] -Instanz. |
| Client-Geheimnis | Das Client-Geheimnis Ihres [!DNL Oracle Responsys] -Instanz. |

Weitere Informationen zu Authentifizierungsberechtigungen für [!DNL Oracle Responsys], siehe [[!DNL Oracle Responsys] Authentifizierungshandbuch](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Oracle Responsys]-Konto mit Platform zu verknüpfen.

## Verbinden Sie Ihr [!DNL Oracle Responsys]-Konto

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem [!UICONTROL Marketing-Automatisierung] category, select **[!UICONTROL Oracle Responsys]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Der Adobe Experience Platform-Quellkatalog mit hervorgehobener Oracle Responsys-Quelle.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

Die **[!UICONTROL Oracle Responsys-Konto verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Oracle Responsys]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Der bestehende Bildschirm zur Kontoauthentifizierung für Oracle Responsys.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Neues Konto

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und die entsprechenden Werte für Ihre [!DNL Oracle Responsys] Anmeldedaten. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Der neue Bildschirm zur Kontoauthentifizierung für Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie sich authentifiziert und eine Quellverbindung zwischen Ihrer [!DNL Oracle Responsys] -Konto und -Plattform. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung an Platform zu bringen](../../dataflow/marketing-automation.md).
