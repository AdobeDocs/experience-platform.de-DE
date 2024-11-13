---
keywords: Experience Platform; Query Service; IP-Zugriffskontrolle; Autorisierung; API; Erste Schritte
title: Handbuch zur Autorisierungs-API für Query Service
description: Erfahren Sie mehr über die ersten Schritte zur Autorisierung und IP-Bereichsbeschränkungen für sicheren Datenzugriff in Adobe Experience Platform Query Service.
role: Developer
exl-id: d93ce774-c8b2-4f15-a4d9-117d9aa5d9e7
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 6%

---

# Handbuch zur Autorisierungs-API für Query Service

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Data Distiller-Add-on erworben haben. Weitere Informationen erhalten Sie bei Ihrer bzw. Ihrem Adobe-Support-Mitarbeitenden.

Die Autorisierungs-API von Query Service bietet Unternehmen eine strengere Kontrolle über den Datenzugriff über die SQL-Schnittstelle in Adobe Experience Platform. Mit dieser API können Sie IP-Einschränkungen definieren, den Datenzugriff auf bestimmte Netzwerke einschränken und die Sicherheitsüberwachung verbessern.

In diesem Handbuch wird beschrieben, wie Sie die Autorisierungsberechtigungen und -berechtigungen einrichten, die für Aufrufe an die Autorisierungs-API von Query Service erforderlich sind.

## Erste Schritte {#getting-started}

In den folgenden Abschnitten finden Sie Informationen zum Vorbereiten der erforderlichen Autorisierungswerte und zum Ausführen Ihrer ersten Anfragen an die Autorisierungs-API von Query Service.

### Erforderliche Berechtigungen {#required-permissions}

Um sichere Datenzugriffsbeschränkungen in Query Service zu aktivieren, benötigen Sie die Berechtigung **[!UICONTROL Zulassungsliste verwalten]** . Mit dieser Berechtigung können Unternehmen bestimmte IP-Bereiche definieren (im IPv4- oder IPv6-Format), die über die SQL-Schnittstelle für den Zugriff auf Daten in Platform berechtigt sind. Der Zugriff wird auf Sandbox-Ebene verwaltet, wo Benutzer eine Liste genehmigter IP-Adressen oder CIDR-Blöcke konfigurieren können, die den Zugriff nur auf zugelassene Netzwerke beschränken.

>[!NOTE]
>
>Systemadministratoren können über die Adobe [Admin Console](https://adminconsole.adobe.com/) Benutzerberechtigungen einrichten. Weitere Informationen finden Sie im [Benutzerhandbuch für die Admin Console](https://helpx.adobe.com/de/enterprise/using/admin-console.html).

Die folgenden Funktionen sind mit der Berechtigung **[!UICONTROL Zulassungsliste verwalten]** verfügbar:

- **Zulässige IP-Bereiche definieren**: Nur IP-Adressen oder CIDR-Blöcke aus diesen definierten Bereichen können über Query Service auf Daten in Platform zugreifen.
- **IP-Bereichsprüfungen erzwingen**: Verbindungen von IP-Adressen außerhalb der zulässigen Bereiche werden verweigert.
- **Audit- und Warnfunktionen**: Alle Zugriffsversuche, einschließlich verweigerter Verbindungen, werden als Prüfereignisse protokolliert. Diese Ereignisse sind in den [Adobe Experience Platform-Auditprotokollen](../../landing/governance-privacy-security/audit-logs/overview.md) verfügbar und ermöglichen die Überwachung potenzieller Sicherheitsverletzungen.

### Sammeln von Werten für erforderliche Kopfzeilen {#gather-values-for-required-headers}

Um die Autorisierungs-API von Query Service aufzurufen, müssen Sie das [Tutorial zur Platform-API-Authentifizierung](../../landing/api-authentication.md) abschließen, das Werte für erforderliche Kopfzeilen in API-Aufrufen bereitstellt. Schließen Sie die folgenden Header in jede Anfrage ein:

- **Autorisierung**: `Bearer {ACCESS_TOKEN}`
- **x-api-key**: `{API_KEY}`
- **x-gw-ims-org-id**: `{ORG_ID}`
- **x-sandbox-name**: `{SANDBOX_NAME}`

>[!NOTE]
>
> Weitere Informationen zu Sandboxes finden Sie in der [Sandbox - Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist ebenfalls diese Kopfzeile erforderlich:

- **Content-Type**: `application/json`

### Nächste Schritte

Nachdem Sie die erforderlichen Berechtigungen und Kopfzeilenwerte gesammelt haben, können Sie mit der Konfiguration von IP-Einschränkungen für Query Service beginnen. In der Endpunktdokumentation finden Sie ausführliche Beispiele für CRUD-Vorgänge, darunter:

- API-Format und Beispiel-Anfrage-/Antwortpaare.
- Kopfzeilen, Payloads und Antwort-Codes für jeden Vorgang.

Jedes API-Aufrufbeispiel veranschaulicht, wie Anforderungen formatiert und Antworten interpretiert werden, sodass Sie sicheren Zugriff auf Ihre Daten in Query Service erzwingen können.

Spezifische Anweisungen zum Konfigurieren und Validieren von IP-Einschränkungen finden Sie in der Dokumentation zum [IP-Zugriffendpunkt](./ip-access.md) und in der Dokumentation zum [IP-Validierungsendpunkt](./validate.md) .
