---
keywords: Experience Platform; Startseite; beliebte Themen; Zoho CRM; Zoho crm; Zoho; Zoho
solution: Experience Platform
title: Zoho CRM Source Connector - Übersicht
topic-legacy: overview
description: Erfahren Sie, wie Sie das Zoho CRM mit Adobe Experience Platform über APIs oder die Benutzeroberfläche verbinden.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 46b2fd6bc715bf1d8ccfeed576a2a2d193f92edd
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 3%

---

# [!DNL Zoho CRM]

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern mithilfe von [!DNL Platform] Dienste. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus einem Drittanbieter-CRM-System. Unterstützung für CRM-Anbieter umfasst [!DNL Zoho CRM].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Siehe [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md) für weitere Informationen.

## Abrufen Ihrer Authentifizierungsberechtigungen für [!DNL Zoho CRM]

Bevor Sie Daten aus Ihrem [!DNL Zoho CRM] -Konto für Platform verwenden, müssen Sie zunächst Ihre Anmeldedaten abrufen, um Ihre [!DNL Zoho CRM] -Quelle. Gehen Sie wie folgt vor, um Ihre Client-ID, Ihr Client-Geheimnis, Ihr Zugriffstoken und Ihr Aktualisierungstoken abzurufen.

### App registrieren

Der erste Schritt beim Abrufen Ihrer Authentifizierungsberechtigungen besteht darin, Ihre Anwendung mit dem [[!DNL Zoho CRM] Entwicklerkonsole](https://accounts.zoho.com/). Um Ihre Anwendung zu registrieren, müssen Sie Ihren Client-Typ unter folgendem Pfad auswählen: JavaScript, webbasierte, mobile, mobile, mobile Anwendungen ohne Browser oder Self-Client. Geben Sie als Nächstes Werte für den Namen Ihrer Anwendung, die URL Ihrer Webseite und einen autorisierten Weiterleitungs-URI an, der Folgendes ermöglicht: [!DNL Zoho CRM] können Sie dann verwenden, um Sie mit einem Grant-Token umzuleiten.

Bei erfolgreicher Registrierung werden Ihre Client-ID und das Client-Geheimnis zurückgegeben.

### Autorisierungsanfrage erstellen

Als Nächstes müssen Sie eine [Genehmigungsanfrage](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) entweder mit einer webbasierten Anwendung oder einem Self-Client. Die Autorisierungsanfrage gibt Ihr Grant-Token zurück, mit dem Sie Ihr Zugriffstoken abrufen können.

Bei der Erstellung einer Autorisierungsanfrage müssen Sie Werte für **Bereiche** und **Zugriffstyp**. Siehe hierzu [[!DNL Zoho CRM] Dokument](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) Weitere Informationen zu Bereichen finden Sie in der **Zugriffstyp** sollte immer auf `offline`.

### Zugriffs- und Aktualisierungstoken erstellen

Nachdem Sie Ihr Zuschuss-Token abgerufen haben, können Sie Ihre [Zugriffs- und Aktualisierungstoken](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) , indem Sie eine POST an `{ACCOUNTS_URL}/oauth/v2/token` bei der Bereitstellung Ihrer Client-ID, des Client-Geheimnisses, des Tokens für die Gewährung und der Weiterleitungs-URI. In diesem Schritt müssen Sie auch `grant_type` als Parameter verwenden und den Wert als `"authorization_code"`.

Bei einer erfolgreichen Anfrage werden Ihre Zugriffs- und Aktualisierungstoken zurückgegeben, die Sie dann zur Authentifizierung verwenden können.

Ausführliche Anweisungen zum Erwerb Ihrer Anmeldedaten finden Sie in der [[!DNL Zoho CRM] Authentifizierungshandbuch](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Verbinden [!DNL Zoho CRM] nach [!DNL Platform] Verwenden von APIs

Die folgende Dokumentation enthält Informationen zur Verbindung [!DNL Zoho CRM] zur Plattform mithilfe von APIs oder der Benutzeroberfläche:

- [Erstellen Sie eine [!DNL Zoho CRM] Basisverbindung mit der Flow Service-API](../../tutorials/api/create/crm/zoho.md)
- [Datenstruktur und Inhalt einer CRM-Quelle mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/crm.md)
- [Erstellen eines Datenflusses für eine CRM-Quelle mithilfe der Flow Service-API](../../tutorials/api/collect/crm.md)

## Verbinden [!DNL Zoho CRM] nach [!DNL Platform] über die Benutzeroberfläche

- [Erstellen Sie eine [!DNL Zoho CRM] Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/crm/zoho.md)
- [Erstellen eines Datenflusses für eine CRM-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/crm.md)
