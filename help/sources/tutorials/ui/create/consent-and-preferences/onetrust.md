---
keywords: Experience Platform; home; beliebte Themen; onetrust; OneTrust
solution: Experience Platform
title: (Beta) Erstellen einer OneTrust Source-Verbindung in der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine OneTrust-Quellverbindung erstellen.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 38%

---

# (Beta) Erstellen Sie eine [!DNL OneTrust Integration] Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL OneTrust Integration]-Quelle befindet sich in der Beta-Phase. Die Funktionen und Dokumentation können sich ändern. Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellen - Übersicht](../../../../home.md#terms-and-conditions).

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
| Hostname | Die Umgebung, aus der die [!DNL OneTrust Integration] -Daten abgerufen werden. | `https://uat.onetrust.com/` |
| Autorisierungstest-URL | (Optional) Die URL für den Autorisierungstest wird verwendet, um Anmeldeinformationen beim Erstellen einer Basisverbindung zu überprüfen. Wenn die Anmeldeinformationen nicht angegeben sind, werden sie stattdessen während des Erstellungsschritts der Quellverbindung automatisch überprüft. |  |
| Zugriffs-Token | Das Zugriffstoken, das dem [!DNL OneTrust Integration] -Konto. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Weitere Informationen zu diesen Anmeldedaten finden Sie im Abschnitt [[!DNL OneTrust Integration] Authentifizierungsdokumentation](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Verbinden Ihres [!DNL OneTrust Integration]-Kontos

>[!NOTE]
>
>Die [!DNL OneTrust Integration] API-Spezifikationen werden für Adobe zur Datenerfassung freigegeben.

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem *[!UICONTROL Einverständnis und Voreinstellungen]* category, select [!DNL OneTrust Integration]und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/onetrust/catalog.png)

Die **[!UICONTROL OneTrust-Integrationskonto verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL OneTrust Integration]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/onetrust/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre -Anmeldedaten an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/onetrust/new.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL OneTrust Integration]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Datenfluss konfigurieren, um Einwilligungsdaten in Platform zu importieren](../../dataflow/consent-and-preferences.md).
