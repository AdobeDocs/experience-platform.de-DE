---
title: Übersicht über den Salesforce Service Cloud Source Connector
description: Erfahren Sie, wie Sie Salesforce Service Cloud mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 9bebbc00-55b3-4aec-9357-4127c05844e2
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 10%

---

# [!DNL Salesforce Service Cloud]

[!DNL Salesforce Service Cloud] ist eine Customer Success-Plattform, die zur Automatisierung von Service-Workflows und zur Optimierung der Kommunikation zwischen Unternehmen und ihren Kunden entwickelt wurde. Er fasst Anfragen aus verschiedenen Kanälen wie E-Mail, Telefon, Social Media und Live-Chat in einer zentralen Agentenkonsole zusammen. Auf diese Weise können Support-Teams „Fälle“ mit einer 360-Grad-Ansicht der Kundenhistorie verwalten und sicherstellen, dass die Antworten personalisiert und effizient sind, unabhängig davon, wie der Kunde sich meldet.

Sie können den [!DNL Salesforce Service Cloud]-Quell-Connector in Adobe Experience Platform Sources verwenden, um Ihr [!DNL Salesforce Service Cloud]-Konto zu verbinden und Ihre Daten zur Verwendung in Experience Platform Services bereitzustellen.

Lesen Sie dieses Dokument, um zu erfahren, wie Sie Ihr [!DNL Salesforce Service Cloud]-Konto einrichten und mit Experience Platform verbinden können.

## Voraussetzungen {#prerequisites}

Lesen Sie diesen Abschnitt, um die erforderliche Einrichtung zu erfahren, die Sie durchführen müssen, bevor Sie eine erfolgreiche Verbindung zu Experience Platform herstellen können.

### Zulassungsliste von IP-Adressen {#allowlist}

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform](../../ip-address-allow-list.md) .

### Sammeln erforderlicher Anmeldedaten {#credentials}

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihr [!DNL Salesforce Service Cloud]-Konto mit OAuth2-Client-Anmeldeinformationen zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Umgebungs-URL | Die URL der [!DNL Salesforce Service Cloud] Quellinstanz. |
| Client-ID | Die Client-ID wird im Rahmen der OAuth2-Authentifizierung zusammen mit dem Client-Geheimnis verwendet. Zusammen ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre Anwendung für die [!DNL Salesforce Service Cloud] identifizieren. |
| Client-Geheimnis | Das Client-Geheimnis wird zusammen mit der Client-ID als Teil der OAuth2-Authentifizierung verwendet. Zusammen ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre Anwendung für die [!DNL Salesforce Service Cloud] identifizieren. |
| API-Version | Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce Service Cloud]. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version `52` verwenden, müssen Sie den Wert als `52.0` eingeben. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |

Weitere Informationen zur Verwendung von OAuth für [!DNL Salesforce Service Cloud] finden Sie im [[!DNL Salesforce Service Cloud] Handbuch zu OAuth-Autorisierungsflüssen](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

## Verbinden von [!DNL Salesforce Service Cloud]mit Experience Platform mithilfe von APIs

- [Erstellen einer Salesforce Service Cloud-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/customer-success/salesforce-service-cloud.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine Customer Success-Quelle mithilfe der Flow Service-API](../../tutorials/api/collect/customer-success.md)

## Verbinden von [!DNL Salesforce Service Cloud] mit Experience Platform über die Benutzeroberfläche

- [Erstellen einer Salesforce Service Cloud-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/customer-success/salesforce-service-cloud.md)
- [Erstellen eines Datenflusses für eine Customer Success-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/customer-success.md)
