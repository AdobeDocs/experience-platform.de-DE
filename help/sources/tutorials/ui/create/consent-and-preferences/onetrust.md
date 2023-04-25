---
keywords: Experience Platform; home; beliebte Themen; onetrust; OneTrust
solution: Experience Platform
title: Erstellen einer OneTrust-Quellverbindung in der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine OneTrust-Quellverbindung erstellen.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 26%

---

# Erstellen eines Quell-Connectors für [!DNL OneTrust Integration] in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL OneTrust Integration] -Quelle unterstützt nur die Erfassung von Einwilligungs- und Voreinstellungsdaten und keine Cookies.

In diesem Tutorial werden Schritte zum Erstellen eines [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) Quellverbindung zur Aufnahme von historischen und geplanten Einwilligungsdaten in Adobe Experience Platform über die Platform-Benutzeroberfläche.

## Voraussetzungen

>[!IMPORTANT]
>
>Die [!DNL OneTrust Integration] Quell-Connector und -Dokumentation wurden von der [!DNL OneTrust Integration] Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte an die [[!DNL OneTrust] Team](https://my.onetrust.com/s/contactsupport?language=en_US) direkt.

Bevor Sie eine Verbindung herstellen können [!DNL OneTrust Integration] in Platform verwenden, müssen Sie zunächst Ihr Zugriffstoken abrufen. Detaillierte Anweisungen zum Auffinden Ihres Zugriffstokens finden Sie unter [[!DNL OneTrust Integration] OAuth 2-Handbuch](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

Das Zugriffstoken wird nach seinem Ablauf nicht automatisch aktualisiert, da die Aktualisierungstoken des Systems nicht von [!DNL OneTrust]. Daher müssen Sie sicherstellen, dass Ihr Zugriffstoken in der Verbindung aktualisiert wird, bevor es abläuft. Die maximale konfigurierbare Lebensdauer für ein Zugriffstoken beträgt ein Jahr. Weitere Informationen zum Aktualisieren Ihres Zugriffstokens finden Sie unter [[!DNL OneTrust] Dokument zur Verwaltung Ihrer OAuth 2.0-Client-Anmeldedaten](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Sammeln erforderlicher Anmeldeinformationen

Um eine Verbindung herzustellen [!DNL OneTrust Integration] in Platform angeben, müssen Sie Werte für die folgenden Authentifizierungsberechtigungen angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Hostname | Die Umgebung, aus der die [!DNL OneTrust Integration] -Daten abgerufen werden. | `app.onetrust.com` |
| Autorisierungstest-URL | (Optional) Die URL für den Autorisierungstest wird verwendet, um Anmeldeinformationen beim Erstellen einer Basisverbindung zu überprüfen. Wenn die Anmeldeinformationen nicht angegeben sind, werden sie stattdessen während des Erstellungsschritts der Quellverbindung automatisch überprüft. |  |
| Zugriffs-Token | Das Zugriffstoken, das dem [!DNL OneTrust Integration] -Konto. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Weitere Informationen zu diesen Anmeldedaten finden Sie im Abschnitt [[!DNL OneTrust Integration] Authentifizierungsdokumentation](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Verbinden Ihres [!DNL OneTrust Integration]-Kontos

>[!NOTE]
>
>Die [!DNL OneTrust Integration] API-Spezifikationen werden für Adobe zur Datenerfassung freigegeben.

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über die linke Navigationsleiste auf [!UICONTROL Quellen] Arbeitsbereich für einen in Experience Platform verfügbaren Quellkatalog.

Verwenden Sie die *[!UICONTROL Kategorien]* Menü zum Filtern von Quellen nach Kategorie. Geben Sie alternativ einen Quellnamen in die Suchleiste ein, um eine bestimmte Quelle aus dem Katalog zu finden.

Navigieren Sie zu [!UICONTROL Einverständnis und Voreinstellungen] -Kategorie für [!DNL OneTrust Integration] Quellkarte. Wählen Sie zunächst **[!UICONTROL Daten hinzufügen]**.

![Der Quellenkatalog der Experience Platform-Benutzeroberfläche.](../../../../images/tutorials/create/onetrust/catalog.png)

Die **[!UICONTROL OneTrust-Integrationskonto verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL OneTrust Integration]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Der vorhandene Schritt zur Kontoauthentifizierung im Ursprungs-Workflow.](../../../../images/tutorials/create/onetrust/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre -Anmeldedaten an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Der neue Schritt zur Kontoauthentifizierung im Ursprungs-Workflow.](../../../../images/tutorials/create/onetrust/new.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL OneTrust Integration]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Datenfluss konfigurieren, um Einwilligungsdaten in Platform zu importieren](../../dataflow/consent-and-preferences.md).
