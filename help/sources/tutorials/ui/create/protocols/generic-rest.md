---
keywords: Experience Platform;Startseite;beliebte Themen;generische REST-API
title: Erstellen einer generischen Source-REST-API-Verbindung über die Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine generische REST-API-Quellverbindung erstellen.
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 23%

---

# Erstellen eines Quell-Connectors für [!DNL Generic REST API] in der Benutzeroberfläche

>[!NOTE]
>
> Die [!DNL Generic REST API]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Connectoren finden Sie ](../../../../home.md#terms-and-conditions) „Quellen - Übersicht“ .

In diesem Tutorial finden Sie die Schritte zum Erstellen eines [!DNL Generic REST API]-Quell-Connectors mithilfe der Benutzeroberfläche von Adobe Experience Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

### Sammeln erforderlicher Anmeldedaten

Um auf Ihr [!DNL Generic REST API]-Konto in Experience Platform zugreifen zu können, müssen Sie gültige Anmeldeinformationen für den Authentifizierungstyp Ihrer Wahl angeben. Die generische REST-API unterstützt sowohl OAuth 2-Aktualisierungs-Code als auch die Standardauthentifizierung. In den folgenden Tabellen finden Sie Informationen zu den Anmeldeinformationen für die beiden unterstützten Authentifizierungstypen.

#### OAuth 2-Aktualisierungs-Code

| Anmeldedaten | Beschreibung |
| --- | --- |
| Host | Die Host-URL der Quelle, an die Sie Ihre Anfrage stellen. Dieser Wert ist erforderlich und kann nicht mit der Überschreibung von Anfrageparametern umgangen werden. |
| URL für den Autorisierungstest | (Optional) Die URL für den Autorisierungstest wird verwendet, um Anmeldedaten beim Erstellen einer Basisverbindung zu überprüfen. Wenn die Anmeldedaten nicht angegeben sind, werden sie stattdessen während des Erstellungsschritts der Quellverbindung automatisch überprüft. |
| Client-ID | (Optional) Die mit Ihrem Benutzerkonto verknüpfte Client-ID. |
| Client-Geheimnis | (Optional) Das mit Ihrem Benutzerkonto verknüpfte Client-Geheimnis. |
| Zugriffs-Token | Die primären Authentifizierungsberechtigungen, die für den Zugriff auf Ihr Programm verwendet werden. Das Zugriffs-Token stellt die Autorisierung Ihrer Anwendung für den Zugriff auf bestimmte Aspekte der Daten eines Benutzers dar. Dieser Wert ist erforderlich und kann nicht mit der Überschreibung von Anfrageparametern umgangen werden. |
| Token aktualisieren | (Optional) Ein Token, mit dem ein neues Zugriffstoken generiert wird, wenn das Zugriffstoken abgelaufen ist. |
| Zugriffstoken-URL | (Optional) Der URL-Endpunkt, der zum Abrufen Ihres Zugriffs-Tokens verwendet wird. |
| Parameterüberschreibung bei Anfragen | (Optional) Eine Eigenschaft, mit der Sie angeben können, welche Berechtigungsparameter überschrieben werden sollen. |


#### Einfache Authentifizierung

| Anmeldedaten | Beschreibung |
| --- | --- |
| Host | Die Host-URL der Quelle, an die Sie Ihre Anfrage stellen. |
| Benutzername | Der Benutzername, der Ihrem Benutzerkonto entspricht. |
| Kennwort | Das Passwort, das Ihrem Benutzerkonto entspricht. |

## Verbinden Ihres allgemeinen REST-API-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter [!UICONTROL  Kategorie ] die Option **[!UICONTROL Generische REST-]**) und dann **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/generic-rest/catalog.png)

Die **[!UICONTROL Verbindung zur generischen REST-API herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das generische REST-API-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/generic-rest/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine Optionsbeschreibung für Ihr neues [!DNL Generic REST API] Konto an.

![neu](../../../../images/tutorials/create/generic-rest/new.png)

#### Authentifizieren mit OAuth 2-Aktualisierungs-Code

[!DNL Generic REST API] unterstützt sowohl OAuth 2-Aktualisierungs-Code als auch die Standardauthentifizierung. Um sich mit einer OAuth2-Authentifizierung zu authentifizieren, wählen Sie **[!UICONTROL OAuth2RefreshCode]**, geben Sie Ihre OAuth 2-Anmeldeinformationen ein und wählen Sie dann **[!UICONTROL Mit Quelle verbinden]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### Authentifizieren mit Standardauthentifizierung

Um die Standardauthentifizierung zu verwenden, wählen Sie **[!UICONTROL Standardauthentifizierung]**, geben Sie Ihren Host, Ihren Benutzernamen und Ihr Kennwort ein und wählen Sie dann **[!UICONTROL Mit Quelle verbinden]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem generischen REST-API-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in Experience Platform zu importieren](../../dataflow/protocols.md).
