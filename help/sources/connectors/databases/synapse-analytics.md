---
title: Übersicht über den Azure Synapse Analytics Source Connector
description: Erfahren Sie, wie Sie Azure Synapse Analytics mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2025-06-17T00:00:00Z
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 8%

---

# [!DNL Azure Synapse Analytics]

>[!IMPORTANT]
>
>Die [!DNL Azure Synapse Analytics] ist im Quellkatalog für Benutzende verfügbar, die Real-Time Customer Data Platform Ultimate erworben haben.

[!DNL Azure Synapse Analytics] ist ein Cloud-basierter Analytics-Service, der Big Data und Data Warehousing vereinheitlicht. Sie können Daten mithilfe von SQL-, [!DNL Spark]- oder Echtzeit-Tools aufnehmen, untersuchen, vorbereiten und analysieren, ohne Ihre Daten zu verschieben.

Sie können die [!DNL Azure Synapse Analytics] verwenden, um Ihr Konto zu verbinden und Ihre Daten an Adobe Experience Platform zu übertragen.

## Voraussetzungen {#prerequisites}

Lesen Sie die folgenden Abschnitte, um die erforderliche Einrichtung abzuschließen, bevor Sie Ihr [!DNL Azure Synapse Analytics]-Konto mit Experience Platform verbinden.

### Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform](../../ip-address-allow-list.md) .

### Berechtigungen konfigurieren

Um Ihr Quellkonto mit Experience Platform zu verbinden, müssen für Ihr Konto die beiden folgenden Berechtigungen aktiviert sein:

* **Anzeigen von Quellen**
* **Verwalten von Quellen**

Wenn Sie nicht über diese Berechtigungen verfügen, wenden Sie sich an Ihren Produktadministrator, um den Zugriff anzufordern. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche der Zugriffssteuerung](../../../access-control/ui/overview.md).

### Bei Experience Platform authentifizieren

Sie können entweder die Kontoschlüsselauthentifizierung oder die Service-Prinzipal-Schlüsselauthentifizierung verwenden, um Ihre [!DNL Azure Synapse Analytics] mit Experience Platform zu verbinden.

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel]

Geben Sie Werte für die folgenden Anmeldeinformationen an, um Ihre [!DNL Azure Synapse Analytics] mithilfe der Kontoschlüsselauthentifizierung mit Experience Platform zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Verbindungszeichenfolge | Dies ist die **Verbindungszeichenfolge** die für die Authentifizierung bei [!DNL Azure Synapse Analytics] verwendet wird. Das Standardformat ist: `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. Sie müssen die Platzhalter durch Ihre tatsächlichen Verbindungsdetails ersetzen. |
| Verbindungsspezifikations-ID | Die **Verbindungsspezifikation** stellt die Connector-Eigenschaften einer Datenquelle bereit. Dazu gehören Details wie Authentifizierungsspezifikationen und Anforderungen für die Erstellung von **Basis**- und **Quelle**-Verbindungen. [!DNL Azure Synapse Analytics] lautet die Verbindungsspezifikations-ID: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. **Hinweis:** Diese Anmeldedaten sind nur bei der Verbindung über APIs erforderlich. |

>[!TAB Authentifizierung für Service-Prinzipal-Schlüssel]

Um Ihre Anmeldeinformationen für die Authentifizierung des Service-Prinzipalschlüssels abzurufen, navigieren Sie zur [[!DNL Microsfot Entra admin center]](https://entra.microsoft.com/#home) und rufen Werte für Folgendes ab:

* App-ID
* Anzeigename
* Geheimnis
* Mandanten-ID

Navigieren Sie dann zu Ihrer [[!DNL Azure Synapse Analytics] Instanz](https://azure.microsoft.com/en-ca/products/synapse-analytics) und wählen Sie die Option zum Erstellen eines Benutzers aus einem externen Anbieter aus. Geben Sie von hier aus die entsprechenden Berechtigungen für den Service-Prinzipal für das Schema an. **HINWEIS:**: Sie müssen „SELECT“ einbeziehen, da dies für die Schemavorschau erforderlich ist, ähnlich wie „COPY“. Ein Beispielbefehl kann beispielsweise wie folgt lauten:

```SQL
GRANT SELECT ON SCHEMA::dbo TO {APP_ID};
```

Geben Sie Werte für die folgenden Anmeldeinformationen an, um Ihre [!DNL Azure Synapse Analytics]-Datenbank mithilfe der Authentifizierung für Service-Prinzipal-Schlüssel mit Experience Platform zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Server | Der vollständig qualifizierte Domain-Name Ihres [!DNL Azure Synapse Analytics] SQL-Endpunkts. |
| Datenbank | Der Name der spezifischen Datenbank in Ihrem [!DNL Azure Synapse Analytics] Workspace. |
| Mandant | Die mit Ihrem [!DNL Azure]-Abonnement verknüpfte [!DNL Azure Active Directory]-Mandanten-ID. |
| Primär-ID des Diensts | Die Client-ID einer [!DNL Azure Active Directory]. |
| Primärschlüssel des Diensts | Das mit dem Service-Prinzipal verknüpfte Client-Geheimnis oder Kennwort. |
| Verbindungsspezifikations-ID | Die **Verbindungsspezifikation** stellt die Connector-Eigenschaften einer Datenquelle bereit. Dazu gehören Details wie Authentifizierungsspezifikationen und Anforderungen für die Erstellung von **Basis**- und **Quelle**-Verbindungen. [!DNL Azure Synapse Analytics] lautet die Verbindungsspezifikations-ID: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. **Hinweis:** Diese Anmeldedaten sind nur bei der Verbindung über APIs erforderlich. |

Weitere Informationen finden Sie in der [[!DNL Azure] Dokumentation zum Verwalten von Identitäten für [!DNL Azure Synapse Analytics]](https://learn.microsoft.com/en-us/azure/synapse-analytics/synapse-service-identity).

>[!ENDTABS]

## Verbinden von [!DNL Azure Synapse Analytics] mit Experience Platform mithilfe von APIs

* [Verbinden  [!DNL Azure Synapse Analytics]  Experience Platform mithilfe der Flow Service-API](../../tutorials/api/create/databases/synapse-analytics.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden von [!DNL Azure Synapse Analytics] mit Experience Platform über die Benutzeroberfläche

* [Verbinden  [!DNL Azure Synapse Analytics]  Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/databases/synapse-analytics.md)
* [Erstellen eines Datenflusses für eine Datenbank-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)

