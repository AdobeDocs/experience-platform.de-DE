---
keywords: Experience Platform; Startseite; beliebte Themen; Quellen; Connectoren; oracle; oracle eloqua; eloqua
solution: Experience Platform
title: Erstellen einer Oracle Eloqua-Quellverbindung über die Platform-Benutzeroberfläche
topic-legacy: tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform über die Platform-Benutzeroberfläche mit Oracle Eloqua verbinden.
source-git-commit: a40a1b8fae41c495afd9cdfc3c8d68148e90f2cd
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 4%

---


# Erstellen Sie eine [!DNL Oracle Eloqua] Quellverbindung über die Platform-Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Oracle Eloqua] Quell-Connector über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Platform voraus:

* [Quellen](../../../../home.md): Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

Wenn Sie bereits über eine authentifizierte [!DNL Oracle Eloqua] -Konto in Platform verwenden, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zu [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung an Platform zu bringen](../../dataflow/marketing-automation.md).

### Erforderliche Anmeldedaten sammeln

Um eine Verbindung herzustellen [!DNL Oracle Eloqua] in Platform angeben, müssen Sie Werte für die folgenden Authentifizierungseigenschaften angeben:

| Berechtigung | Beschreibung |
| --- | --- |
| Endpunkt | Der Endpunkt Ihrer [!DNL Oracle Eloqua]. |
| Benutzername | Der Benutzername Ihres [!DNL Oracle Eloqua] -Konto. Der Benutzername muss als `siteName + \\ + username`, wobei `siteName` ist der Unternehmensname, mit dem Sie sich bei [!DNL Oracle Eloqua] und `username` ist Ihr Benutzername. Der Benutzername für die Anmeldung kann beispielsweise wie folgt lauten: `adobe\\emily`. |
| Passwort | Das Passwort, das Ihrem [!DNL Oracle Eloqua] Benutzername. |

Weitere Informationen zu Authentifizierungsberechtigungen für [!DNL Oracle Eloqua], siehe [[!DNL Oracle Eloqua] Authentifizierungshandbuch](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Nachdem Sie die erforderlichen Anmeldedaten erfasst haben, können Sie die folgenden Schritte ausführen, um Ihre [!DNL Oracle Eloqua] -Konto auf Platform.

## Verbinden Sie Ihre [!DNL Oracle Eloqua] account

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über die linke Navigationsleiste auf [!UICONTROL Quellen] Arbeitsbereich. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem [!UICONTROL Marketing-Automatisierung] category, select **[!UICONTROL Oracle Eloqua]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

Die **[!UICONTROL Oracle Eloqua-Konto verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie die [!DNL Oracle Eloqua] Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, wählen Sie **[!UICONTROL Nächste]** um fortzufahren.

![vorhandene](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und die entsprechenden Werte für Ihre [!DNL Oracle Eloqua] Anmeldedaten. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbindung mit Quelle herstellen]** und dann etwas Zeit für die Einrichtung der neuen Verbindung.

![new](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie sich authentifiziert und eine Quellverbindung zwischen Ihrer [!DNL Oracle Eloqua] -Konto und -Plattform. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung an Platform zu bringen](../../dataflow/marketing-automation.md).

