---
keywords: Experience Platform;home;popular topics;onetrust;OneTrust
solution: Experience Platform
title: Erstellen einer OneTrust Source-Verbindung in der Benutzeroberfläche
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
>Die [!DNL OneTrust Integration]-Quelle unterstützt nur die Erfassung von Zustimmungs- und Voreinstellungsdaten und keine Cookies.

In diesem Tutorial erfahren Sie, wie Sie eine [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) -Quellverbindung erstellen, um sowohl historische als auch geplante Einwilligungsdaten über die Platform-Benutzeroberfläche in Adobe Experience Platform zu erfassen.

## Voraussetzungen

>[!IMPORTANT]
>
>Der Quell-Connector und die Dokumentation für [!DNL OneTrust Integration] wurden vom [!DNL OneTrust Integration]-Team erstellt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an das [[!DNL OneTrust] Team](https://my.onetrust.com/s/contactsupport?language=en_US).

Bevor Sie [!DNL OneTrust Integration] mit Platform verbinden können, müssen Sie zunächst Ihr Zugriffstoken abrufen. Detaillierte Anweisungen zum Auffinden Ihres Zugriffstokens finden Sie im [[!DNL OneTrust Integration] OAuth 2-Handbuch](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

Das Zugriffstoken wird nach seinem Ablauf nicht automatisch aktualisiert, da die Aktualisierungstoken des Systems nicht von [!DNL OneTrust] unterstützt werden. Daher müssen Sie sicherstellen, dass Ihr Zugriffstoken in der Verbindung aktualisiert wird, bevor es abläuft. Die maximale konfigurierbare Lebensdauer für ein Zugriffstoken beträgt ein Jahr. Weitere Informationen zum Aktualisieren Ihres Zugriffstokens finden Sie im Dokument [[!DNL OneTrust] zur Verwaltung Ihrer OAuth 2.0-Client-Anmeldedaten](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Sammeln erforderlicher Anmeldeinformationen

Um [!DNL OneTrust Integration] mit Platform zu verbinden, müssen Sie Werte für die folgenden Authentifizierungsberechtigungen angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Hostname | Die Umgebung, aus der die [!DNL OneTrust Integration] -Daten abgerufen werden müssen. | `app.onetrust.com` |
| Autorisierungstest-URL | (Optional) Die URL für den Autorisierungstest wird verwendet, um Anmeldeinformationen beim Erstellen einer Basisverbindung zu überprüfen. Wenn die Anmeldeinformationen nicht angegeben sind, werden sie stattdessen während des Erstellungsschritts der Quellverbindung automatisch überprüft. | |
| Zugriffs-Token | Das Zugriffstoken, das Ihrem [!DNL OneTrust Integration] -Konto entspricht. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Weitere Informationen zu diesen Anmeldedaten finden Sie in der [[!DNL OneTrust Integration] Authentifizierungsdokumentation](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Verbinden Ihres [!DNL OneTrust Integration]-Kontos

>[!NOTE]
>
>Die [!DNL OneTrust Integration]-API-Spezifikationen werden für die Datenerfassung mit Adobe freigegeben.

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich die Option **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich [!UICONTROL Quellen] für einen in Experience Platform verfügbaren Quellkatalog zuzugreifen.

Verwenden Sie das Menü *[!UICONTROL Kategorien]* , um Quellen nach Kategorie zu filtern. Geben Sie alternativ einen Quellnamen in die Suchleiste ein, um eine bestimmte Quelle aus dem Katalog zu finden.

Gehen Sie zur Kategorie [!UICONTROL Einverständnis &amp; Voreinstellungen] für die Quellkarte [!DNL OneTrust Integration]. Wählen Sie zunächst **[!UICONTROL Daten hinzufügen]** aus.

![Der Quellenkatalog für die Experience Platform-Benutzeroberfläche.](../../../../images/tutorials/create/onetrust/catalog.png)

Die Seite **[!UICONTROL OneTrust-Integrationskonto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL OneTrust Integration]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Der vorhandene Schritt zur Kontoauthentifizierung im Quellen-Workflow.](../../../../images/tutorials/create/onetrust/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Der neue Schritt zur Kontoauthentifizierung im Ursprungs-Workflow.](../../../../images/tutorials/create/onetrust/new.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL OneTrust Integration]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss konfigurieren, um Einwilligungsdaten in Platform](../../dataflow/consent-and-preferences.md) zu importieren.[
