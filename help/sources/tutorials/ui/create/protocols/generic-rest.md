---
keywords: Experience Platform; Startseite; beliebte Themen; generische REST-API
title: Erstellen einer generischen REST API-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine generische REST-API-Quellverbindung erstellen.
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 1a9c4d5ba3ba9201378e78c0e92dea5101668a24
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 8%

---

# Erstellen Sie eine [!DNL Generic REST API] Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
> Die [!DNL Generic REST API] -Quelle befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../../../home.md#terms-and-conditions) Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren.

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Generic REST API] Quell-Connector über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Erforderliche Anmeldedaten sammeln

Um auf Ihre [!DNL Generic REST API] -Konto auf Platform verwenden, müssen Sie gültige Anmeldeinformationen für den Authentifizierungstyp Ihrer Wahl angeben. Die generische REST-API unterstützt sowohl OAuth 2-Aktualisierungscode als auch einfache Authentifizierung. In den folgenden Tabellen finden Sie Informationen zu den Anmeldeinformationen für die beiden unterstützten Authentifizierungstypen.

#### OAuth 2-Aktualisierungscode

| Berechtigung | Beschreibung |
| --- | --- |
| Host | Die Host-URL der Quelle, an die Sie Ihre Anfrage richten. Dieser Wert ist erforderlich und kann nicht mit der Außerkraftsetzung von Anforderungsparametern umgangen werden. |
| Autorisierungstest-URL | (Optional) Die URL für den Autorisierungstest wird verwendet, um Anmeldeinformationen beim Erstellen einer Basisverbindung zu überprüfen. Wenn die Anmeldeinformationen nicht angegeben sind, werden sie stattdessen während des Erstellungsschritts der Quellverbindung automatisch überprüft. |
| Client-ID | (Optional) Die mit Ihrem Benutzerkonto verknüpfte Client-ID. |
| Client-Geheimnis | (Optional) Das mit Ihrem Benutzerkonto verknüpfte Client-Geheimnis. |
| Zugriffstoken | Die primäre Authentifizierungsberechtigung für den Zugriff auf Ihre Anwendung. Das Zugriffstoken stellt die Autorisierung Ihrer Anwendung dar, um auf bestimmte Aspekte der Daten eines Benutzers zuzugreifen. Dieser Wert ist erforderlich und kann nicht mit der Außerkraftsetzung von Anforderungsparametern umgangen werden. |
| Aktualisierungstoken | (Optional) Ein Token, mit dem ein neues Zugriffstoken generiert wird, wenn das Zugriffstoken abgelaufen ist. |
| Zugriffstoken-URL | (Optional) Der URL-Endpunkt, der zum Abrufen Ihres Zugriffstokens verwendet wird. |
| Außerkraftsetzen von Anforderungsparametern | (Optional) Eine Eigenschaft, mit der Sie angeben können, welche Berechtigungsparameter überschrieben werden sollen. |


#### Grundlegende Authentifizierung

| Berechtigung | Beschreibung |
| --- | --- |
| Host | Die Host-URL der Quelle, an die Sie Ihre Anfrage richten. |
| Benutzername | Der Benutzername, der Ihrem Benutzerkonto entspricht. |
| Passwort | Das Kennwort, das Ihrem Benutzerkonto entspricht. |

## Generisches REST-API-Konto verbinden

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über die linke Navigationsleiste auf [!UICONTROL Quellen] Arbeitsbereich. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Unter dem [!UICONTROL Protokolle] category, select **[!UICONTROL Generische REST-API]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/generic-rest/catalog.png)

Die **[!UICONTROL Verbindung zur generischen REST-API herstellen]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das generische REST-API-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Nächste]** um fortzufahren.

![vorhandene](../../../../images/tutorials/create/generic-rest/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine Optionsbeschreibung für Ihre neue [!DNL Generic REST API] -Konto.

![new](../../../../images/tutorials/create/generic-rest/new.png)

#### Authentifizieren Sie sich mit dem OAuth 2-Aktualisierungscode.

[!DNL Generic REST API] unterstützt sowohl OAuth 2-Aktualisierungscode als auch einfache Authentifizierung. Um sich mit einer OAuth2-Authentifizierung zu authentifizieren, wählen Sie **[!UICONTROL OAuth2RefreshCode]**, geben Sie Ihre OAuth 2-Anmeldeinformationen ein und wählen Sie dann **[!UICONTROL Verbindung mit Quelle herstellen]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### Authentifizierung mit einfacher Authentifizierung

Um die einfache Authentifizierung zu verwenden, wählen Sie **[!UICONTROL Grundlegende Authentifizierung]**, geben Sie Ihren Host, Benutzernamen und Ihr Kennwort ein und wählen Sie **[!UICONTROL Verbindung mit Quelle herstellen]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem generischen REST-API-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Datenfluss konfigurieren, um Daten in Platform zu importieren](../../dataflow/protocols.md).
