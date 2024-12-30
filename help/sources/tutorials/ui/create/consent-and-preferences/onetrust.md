---
keywords: Experience Platform;Startseite;beliebte Themen;onetrust;OneTrust
solution: Experience Platform
title: Erstellen einer OneTrust Source-Verbindung über die Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine OneTrust-Quellverbindung erstellen.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 23%

---

# Erstellen eines Quell-Connectors für [!DNL OneTrust Integration] in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL OneTrust Integration]-Quelle unterstützt nur die Aufnahme von Einverständnis- und Voreinstellungsdaten und nicht Cookies.

In diesem Tutorial werden Schritte zum Erstellen einer [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US)-Quellverbindung beschrieben, um historische und geplante Einverständnisdaten über die Platform-Benutzeroberfläche in Adobe Experience Platform aufzunehmen.

## Voraussetzungen

>[!IMPORTANT]
>
>Der [!DNL OneTrust Integration]-Quell-Connector und die Dokumentation wurden vom [!DNL OneTrust Integration]-Team erstellt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [[!DNL OneTrust] Team](https://my.onetrust.com/s/contactsupport?language=en_US).

Bevor Sie eine Verbindung zwischen [!DNL OneTrust Integration] und Platform herstellen können, müssen Sie zunächst Ihr Zugriffs-Token abrufen. Detaillierte Anweisungen zum Auffinden Ihres Zugriffs-Tokens finden Sie im [[!DNL OneTrust Integration] OAuth 2-Handbuch](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

Das Zugriffstoken wird nach Ablauf nicht automatisch aktualisiert, da System-zu-System-Aktualisierungstoken von [!DNL OneTrust] nicht unterstützt werden. Daher müssen Sie sicherstellen, dass Ihr Zugriffstoken in der Verbindung aktualisiert wird, bevor es abläuft. Die konfigurierbare maximale Lebensdauer für ein Zugriffstoken beträgt ein Jahr. Weitere Informationen zum Aktualisieren Ihres Zugriffstokens finden Sie unter [[!DNL OneTrust] Verwalten Ihrer OAuth 2.0-Client-Anmeldeinformationen](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Sammeln erforderlicher Anmeldedaten

Um [!DNL OneTrust Integration] mit Platform zu verbinden, müssen Sie Werte für die folgenden Authentifizierungsdaten angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Hostname | Die Umgebung, aus der die [!DNL OneTrust Integration] Daten abgerufen werden müssen. | `app.onetrust.com` |
| URL für den Autorisierungstest | (Optional) Die URL für den Autorisierungstest wird verwendet, um Anmeldedaten beim Erstellen einer Basisverbindung zu überprüfen. Wenn die Anmeldedaten nicht angegeben sind, werden sie stattdessen während des Erstellungsschritts der Quellverbindung automatisch überprüft. | |
| Zugriffs-Token | Das Zugriffstoken, das Ihrem [!DNL OneTrust Integration]-Konto entspricht. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Weitere Informationen zu diesen Anmeldeinformationen finden Sie unter [[!DNL OneTrust Integration] Authentifizierungsdokumentation](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Verbinden Ihres [!DNL OneTrust Integration]-Kontos

>[!NOTE]
>
>Die [!DNL OneTrust Integration] API-Spezifikationen werden für Adobe zur Datenaufnahme freigegeben.

Wählen Sie in der Platform **[!UICONTROL Benutzeroberfläche die Option]** Quellen“ in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] für einen Quellenkatalog zuzugreifen, der auf Experience Platform verfügbar ist.

Verwenden Sie das Menü *[!UICONTROL Kategorien]*, um Quellen nach Kategorie zu filtern. Geben Sie alternativ einen Quellnamen in die Suchleiste ein, um eine bestimmte Quelle aus dem Katalog zu finden.

Gehen Sie zur Kategorie [!UICONTROL Einverständnis und Voreinstellungen] für die [!DNL OneTrust Integration]. Wählen Sie zunächst **[!UICONTROL Daten hinzufügen]** aus.

![Der Quellkatalog der Experience Platform-Benutzeroberfläche.](../../../../images/tutorials/create/onetrust/catalog.png)

Die **[!UICONTROL Connect OneTrust Integration-Konto]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL OneTrust Integration]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Der Schritt zur Authentifizierung eines vorhandenen Kontos im Quell-Workflow.](../../../../images/tutorials/create/onetrust/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre -Anmeldeinformationen an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Der Schritt zur Authentifizierung eines neuen Kontos im Quell-Workflow.](../../../../images/tutorials/create/onetrust/new.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL OneTrust Integration]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Einverständnisdaten in Platform zu importieren](../../dataflow/consent-and-preferences.md).
