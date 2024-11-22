---
keywords: Experience Platform; Query Service; IP-Zugriffskontrolle; Autorisierung; API; Erste Schritte
title: Data Distiller Authorization API-Anleitung
description: Erfahren Sie mehr über die ersten Schritte zur Autorisierung und IP-Bereichsbeschränkungen für sicheren Datenzugriff in Adobe Experience Platform Query Service.
role: Developer
exl-id: d93ce774-c8b2-4f15-a4d9-117d9aa5d9e7
source-git-commit: 804eeb4ec976cf41fdd450bd8f307499c3ebae03
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 5%

---

# Erste Schritte mit der Data Distiller Authorization API

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Data Distiller-Add-on erworben haben. Weitere Informationen erhalten Sie bei Ihrer bzw. Ihrem Adobe-Support-Mitarbeitenden.

Die Data Distiller Authorization-API bietet Unternehmen eine strengere Kontrolle über den Datenzugriff über die SQL-Schnittstelle in Adobe Experience Platform. Mit dieser API können Sie IP-Einschränkungen definieren, den Datenzugriff auf bestimmte Netzwerke einschränken und die Sicherheitsüberwachung verbessern.

In diesem Handbuch wird beschrieben, wie Sie die Autorisierungsberechtigungen und -berechtigungen einrichten, die für Aufrufe an die Data Distiller Authorization-API erforderlich sind.

## Erste Schritte {#getting-started}

In den folgenden Abschnitten finden Sie Informationen zum Vorbereiten der erforderlichen Autorisierungswerte und zum Ausführen Ihrer ersten Anfragen an die Data Distiller Authorization-API.

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

Um die Data Distiller Authorization-API aufzurufen, müssen Sie das Tutorial zur Authentifizierung mit der Platform-API](../../landing/api-authentication.md) abschließen, das Werte für erforderliche Kopfzeilen in API-Aufrufen bereitstellt. [ Schließen Sie die folgenden Header in jede Anfrage ein:

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

In der Referenzdokumentation für die Data Distiller Authorization OpenAPI](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) finden Sie ein standardisiertes, maschinenlesbares Format für einfachere Integration, Tests und Exploration.[
