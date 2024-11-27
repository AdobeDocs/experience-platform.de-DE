---
title: Erstellen einer Oracle Eloqua-Quellverbindung über die Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie Adobe Experience Platform über die Platform-Benutzeroberfläche mit Oracle Eloqua verbinden.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: 9ca4f19f7b59f075250bce7035303e11d3f3710f
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 59%

---

# Erstellen einer Quellverbindung mit [!DNL Oracle Eloqua] über die Platform-Benutzeroberfläche

>[!WARNING]
>
>Die Quelle [!DNL Oracle Eloqua] wird Ende Juni 2025 eingestellt.

In diesem Tutorial werden die Schritte zum Erstellen einer 0-Quell-Verbindung mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.[!DNL Oracle Eloqua]

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Platform voraus:

* [Quellen](../../../../home.md): Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Wenn Sie bereits über ein authentifiziertes [!DNL Oracle Eloqua]-Konto in Platform verügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung in Platform aufzunehmen](../../dataflow/marketing-automation.md) fortfahren.

### Sammeln erforderlicher Anmeldedaten

Um eine Verbindung zwischen [!DNL Oracle Eloqua] und Platform herzustellen, müssen Sie Werte für die folgenden Authentifizierungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Endpunkt | Der Endpunkt Ihres [!DNL Oracle Eloqua] -Servers. [!DNL Oracle Eloqua] unterstützt mehrere Rechenzentren. Um Ihren Endpunkt zu finden, melden Sie sich mit Ihren Anmeldeinformationen bei der [[!DNL Oracle Eloqua] Schnittstelle](https://login.eloqua.com) an und kopieren Sie dann den Basis-URL-Teil aus der Umleitungs-URL. Das Format für Ihr URL-Muster ist `xxx.xx.eloqua.com` und sollte ohne `http` oder `https` eingegeben werden. |
| Benutzername | Der Benutzername Ihres [!DNL Oracle Eloqua] -Servers. Der Benutzername muss als `siteName + \\ + username` formatiert sein, wobei `siteName` der Unternehmensname ist, mit dem Sie sich bei [!DNL Oracle Eloqua] angemeldet haben, und `username` Ihr Benutzername. Ihr Benutzername für die Anmeldung kann beispielsweise: `Eloqua\Andy` lauten. **Hinweis**: Bei Verwendung der Benutzeroberfläche müssen Sie einen einzelnen umgekehrten Schrägstrich (`\`) verwenden, da die Experience Platform-Benutzeroberfläche bei der Eingabe eines Benutzernamens automatisch einen zusätzlichen umgekehrten Schrägstrich (`\`) hinzufügt. |
| Kennwort | Das Kennwort, das Ihrem [!DNL Oracle Eloqua]-Benutzernamen entspricht. |

Weitere Informationen zu Authentifizierungs-Anmeldedaten für [!DNL Oracle Eloqua] finden Sie im [[!DNL Oracle Eloqua] Authentifizierungshandbuch](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Nachdem Sie die erforderlichen Anmeldedaten zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Oracle Eloqua]-Konto mit Platform zu verknüpfen.

## Verbinden Sie Ihr [!DNL Oracle Eloqua]-Konto

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Marketing-Automatisierung] die Option **[!UICONTROL Oracle Eloqua]** und dann **[!UICONTROL Daten hinzufügen]** aus.

![Katalog](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

Die Seite **[!UICONTROL Oracle Eloqua-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Oracle Eloqua]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und die entsprechenden Werte für Ihre [!DNL Oracle Eloqua]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Quellverbindung zwischen Ihrem [!DNL Oracle Eloqua]-Konto und Platform authentifiziert und hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen [Datenfluss erstellen, um Daten zur Marketing-Automatisierung in Platform aufzunehmen](../../dataflow/marketing-automation.md).
