---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
solution: Experience Platform
title: Erstellen einer Quellverbindung für MailChimp-Kampagnen mithilfe der Experience Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Experience Platform-Benutzeroberfläche mit MailChimp-Kampagnen verbinden.
exl-id: e8e1ed32-4277-44c9-aafc-6bb9e0a1fe0d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 63%

---

# Erstellen einer [!DNL Mailchimp Campaigns] Quellverbindung mithilfe der Experience Platform-Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Mailchimp]-Quell-Connectors erläutert, um [!DNL Mailchimp Campaigns]-Daten über die Benutzeroberfläche in Adobe Experience Platform aufzunehmen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

## Sammeln erforderlicher Anmeldedaten

Um Ihre [!DNL Mailchimp Campaigns] Daten in Experience Platform einzubringen, müssen Sie zunächst die Authentifizierungsdaten angeben, die Ihrem [!DNL Mailchimp] entsprechen.

Die [!DNL Mailchimp Campaigns]-Quelle unterstützt sowohl OAuth 2-Aktualisierungs-Code als auch die einfache Authentifizierung. Weitere Informationen zu diesen Authentifizierungstypen finden Sie in den Tabellen unten.

### OAuth 2-Aktualisierungs-Code

| Anmeldedaten | Beschreibung |
| --- | --- |
| Domain | Die Stamm-URL, die für die Verbindung mit der MailChimp-API verwendet wird. Das Format für die Stamm-URL lautet `https://{DC}.api.mailchimp.com`, wobei `{DC}` das Rechenzentrum darstellt, das Ihrem Konto entspricht. |
| URL für den Autorisierungstest | Die URL für den Autorisierungstest wird verwendet, um Anmeldeinformationen beim Herstellen einer Verbindung von [!DNL Mailchimp] mit Experience Platform zu überprüfen. Wenn dies nicht angegeben wird, werden die Anmeldedaten stattdessen während des Erstellungsschritts der Quellverbindung automatisch überprüft. |
| Zugriffs-Token | Das entsprechende Zugriffs-Token, das zum Authentifizieren Ihrer Quelle verwendet wird. Dies ist für die OAuth-basierte Authentifizierung erforderlich. |

Weitere Informationen zur Verwendung von OAuth 2 zum Authentifizieren Ihres [!DNL Mailchimp]-Kontos für Experience Platform finden Sie in diesem [[!DNL Mailchimp] Dokument zur Verwendung von OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

### Einfache Authentifizierung

| Anmeldedaten | Beschreibung |
| --- | --- |
| Domain | Die Stamm-URL, die für die Verbindung mit der MailChimp-API verwendet wird. Das Format für die Stamm-URL lautet `https://{DC}.api.mailchimp.com`, wobei `{DC}` das Rechenzentrum darstellt, das Ihrem Konto entspricht. |
| Benutzername | Der Benutzername, der Ihrem MailChimp-Konto entspricht. Dies ist für die einfache Authentifizierung erforderlich. |
| Passwort | Das Passwort, das Ihrem MailChimp-Konto entspricht. Dies ist für die einfache Authentifizierung erforderlich. |

## Verbinden Ihres [!DNL Mailchimp Campaigns] mit Experience Platform

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie in der Kategorie [!UICONTROL Marketing-Automatisierung] die Option **[!UICONTROL Mailchimp-Kampagne]** und anschließend **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/mailchimp-campaigns/catalog.png)

Die Seite **[!UICONTROL Mailchimp-Kampagnenkonto verbinden]** wird angezeigt. Auf dieser Seite können Sie auswählen, ob Sie auf ein vorhandenes Konto zugreifen oder ein neues Konto erstellen möchten.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Mailchimp Campaigns]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/mailchimp-campaigns/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine Beschreibung für Ihre [!DNL Mailchimp Campaigns]-Quellverbindungsdetails an.

![neu](../../../../images/tutorials/create/mailchimp-campaigns/new.png)

#### Authentifizieren mit OAuth 2

Um OAuth 2 zu verwenden, wählen Sie [!UICONTROL OAuth 2-Aktualisierungs-Code] aus, geben Sie Werte für Ihre Domain, die URL für den Autorisierungstest und Zugriffs-Token an und klicken Sie auf **[!UICONTROL Verbindung mit Quelle herstellen]**. Warten Sie einige Augenblicke, bis Ihre Anmeldedaten validiert wurden, und wählen Sie dann **[!UICONTROL Weiter]** aus, um fortzufahren.

![oauth](../../../../images/tutorials/create/mailchimp-campaigns/oauth.png)

#### Authentifizieren mit Standardauthentifizierung

Um die Standardauthentifizierung zu verwenden, wählen Sie [!UICONTROL Standardauthentifizierung] aus, geben Sie Werte für Ihre Domain, Ihren Benutzernamen und Ihr Kennwort ein und wählen Sie dann **[!UICONTROL Mit Quelle verbinden]** aus. Warten Sie einige Augenblicke, bis Ihre Anmeldedaten validiert wurden, und wählen Sie dann **[!UICONTROL Weiter]** aus, um fortzufahren.

![De base](../../../../images/tutorials/create/mailchimp-campaigns/basic.png)

### Auswählen von [!DNL Mailchimp Campaigns]-Daten

Nachdem Ihre Quelle authentifiziert wurde, müssen Sie die `campaignId` angeben, die Ihrem [!DNL Mailchimp Campaigns]-Konto entspricht.

Geben Sie auf der Seite [!UICONTROL Daten auswählen] Ihre `campaignId` ein und wählen Sie **[!UICONTROL Erkunden]** aus.

![erkunden](../../../../images/tutorials/create/mailchimp-campaigns/explore.png)

Die Seite wird in eine interaktive Schemastruktur aktualisiert, in der Sie die Hierarchie Ihrer Daten analysieren und untersuchen können. Wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![select-data](../../../../images/tutorials/create/mailchimp-campaigns/select-data.png)

## Nächste Schritte

Nachdem Sie Ihr [!DNL Mailchimp]-Konto authentifiziert und Ihre [!DNL Mailchimp Campaigns] ausgewählt haben, können Sie jetzt mit der Erstellung eines Datenflusses beginnen, um Ihre Daten in Experience Platform zu übertragen. Ausführliche Anweisungen zum Erstellen eines Datenflusses finden Sie in der Dokumentation unter [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung in Experience Platform zu übertragen](../../dataflow/marketing-automation.md).
