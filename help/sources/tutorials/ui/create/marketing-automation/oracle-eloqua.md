---
title: Erstellen einer Oracle Eloqua-Quellverbindung mithilfe der Experience Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie Adobe Experience Platform über die Experience Platform-Benutzeroberfläche mit Oracle Eloqua verbinden.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: 7ff0709b62590bb80c1ed664368f28cdc4a950ea
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 25%

---

# Erstellen einer [!DNL Oracle Eloqua] Quellverbindung mithilfe der Experience Platform-Benutzeroberfläche

>[!WARNING]
>
>Die [!DNL Oracle Eloqua] wird im Januar 2026 eingestellt. Eine neue Quelle wird noch in diesem Jahr als Alternative veröffentlicht. Nach der Veröffentlichung der neuen Quelle müssen Sie die Migration zur neuen Quelle planen, indem Sie neue Kontoverbindungen und Datenflüsse vor Ende Januar 2026 erstellen.

In diesem Tutorial finden Sie die Schritte zum Erstellen einer [!DNL Oracle Eloqua]-Quellverbindung mithilfe der Benutzeroberfläche von Adobe Experience Platform.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Wenn Sie bereits über ein authentifiziertes [!DNL Oracle Eloqua]-Konto in Experience Platform verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung in Experience Platform aufzunehmen“ ](../../dataflow/marketing-automation.md).

### Sammeln erforderlicher Anmeldedaten

Um [!DNL Oracle Eloqua] mit Experience Platform zu verbinden, müssen Sie Werte für die folgenden Authentifizierungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Endpunkt | Der Endpunkt Ihres [!DNL Oracle Eloqua]. [!DNL Oracle Eloqua] unterstützt mehrere Rechenzentren. Um Ihren Endpunkt zu finden, melden Sie sich bei [[!DNL Oracle Eloqua] Schnittstelle](https://login.eloqua.com) mit Ihren -Anmeldeinformationen an und kopieren Sie dann den Teil der Basis-URL aus der Umleitungs-URL. Das Format für Ihr URL-Muster ist `xxx.xx.eloqua.com` und sollte ohne `http` oder `https` eingegeben werden. |
| Benutzername | Der Benutzername Ihres [!DNL Oracle Eloqua]. Der Benutzername muss als `siteName + \\ + username` formatiert sein, wobei `siteName` der Firmenname ist, mit dem Sie sich bei [!DNL Oracle Eloqua] anmelden, und `username` Ihr Benutzername. Ihr Anmelde-Benutzername kann beispielsweise lauten: `Eloqua\Andy`. **Hinweis**: Sie müssen bei der Verwendung der Benutzeroberfläche einen einzelnen umgekehrten Schrägstrich (`\`) verwenden, da die Experience Platform-Benutzeroberfläche bei der Eingabe eines Benutzernamens automatisch einen zusätzlichen umgekehrten Schrägstrich (`\`) hinzufügt. |
| Kennwort | Das Passwort, das Ihrem [!DNL Oracle Eloqua] Benutzernamen entspricht. |

Weitere Informationen zu Authentifizierungs-Anmeldedaten für [!DNL Oracle Eloqua] finden Sie im [[!DNL Oracle Eloqua] Authentifizierungshandbuch](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Oracle Eloqua]-Konto mit Experience Platform zu verknüpfen.

## Verbinden Ihres [!DNL Oracle Eloqua]-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Marketing] die Option **[!UICONTROL Oracle Eloqua]** und dann **[!UICONTROL Daten hinzufügen]** aus.

![Katalog](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

Die **[!UICONTROL Oracle Eloqua-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Oracle Eloqua]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und die entsprechenden Werte für Ihre [!DNL Oracle Eloqua]-Anmeldeinformationen an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Quellverbindung zwischen Ihrem [!DNL Oracle Eloqua]-Konto und Experience Platform authentifiziert und hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Datenfluss erstellen, um Daten zur Marketing-Automatisierung in Experience Platform zu übertragen](../../dataflow/marketing-automation.md).
