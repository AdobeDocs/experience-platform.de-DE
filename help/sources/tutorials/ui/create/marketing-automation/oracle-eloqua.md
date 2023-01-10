---
keywords: Experience Platform; Startseite; beliebte Themen; Quellen; Connectoren; oracle; oracle eloqua; eloqua
solution: Experience Platform
title: Erstellen einer Oracle Eloqua-Quellverbindung über die Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie Adobe Experience Platform über die Platform-Benutzeroberfläche mit Oracle Eloqua verbinden.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 68%

---

# Erstellen einer [!DNL Oracle Eloqua]-Quellverbindung mithilfe der Platform-Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Oracle Eloqua] Quell-Connector über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Platform voraus:

* [Quellen](../../../../home.md): Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Wenn Sie bereits über ein authentifiziertes [!DNL Oracle Eloqua]-Konto in Platform verügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung in Platform aufzunehmen](../../dataflow/marketing-automation.md) fortfahren.

### Sammeln erforderlicher Anmeldeinformationen

Um eine Verbindung zwischen [!DNL Oracle Eloqua] und Platform herzustellen, müssen Sie Werte für die folgenden Authentifizierungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Endpunkt | Der Endpunkt Ihrer [!DNL Oracle Eloqua]. |
| Benutzername | Der Benutzername Ihres [!DNL Oracle Eloqua] -Konto. Der Benutzername muss als `siteName + \\ + username`, wobei `siteName` ist der Unternehmensname, mit dem Sie sich bei [!DNL Oracle Eloqua] und `username` ist Ihr Benutzername. Der Benutzername für die Anmeldung kann beispielsweise wie folgt lauten: `adobe\\emily`. |
| Kennwort | Das Passwort, das Ihrem [!DNL Oracle Eloqua] Benutzername. |

Weitere Informationen zu Authentifizierungsdaten für [!DNL Oracle Eloqua] finden Sie im [[!DNL Oracle Eloqua] Authentifizierungshandbuch](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Oracle Eloqua]-Konto mit Platform zu verknüpfen.

## Verbinden Sie Ihr [!DNL Oracle Eloqua]-Konto

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem [!UICONTROL Marketing-Automatisierung] category, select **[!UICONTROL Oracle Eloqua]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

Die **[!UICONTROL Oracle Eloqua-Konto verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Oracle Eloqua]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und die entsprechenden Werte für Ihre [!DNL Oracle Eloqua] Anmeldedaten. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Quellverbindung zwischen Ihrem [!DNL Oracle Eloqua]-Konto und Platform authentifiziert und hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen [Datenfluss erstellen, um Daten zur Marketing-Automatisierung in Platform aufzunehmen](../../dataflow/marketing-automation.md).
