---
keywords: Experience Platform;home;beliebte Themen;Zoho CRM;zoho crm;Zoho;Zoho
solution: Experience Platform
title: Übersicht über Zoho CRM Source Connector
topic-legacy: overview
description: Erfahren Sie, wie Sie Zoho CRM über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: fcd7af48-e66a-4313-bbfe-73301d335c67
source-git-commit: 7a15090d8ed2c1016d7dc4d7d3d0656640c4785c
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 3%

---

# (Betaversion) [!DNL Zoho CRM]

>[!NOTE]
>
>Die [!DNL Zoho CRM] Quelle befindet sich in der Beta-Version. Siehe [Quellübersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-gekennzeichneten Steckverbindern.

Adobe Experience Platform ermöglicht die Erfassung von Daten aus externen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Dienstleistungen. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt das Erfassen von Daten aus einem CRM-System eines Drittanbieters. Unterstützung für CRM-Anbieter umfasst [!DNL Zoho CRM].

## IP-Adresse Zulassungsliste

Vor dem Arbeiten mit Quellschnittstellen muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regional spezifische IP-Adresse nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungsmängeln führen. Siehe [IP-Adresse Zulassungsliste](../../ip-address-allow-list.md) für weitere Informationen.

## Authentifizierungsinformationen abrufen für [!DNL Zoho CRM]

Bevor Sie Daten von [!DNL Zoho CRM] Konto auf Platform, müssen Sie zunächst Ihre Anmeldedaten abrufen, um Ihre [!DNL Zoho CRM] Quelle. Führen Sie die folgenden Schritte aus, um Ihre Client-ID, das Kundengeheimnis, das Zugriffstoken und das Aktualisierungstoken abzurufen.

### Anwendung registrieren

Der erste Schritt beim Abrufen Ihrer Authentifizierungsberechtigungen besteht darin, Ihre Anwendung mit dem [[!DNL Zoho CRM] Entwicklerkonsole](https://accounts.zoho.com/). Um Ihre Anwendung zu registrieren, müssen Sie Ihren Clienttyp auswählen aus: JavaScript, webbasierte, mobile, mobile Anwendungen, mobile Anwendungen ohne Browser oder Selbstclient. Geben Sie als Nächstes Werte für den Namen der Anwendung, die URL Ihrer Webseite und eine autorisierte Umleitungs-URI an, die [!DNL Zoho CRM] können Sie dann mit einem Zuschuss-Token umleiten.

Bei erfolgreicher Registrierung werden Ihre Kunden-ID und das Kundengeheimnis zurückgegeben.

### Autorisierungsanforderung erstellen

Als Nächstes müssen Sie eine [Autorisierungsanforderung](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) entweder mit einer webbasierten Anwendung oder mit einem Self-Client. Die Autorisierungsanfrage gibt Ihr Zuschuss-Token zurück, mit dem Sie wiederum Ihr Zugriffstoken abrufen können.

Bei der Erstellung einer Autorisierungsanforderung müssen Sie Werte für beide eingeben **Bereiche** und **Zugriffstyp**. Siehe [[!DNL Zoho CRM] Dokument](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) für weitere Informationen zu Bereichen, während **Zugriffstyp** sollte immer auf `offline`.

### Zugriffstoken generieren und aktualisieren

Nachdem Sie Ihr ZuschussToken abgerufen haben, können Sie Ihr [Zugriffstoken und Aktualisierungstoken](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) , indem sie eine POST anfordern, `{ACCOUNTS_URL}/oauth/v2/token` , während Sie Ihre Client-ID, das Clientgeheimnis, das Grant-Token und die Umleitungs-URI angeben. In diesem Schritt müssen Sie `grant_type` als Parameter und legen Sie den Wert als `"authorization_code"`.

Bei einer erfolgreichen Anforderung werden die Zugriffstoken und Aktualisierungstoken zurückgegeben, mit denen Sie sich dann authentifizieren können.

Detaillierte Anweisungen zum Erwerb Ihrer Anmeldedaten finden Sie im [[!DNL Zoho CRM] Authentifizierungsleitfaden](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Verbinden [!DNL Zoho CRM] nach [!DNL Platform] mit APIs

In der folgenden Dokumentation finden Sie Informationen zur Verbindungsherstellung [!DNL Zoho CRM] zur Plattform mit APIs oder der Benutzeroberfläche:

- [Erstellen Sie eine [!DNL Zoho CRM] Basisverbindung mit der Flow Service API](../../tutorials/api/create/crm/zoho.md)
- [Erforschen Sie die Datenstruktur und Inhalte einer CRM-Quelle mithilfe der Flow Service API.](../../tutorials/api/explore/crm.md)
- [Erstellen eines Datenflusses für eine CRM-Quelle mithilfe der Flow Service API](../../tutorials/api/collect/crm.md)

## Verbinden [!DNL Zoho CRM] nach [!DNL Platform] über die Benutzeroberfläche

- [Erstellen Sie eine [!DNL Zoho CRM] Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/crm/zoho.md)
- [Erstellen eines Datenflusses für eine CRM-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/crm.md)
