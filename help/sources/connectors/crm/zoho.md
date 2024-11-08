---
keywords: Experience Platform;Startseite;beliebte Themen;Zoho CRM;Zoho crm;Zoho;Zoho
solution: Experience Platform
title: Übersicht über den Quell-Connector Zoho CRM
description: Erfahren Sie, wie Sie Zoho CRM über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 97%

---

# [!DNL Zoho CRM]

>[!WARNING]
>
>Die Quelle [!DNL Zoho CRM] wird Ende Juni 2025 eingestellt.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und zu verbessern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform bietet Unterstützung für die Aufnahme von Daten aus einem CRM-System eines Drittanbieters. Unterstützung für CRM-Anbieter umfasst [!DNL Zoho CRM].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Informationen finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Abrufen Ihrer Authentifizierungs-Anmeldedaten für [!DNL Zoho CRM]

Bevor Sie Daten aus Ihrem [!DNL Zoho CRM]-Konto auf Platform übertragen können, müssen Sie zunächst Ihre Anmeldedaten abrufen, um Ihre [!DNL Zoho CRM]-Quelle zu authentifizieren. Gehen Sie wie folgt vor, um Ihre Client-ID, Ihr Client-Geheimnis, Ihr Zugriffs-Token und Ihr Aktualisierungs-Token abzurufen.

### Registrieren Ihres Programms

Der erste Schritt zum Abrufen Ihrer Authentifizierungs-Anmeldedaten ist die Registrierung Ihres Programms über die [[!DNL Zoho CRM] Entwicklerkonsole](https://accounts.zoho.com/). Um Ihr Programm zu registrieren, müssen Sie Ihren Client-Typ unter folgendem Pfad auswählen: JavaScript, Web-basiert, Mobile Apps ohne Browser oder Self-Client. Geben Sie als Nächstes Werte für den Namen Ihres Programms, die URL Ihrer Web-Seite und einen autorisierten Umleitungs-URI an, den [!DNL Zoho CRM] dann verwenden kann, um Sie mit einem Grant-Token umzuleiten.

Bei erfolgreicher Registrierung werden Ihre Client-ID und das Client-Geheimnis angegeben.

### Erstellen einer Autorisierungsanfrage

Als Nächstes müssen Sie eine [Autorisierungsanfrage](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) erstellen, entweder mithilfe eines Web-basierten Programms oder mit einem Self-Client. Die Autorisierungsanfrage gibt Ihr Grant-Token an, mit dem Sie Ihr Zugriffs-Token abrufen können.

Bei der Erstellung einer Autorisierungsanfrage müssen Sie Werte für **Bereiche** und **Zugriffstyp** angeben. Weitere Informationen zu Bereichen finden Sie in diesem [[!DNL Zoho CRM] Dokument](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html), während Ihr **Zugriffstyp** immer auf `offline` festgelegt sein sollte.

### Erstellen Ihrer Zugriffs- und Aktualisierungs-Token

Nachdem Sie Ihr Grant-Token abgerufen haben, können Sie Ihre [Zugriffs- und Aktualisierungs-Token](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) erstellen, indem Sie eine POST-Anfrage an `{ACCOUNTS_URL}/oauth/v2/token` stellen, und dabei Ihre Client-ID, Ihr Client-Geheimnis, Ihr Grant-Token und die Umleitungs-URI angeben. In diesem Schritt müssen Sie auch `grant_type` als Parameter verwenden und den Wert auf `"authorization_code"` festlegen.

Bei einer erfolgreichen Anfrage werden Ihre Zugriffs- und Aktualisierungs-Token angegeben, die Sie dann zur Authentifizierung verwenden können.

Ausführliche Anweisungen zur Anforderung Ihrer Anmeldedaten finden Sie im [[!DNL Zoho CRM] Authentifizierungshandbuch](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Verbinden von [!DNL Zoho CRM] mit [!DNL Platform] mithilfe von APIs

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Zoho CRM] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

- [Erstellen einer  [!DNL Zoho CRM] -Basisverbindung mit der Flow Service-API](../../tutorials/api/create/crm/zoho.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine CRM-Quelle mithilfe der Flow Service-API](../../tutorials/api/collect/crm.md)

## Verbinden von [!DNL Zoho CRM] mit [!DNL Platform] über die Benutzeroberfläche

- [Erstellen einer  [!DNL Zoho CRM] -Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/crm/zoho.md)
- [Erstellen eines Datenflusses für eine CRM-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/crm.md)
