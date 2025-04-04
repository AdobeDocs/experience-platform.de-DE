---
keywords: Experience Platform; Abfrage-Service; IP-Zugriffskontrolle; Autorisierung; API; Erste Schritte
title: Data Distiller Authorization API-Handbuch
description: Erfahren Sie, wie Sie mit Autorisierungs- und IP-Bereichsbeschränkungen für einen sicheren Datenzugriff im Abfrage-Service von Adobe Experience Platform beginnen.
role: Developer
exl-id: d93ce774-c8b2-4f15-a4d9-117d9aa5d9e7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 5%

---

# Erste Schritte mit der Data Distiller-Autorisierungs-API

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Add-on Data Distiller erworben haben. Weitere Informationen erhalten Sie beim Adobe-Support.

Die Data Distiller-Autorisierungs-API bietet Unternehmen über die SQL-Schnittstelle in Adobe Experience Platform eine engere Kontrolle über den Datenzugriff. Mit dieser API können Sie IP-Einschränkungen definieren, den Datenzugriff auf bestimmte Netzwerke beschränken und die Sicherheitsüberwachung verbessern.

In diesem Handbuch wird beschrieben, wie Sie die Autorisierungsberechtigungen einrichten, die für Aufrufe an die Data Distiller-Autorisierungs-API erforderlich sind.

## Erste Schritte {#getting-started}

Die folgenden Abschnitte enthalten Informationen zur Vorbereitung der erforderlichen Autorisierungswerte und zur Durchführung Ihrer ersten Anfragen an die Data Distiller-Autorisierungs-API.

### Erforderliche Berechtigungen {#required-permissions}

Um sichere Datenzugriffsbeschränkungen in Query Service zu aktivieren, benötigen Sie die Berechtigung **[!UICONTROL Zulassungsliste verwalten]**. Mit dieser Berechtigung können Unternehmen bestimmte IP-Bereiche (im IPv4- oder IPv6-Format) definieren, die für den Zugriff auf Daten in Experience Platform über die SQL-Schnittstelle autorisiert sind. Der Zugriff wird auf Sandbox-Ebene verwaltet, wo Benutzer eine Liste genehmigter IP-Adressen oder CIDR-Blöcke konfigurieren können, die den Zugriff nur auf zulässige Netzwerke beschränken.

>[!NOTE]
>
>Systemadministratoren können Benutzerberechtigungen über die Adobe [Admin Console](https://adminconsole.adobe.com/) einrichten. Weitere Informationen finden Sie im [Benutzerhandbuch für die Admin Console](https://helpx.adobe.com/de/enterprise/using/admin-console.html).

Die folgenden Funktionen sind mit der Berechtigung **[!UICONTROL Zulassungsliste verwalten]** verfügbar:

- **Zugelassene IP-Bereiche definieren**: Nur IP-Adressen oder CIDR-Blöcke aus diesen definierten Bereichen können über den Abfrage-Service mit SQL auf Daten in Experience Platform zugreifen.
- **IP-Bereichsprüfungen erzwingen**: Verbindungen von IPs außerhalb der zulässigen Bereiche werden verweigert.
- **Audit- und Warnfunktionen**: Alle Zugriffsversuche, einschließlich verweigerter Verbindungen, werden als Prüfereignisse protokolliert. Diese Ereignisse sind in den [Adobe Experience Platform-Auditprotokollen](../../landing/governance-privacy-security/audit-logs/overview.md) verfügbar, sodass potenzielle Sicherheitsverletzungen überwacht werden können.

### Sammeln von Werten für erforderliche Kopfzeilen {#gather-values-for-required-headers}

Um die Data Distiller-Autorisierungs-API aufzurufen, müssen Sie das [Tutorial zur Experience Platform-API-Authentifizierung](../../landing/api-authentication.md) abschließen, in dem Werte für erforderliche Kopfzeilen in API-Aufrufen bereitgestellt werden. Nehmen Sie in jede Anfrage die folgenden Kopfzeilen auf:

- **Autorisierung**: `Bearer {ACCESS_TOKEN}`
- **x-api-key**: `{API_KEY}`
- **x-gw-ims-org-id**: `{ORG_ID}`
- **x-sandbox-name**: `{SANDBOX_NAME}`

>[!NOTE]
>
> Weitere Informationen zu Sandboxes finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Alle Anfragen, die eine Payload enthalten (POST, PUT, PATCH), erfordern ebenfalls diese Kopfzeile:

- **Content-Type**: `application/json`

### Nächste Schritte

Wenn Sie die erforderlichen Berechtigungen und Kopfzeilenwerte erfasst haben, können Sie mit der Konfiguration von IP-Einschränkungen für den Abfrage-Service beginnen. Fahren Sie mit der Endpunktdokumentation fort, um ausführliche Beispiele für CRUD-Vorgänge zu erhalten, darunter:

- API-Format und Beispielpaare für Anfragen/Antworten.
- Kopfzeilen, Payloads und Antwort-Codes für jeden Vorgang.

Jedes Beispiel für einen API-Aufruf zeigt, wie Anfragen formatiert und Antworten interpretiert werden, sodass Sie im Abfrage-Service einen sicheren Zugriff auf Ihre Daten erzwingen können.

Spezifische Anweisungen zur Konfiguration und Validierung von IP-Einschränkungen finden Sie in der [Dokumentation zum IP-](./ip-access.md) und in der [Dokumentation zum IP-Validierungsendpunkt](./validate.md).

Siehe die [OpenAPI-Referenzdokumentation zur Data Distiller-Autorisierung](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/), um ein standardisiertes, maschinenlesbares Format für eine einfachere Integration, Tests und Untersuchung anzuzeigen.
