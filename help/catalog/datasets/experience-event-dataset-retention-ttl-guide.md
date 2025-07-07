---
title: Verwalten der Aufbewahrung von Erlebnisereignis-Datensätzen im Data Lake mithilfe von TTL
description: Erfahren Sie, wie Sie die Aufbewahrung von Erlebnisereignis-Datensätzen im Data Lake mithilfe von TTL-Konfigurationen (Time-to-Live) mit Adobe Experience Platform-APIs bewerten, festlegen und verwalten können. In diesem Handbuch wird erläutert, wie die TTL-Gültigkeit auf Zeilenebene die Richtlinien zur Datenaufbewahrung unterstützt, die Speichereffizienz optimiert und ein effektives Daten-Lifecycle-Management sicherstellt. Darüber hinaus bietet sie Anwendungsfälle und Best Practices, die Sie bei der effektiven Anwendung von TTL unterstützen.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: 65a132609bc30233ac9f7efbe1981d4f75f3acb9
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 1%

---

# Verwalten der Aufbewahrung von Erlebnisereignis-Datensätzen im Data Lake mithilfe von TTL

Effizientes Daten-Management ist für optimale Leistung, Kostenkontrolle und Datenintegrität von entscheidender Bedeutung. Verwenden Sie die TTL (Time-to-Live) zur Aufbewahrung von Erlebnisereignissen-Datensätzen, um eine Gültigkeit auf Zeilenebene durchzusetzen. Dabei werden veraltete Datensätze automatisch aus Datensätzen im Data Lake entfernt, während gleichzeitig eine optimale Speichereffizienz und Datenrelevanz sichergestellt wird.

In diesem Handbuch wird erläutert, wie Sie TTL mithilfe der Catalog Service-API auswerten, festlegen und verwalten können. Sie erfahren, wann und warum die TTL angewendet wird, wie TTL-Werte mithilfe von API-Aufrufen konfiguriert und aktualisiert werden und welche Best Practices die effektive Implementierung gewährleisten.

>[!IMPORTANT]
>
>TTL wurde entwickelt, um das Data Lifecycle Management und die Speichereffizienz zu optimieren. Es ist kein Compliance-Tool und sollte nicht für regulatorische Anforderungen herangezogen werden. Compliance erfordert häufig umfassendere Data-Governance-Strategien.

## Gründe für die Verwendung von TTL zur Datenverwaltung auf Zeilenebene

Mit dem Wachstum von Datensätzen wird ein effizientes Daten-Management immer wichtiger, um die Leistung zu erhalten, Kosten zu kontrollieren und Daten relevant zu halten. Der Ablauf von TTL-basierten Daten auf Zeilenebene automatisiert die Datenbereinigung, indem veraltete Datensätze ohne manuelles Eingreifen entfernt werden, um die Speicherung zu optimieren und die Systemeffizienz zu verbessern.

TTL ist nützlich bei der Verwaltung zeitkritischer Daten, die im Laufe der Zeit an Relevanz verlieren. Erwägen Sie die Implementierung von TTL, wenn Sie Folgendes benötigen:

- Reduzierung der Speicherkosten durch automatische Entfernung veralteter Datensätze.
- Verbessern Sie die Abfrageleistung, indem Sie irrelevante Daten minimieren.
- Pflegen Sie die Datenhygiene, indem Sie nur relevante Informationen aufbewahren.
- Optimieren Sie die Datenaufbewahrung zur Unterstützung von Geschäftszielen.

>[!NOTE]
>
>Die Aufbewahrung von Erlebnisereignis-Datensätzen gilt für Ereignisdaten, die im Data Lake gespeichert sind. Wenn Sie die Datenspeicherung in Real-Time Customer Data Platform verwalten, sollten Sie [Ablauf von Erlebnisereignissen](../../profile/event-expirations.md) und [Ablauf pseudonymer Profile](../../profile/pseudonymous-profiles.md) zusammen mit den Einstellungen für die Datenspeicherung im Data Lake verwenden.

Verwenden Sie TTL-Konfigurationen, um die Speicherung basierend auf Berechtigungen zu optimieren. Während Profilspeicherdaten (die in Real-Time CDP verwendet werden) als veraltet betrachtet und nach 30 Tagen entfernt werden können, können dieselben Ereignisdaten im Data Lake für 12-13 Monate (oder länger basierend auf der Berechtigung) für Anwendungsfälle von Analytics und Data Distiller verfügbar bleiben.

>[!TIP]
>
>Berechtigungen beziehen sich auf die Speicher- und Aufbewahrungszertifikate, die in Ihren Adobe-Abonnement- und -Lizenzvereinbarungen definiert sind.

### Branchenbeispiel {#industry-example}

Nehmen wir als Beispiel einen Video-Streaming-Service, der Benutzerinteraktionen wie Videoansichten, Suchen und Empfehlungen verfolgt. Obwohl aktuelle Interaktionsdaten für die Personalisierung von entscheidender Bedeutung sind, verlieren ältere Aktivitätsprotokolle (z. B. Interaktionen von vor mehr als einem Jahr) an Relevanz. Durch die Verwendung der Gültigkeit auf Zeilenebene entfernt Experience Platform automatisch veraltete Protokolle, sodass nur aktuelle und aussagekräftige Daten für Analysen und Empfehlungen verwendet werden.

## TTL-Eignung bewerten {#evaluate-ttl-suitability}

Bevor Sie eine Aufbewahrungsrichtlinie anwenden, prüfen Sie, ob Ihr Datensatz ein guter Kandidat für die Gültigkeit auf Zeilenebene ist. Beachten Sie Folgendes:

- Datenrelevanz im Zeitverlauf: Bieten ältere Daten einen Wert oder sind sie veraltet?
- Auswirkungen auf nachgelagerte Prozesse: Wirkt sich das Entfernen von Daten auf die Berichterstellung, Analysen oder Integrationen aus?
- Speicherkosten im Vergleich zum Aufbewahrungswert: Rechtfertigt der Wert älterer Daten die Speicherkosten?

Wenn historische Aufzeichnungen für langfristige Analysen oder Geschäftsvorgänge unerlässlich sind, ist TTL möglicherweise nicht der richtige Ansatz. Durch die Überprüfung dieser Faktoren wird sichergestellt, dass die TTL mit Ihren Datenaufbewahrungsanforderungen übereinstimmt, ohne die Datenverfügbarkeit zu beeinträchtigen.

## Best Practices für das Festlegen von TTL {#best-practices}

Wählen Sie den richtigen TTL-Wert aus, um sicherzustellen, dass Ihre Richtlinie zur Aufbewahrung von Erlebnisereignis-Datensätzen ein ausgewogenes Verhältnis zwischen Datenaufbewahrung, Speichereffizienz und Analyseanforderungen aufweist. Eine zu kurze TTL kann zu Datenverlust führen, während eine zu lange TTL die Speicherkosten und die unnötige Datenakkumulation erhöhen kann. Stellen Sie sicher, dass die TTL mit dem Zweck Ihres Datensatzes übereinstimmt, indem Sie berücksichtigen, wie oft auf die Daten zugegriffen wird und wie lange sie relevant bleiben.

Die folgende Tabelle enthält allgemeine TTL-Empfehlungen, die auf dem Datensatztyp und den Nutzungsmustern basieren:

| Datensatztyp | Empfohlene TTL | Typische Anwendungsfälle |
|-----------------------------|------------------------|-------------------|
| Häufig aufgerufene Datensätze | 30-90 Tage | Benutzerinteraktionslogs, Website-Clickstream-Daten, kurzfristige Kampagnenleistungsdaten. |
| Archivieren von Datensätzen | 1 Jahr oder mehr | Protokolle zu Finanztransaktionen, Compliance-Daten, langfristige Trendanalysen, Datensätze zu maschinellen Lernprogrammen. |
| Vom Programm verwaltete Datensätze | Bis zu 13 Monate | Systemverwaltete Datensätze verfügen über vordefinierte TTL-Einschränkungen, die automatisch erzwungen werden, um die vom System auferlegten Beschränkungen einzuhalten. |
| Vom Kunden verwaltete Datensätze | 30 Tage - Max. TTL | Über die Benutzeroberfläche, APIs oder Data Distiller erstellte Datensätze. Die TTL muss mindestens 30 Tage betragen und innerhalb der definierten maximalen TTL liegen. |

Überprüfen Sie die TTL-Einstellungen regelmäßig, um sicherzustellen, dass sie weiterhin Ihren Speicherrichtlinien, Analyseanforderungen und Geschäftsanforderungen entsprechen.

### Wichtige Aspekte beim Festlegen von TTL {#key-considerations}

Befolgen Sie die folgenden Best Practices, um sicherzustellen, dass die TTL-Einstellungen mit Ihrer Datenaufbewahrungsstrategie übereinstimmen:

- TTL-Änderungen regelmäßig überprüfen. Jeder TTL-Update-Trigger erhält ein Audit-Ereignis. Verwenden Sie Auditprotokolle, um TTL-Änderungen für Compliance-, Data Governance- und Fehlerbehebungszwecke zu verfolgen.
- Deaktivieren Sie TTL, wenn Daten unbegrenzt aufbewahrt werden müssen. Um TTL zu deaktivieren, setzen Sie `ttlValue` auf `null`. Dadurch wird ein automatischer Ablauf verhindert und alle Datensätze werden dauerhaft beibehalten. Berücksichtigen Sie die Auswirkungen auf den Speicher, bevor Sie diese Änderung vornehmen.

## Einschränkungen der TTL {#limitations}

Beachten Sie die folgenden Einschränkungen bei der Verwendung von TTL:

- **Die Aufbewahrung von Erlebnisereignis-Datensätzen mithilfe der TTL gilt für die Gültigkeit auf**, nicht für das Löschen von Datensätzen. TTL entfernt Datensätze basierend auf einer definierten Aufbewahrungsfrist, löscht jedoch nicht ganze Datensätze. Um einen Datensatz zu entfernen, verwenden Sie den [Endpunkt für die Datensatzgültigkeit](../../hygiene/api/dataset-expiration.md) oder das manuelle Löschen.
- **TTL-Konfiguration bleibt aktiv, bis sie explizit deaktiviert**. Die Konfiguration bleibt aktiv, bis Sie sie deaktivieren. Durch Deaktivieren der TTL wird die Gültigkeit gestoppt und sichergestellt, dass alle Datensätze im Datensatz beibehalten werden.
- **TTL ist kein Compliance-Tool**. Während TTL die Speicherung und das Lifecycle Management optimiert, müssen Sie umfassendere Governance-Strategien implementieren, um die Einhaltung behördlicher Auflagen sicherzustellen.

## Analysieren der Datensatzgröße und -relevanz vor der Anwendung der TTL {#analyze-dataset-size}

Bevor Sie die TTL anwenden, verwenden Sie Abfragen, um die Größe und Relevanz des Datensatzes zu analysieren. Führen Sie zielgerichtete Abfragen aus (z. B. Zählen von Datensätzen innerhalb bestimmter Datumsbereiche), um eine Vorschau der Auswirkungen verschiedener TTL-Werte anzuzeigen. Verwenden Sie diese Informationen, um eine optimale Aufbewahrungsfrist auszuwählen, die den Nutzen der Daten und die Kosteneffizienz in Einklang bringt.

![Ein visueller Workflow zur Implementierung von TTL in Erlebnisereignis-Datensätzen. Zu den Schritten gehören die Bewertung der Datenlebensdauer und der Auswirkungen des Entfernens, die Validierung der TTL-Einstellungen mit Abfragen, die Konfiguration der TTL über die Catalog Service API und die kontinuierliche Überwachung der TTL-Auswirkungen sowie Anpassungen.](../images/datasets/dataset-retention-ttl-guide/manage-experience-event-dataset-retention-in-the-data-lake.png)

Das Ausführen gezielter Abfragen hilft dabei, zu bestimmen, wie viele Daten unter verschiedenen TTL-Konfigurationen aufbewahrt oder entfernt werden würden. Beispielsweise zählt die folgende SQL-Abfrage die Anzahl der Datensätze, die in den letzten 30 Tagen erstellt wurden:

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

Das Ausführen ähnlicher Abfragen für verschiedene Zeitintervalle hilft bei der Validierung der TTL-Einstellungen und stellt sicher, dass sie die Speichereffizienz und den Datenzugriff aufeinander abstimmen.

## Erste Schritte mit der TTL-Verwaltung

Bevor Sie die Aufbewahrung von Erlebnisereignis-Datensätzen mit der Catalog Service API bewerten, festlegen und verwalten können, müssen Sie wissen, wie Sie Ihre Anfragen korrekt formatieren. Dazu gehören die Kenntnis der API-Pfade, die Bereitstellung erforderlicher Kopfzeilen und die Formatierung von Anfrage-Payloads. Weitere Informationen finden Sie [ „Erste Schritte mit der Catalog Service](../api/getting-started.md)API“.

>[!NOTE]
>
>Dieses Dokument behandelt die Gültigkeit auf Zeilenebene, bei der einzelne abgelaufene Zeilen innerhalb eines Datensatzes gelöscht werden, während der Datensatz selbst intakt bleibt. Dies gilt nicht für die Datensatzgültigkeit, bei der ganze Datensätze entfernt und von einer separaten Funktion verwaltet werden. Informationen zur Gültigkeit auf Datensatzebene finden Sie in der [API-Dokumentation zur Datensatzgültigkeit](../../hygiene/api/dataset-expiration.md).

### Überprüfen der TTL-Einschränkungen {#check-ttl-constraints}

Verwenden Sie den Data Hygiene API `/ttl/{DATASET_ID}`-Endpunkt, um TTL-Konfigurationen zu planen. Dieser Endpunkt gibt die minimalen und maximalen TTL-Werte zurück, die für Ihre Organisation unterstützt werden, zusammen mit einem empfohlenen Wert (`defaultValue`) für den Datensatztyp.

Weitere Informationen finden Sie in der [ zur Adobe Developer ](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/#operation/getTtl)Datenhygiene-API).

Um [ derzeit auf einen Datensatz angewendete TTL zu überprüfen](#check-applied-ttl-values) stellen Sie stattdessen eine GET-Anfrage an [ Endpunkt ](https://developer.adobe.com/experience-platform-apis/references/catalog/)Catalog Service `/dataSets/{DATASET_ID}`).

>[!TIP]
>
>Die Experience Platform-Gateway-URL und der Basispfad für die Catalog Service-API sind: `https://platform.adobe.io/data/foundation/catalog`. Der Basispfad für die Data Hygiene API lautet: `https://platform.adobe.io/data/core/hygiene`

**API-Format**

```http
GET /ttl/{DATASET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Eine vom System generierte Zeichenfolge, die einen Datensatz eindeutig identifiziert. Verwenden Sie den `/datasets`-Endpunkt, um eine Datensatz-ID zu finden. Anweisungen [ Filtern von Antworten für relevante Datensätze finden Sie ](../api/list-objects.md) Handbuch zur List Catalog Objects API . |

**Anfrage**

Die folgende Anfrage ruft die TTL-Einschränkungen Ihres Unternehmens für einen bestimmten Datensatz ab.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die empfohlenen, maximalen und minimalen TTL-Werte basierend auf den Berechtigungen Ihres Unternehmens sowie eine vorgeschlagene TTL (`defaultValue`) für den Datensatz zurückgegeben. Diese `defaultValue` ist eine empfohlene TTL-Dauer und dient nur als Anleitung. Sie wird nur angewendet, wenn sie ausdrücklich von Ihnen konfiguriert wurde. Die Antwort enthält keine benutzerdefinierten TTL-Werte, die bereits festgelegt sein könnten. Verwenden Sie den GET-`/catalog/dataSets/{DATASET_ID}`-Endpunkt, um die aktuelle TTL für einen Datensatz anzuzeigen.

+++Auswählen, um die Antwort anzuzeigen

```json
{
  "extensions": {
    "adobe_lakeHouse": {
      "rowExpiration": {
        "defaultValue": "P12M",
        "maxValue": "P12M",
        "minValue": "P7D"
      }
    }
  }
}
```

+++

| Eigenschaft | Beschreibung |
|--------------|-------------|
| `defaultValue` | Ein empfohlener TTL-Wert für Ihren Datensatz. Dieser Wert wird **nicht** automatisch angewendet. Sie müssen explizit eine TTL festlegen, damit sie wirksam wird. |
| `maxValue` | Die maximale TTL-Dauer, die gemäß der Berechtigung Ihrer Organisation zulässig ist. In der Regel beträgt diese Dauer 10 Jahre (`P10Y`). |
| `minValue` | Die minimale TTL-Dauer, die gemäß der Berechtigung Ihrer Organisation zulässig ist. Normalerweise beträgt diese Dauer 30 Tage (`P30D`). |

### Überprüfen der angewendeten TTL-Werte {#check-applied-ttl-values}

Verwenden Sie den folgenden API-Aufruf, um den aktuellen TTL-Wert zu überprüfen, der auf einen Datensatz angewendet wurde:

```http
GET /dataSets/{DATASET_ID}
```

Dieser Aufruf gibt die aktuelle `ttlValue` (falls festgelegt) im `extensions.adobe_lakeHouse.rowExpiration` zurück.

**Anfrage**

Die folgende Anfrage ruft den TTL-Wert Ihrer Organisation für einen bestimmten Datensatz ab.

```shell
curl -X GET \
https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält das `extensions`-Objekt, das die aktuelle TTL-Konfiguration enthält, die auf den Datensatz angewendet wurde. Das folgende Antwortbeispiel wird zur Vereinfachung gekürzt.

```json
{
    "{DATASET_ID}": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M",
            }
            }
        }
        ...
    }
}
```

### Festlegen oder Aktualisieren der TTL für einen Datensatz {#set-update-ttl}

>[!IMPORTANT]
>
>Eine TTL-basierte Gültigkeit auf Zeilenebene kann nur auf Ereignis-Datensätze angewendet werden, die ein Zeitreihenschema verwenden. Dazu gehören Datensätze, die auf der standardmäßigen XDM ExperienceEvent-Klasse basieren, sowie benutzerdefinierte Schemata, die das Zeitreihenschema (`https://ns.adobe.com/xdm/data/time-series`) erweitern.
>
>Bevor Sie die TTL anwenden, verwenden Sie die Schema Registry-API, um zu überprüfen, ob das Schema des Datensatzes die richtige Erweiterung enthält, indem Sie die `meta:extends` Eigenschaft überprüfen. Eine Anleitung dazu finden [ in der ](../../xdm/api/schemas.md#lookup) zum Schema-Endpunkt .

Sie können die Aufbewahrung von Erlebnisereignis-Datensätzen konfigurieren, indem Sie eine neue TTL festlegen oder eine vorhandene TTL aktualisieren, indem Sie dieselbe API-Methode verwenden. Verwenden Sie eine PATCH-Anfrage an den `/v2/datasets/{DATASET_ID}`-Endpunkt, um die TTL anzuwenden oder anzupassen.

**API-Format**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Die ID des Datensatzes, für den Sie den TTL-Wert aktualisieren möchten. |

**Anfrage**

Im folgenden Beispiel ist der `ttlValue` auf `P3M` festgelegt. Das bedeutet, dass Datensätze, die älter als drei Monate sind, automatisch gelöscht werden. Passen Sie die Aufbewahrungsfrist an Ihre Geschäftsanforderungen an (z. B. sechs Monate `P6M` oder ein Jahr `P12M`).

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M"  // A 3 month retention period
            }
        }
    }
}
```

| Eigenschaft | Beschreibung |
|----------------------------------|-------------|
| `rowExpiration.ttlValue` | Definiert die Dauer, bevor Datensätze im Datensatz automatisch entfernt werden. Verwendet das ISO-8601-Periodenformat (z. B. `P3M` für 3 Monate oder `P30D` für 30 Tage). |

**Antwort**

Eine erfolgreiche Antwort gibt einen Verweis auf den aktualisierten Datensatz zurück, enthält jedoch nicht explizit die TTL-Einstellungen. Um die TTL-Konfiguration zu bestätigen, stellen Sie eine Folgeanfrage `GET /dataSets/{DATASET_ID}`.

```JSON
[
  "@/dataSets/{DATASET_ID}"
]
```

#### Beispielszenario {#example-scenario}

Stellen Sie sich eine Video-Streaming-Plattform vor, die die TTL zunächst auf drei Monate festlegt, um neue Interaktionsdaten für die Personalisierung sicherzustellen. Wenn eine nachfolgende Analyse jedoch ergibt, dass ältere Interaktionen weiterhin wertvolle Erkenntnisse liefern, kann die TTL mit der folgenden Anfrage auf sechs Monate verlängert werden:

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P6M"  // Extend to 6 months
            }
        }
    }
}
```

## Häufig gestellte Fragen zur Richtlinie zur Datensatzaufbewahrung {#faqs}

Diese häufig gestellten Fragen befassen sich mit praktischen Fragen zu Aufträgen für die Datensatzaufbewahrung, den unmittelbaren Auswirkungen von TTL-Änderungen, Wiederherstellungsoptionen und den Unterschieden zwischen den Aufbewahrungsfristen in den Platform-Services.

### Auf welche Arten von Datensätzen kann ich Regeln für Aufbewahrungsrichtlinien anwenden?

+++Antwort
Sie können TTL-basierte Aufbewahrungsrichtlinien auf jeden Datensatz anwenden, der Zeitreihenverhalten verwendet. Dazu gehören Datensätze, die auf der standardmäßigen XDM ExperienceEvent-Klasse basieren, sowie benutzerdefinierte Schemata, die zur Erfassung von Zeitreihendaten entwickelt wurden.

Für den Ablauf auf Zeilenebene sind die folgenden technischen Bedingungen erforderlich:

- Das Schema muss so konzipiert sein, dass es Zeitreihendaten erfasst.
- Das Schema muss ein Zeitstempelfeld enthalten, das zum Auswerten des Ablaufs verwendet wird.
- Der Datensatz sollte Daten auf Ereignisebene speichern, normalerweise unter Verwendung oder Erweiterung der XDM ExperienceEvent-Klasse.
- Der Datensatz muss im Katalog-Service registriert sein, da TTL-Einstellungen über `extensions.adobe_lakeHouse.rowExpiration` angewendet werden.
- TTL-Werte müssen das ISO-8601-Dauerformat verwenden (z. B. `P30D`, `P6M`, `P1Y`).
+++

### Wie bald löscht der Auftrag zur Datensatzaufbewahrung Daten aus Data Lake-Services?

+++Antwort
Datensatz-TTLs werden alle 30 Tage ausgewertet und verarbeitet und dabei werden alle abgelaufenen Datensätze gelöscht. Ein Ereignis wird als abgelaufen betrachtet, wenn es vor mehr als 30 Tagen (Aufnahmedatum > 30 Tage) in Experience Platform aufgenommen wurde und sein Ereignisdatum die definierte Aufbewahrungsfrist (TTL) überschreitet.
+++

<!-- ### How soon will the Dataset Retention job delete data from Profile services?

+++Answer
Once a retention policy is set, existing events that already exceed the newly defined TTL are immediately deleted. Newer events remain until their timestamps surpass the retention period.

For example, if you apply a 30-day expiration policy on May 15th, the following occurs:

- New events receive a 30-day expiration as they are ingested.
- Existing events with a timestamp older than April 15th are immediately deleted.
- Existing events with a timestamp after April 15th are set to expire 30 days after their timestamp (for example, an event from April 18th would be deleted on May 18th).
+++ -->

### Kann ich unterschiedliche Aufbewahrungsrichtlinien für Data Lake- und Profil-Services festlegen?

+++Antwort
Ja, Sie können unterschiedliche Aufbewahrungsrichtlinien für Data Lake- und Profil-Services festlegen. Je nach Bedarf Ihres Unternehmens kann die Aufbewahrungsfrist für den Profilspeicher kürzer oder länger als die Data-Lake-Aufbewahrungsfrist sein.
+++

### Wie kann ich meine aktuelle Datensatznutzung überprüfen?

+++Antwort
Sie können die neueste Datensatzspeichergröße für Data Lake- und Profilspeicher als separate Metriken im Inventar-Arbeitsbereich [!UICONTROL Datensatz] überprüfen. Sortieren Sie die Spalten, um die größten Datensätze zu identifizieren, und überprüfen Sie, ob Aufbewahrungsrichtlinien angewendet werden.

Weitere Informationen zur Verwendung auf Sandbox-Ebene finden Sie unter Lizenznutzungs-Dashboard . Weitere Informationen finden [ unter &quot;](../../dashboards/guides/license-usage.md)&quot;.
+++

### Wie kann ich überprüfen, ob der Datenaufbewahrungsauftrag erfolgreich war?

+++Antwort
Sie können den letzten Datenaufbewahrungsauftrag überprüfen, indem Sie dessen Zeitstempel in der [Benutzeroberfläche für die Datensatzaufbewahrungskonfiguration](./user-guide.md#data-retention-policy) oder auf der Seite „Dateninventar“ überprüfen.

Alternativ können Sie eine GET-Anfrage an den folgenden Endpunkt senden:

`GET https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID}`

Die Antwort enthält die `extensions.adobe_lakeHouse.rowExpiration.lastCompleted`, die den Unix-Zeitstempel (in Millisekunden) angibt, wann der letzte TTL-Auftrag abgeschlossen wurde.

Berichte zur historischen Datensatznutzung sind derzeit nicht verfügbar.
+++

### Kann ich gelöschte Daten wiederherstellen?

+++Antwort
Nein, nach Anwendung einer Aufbewahrungsrichtlinie werden alle Daten, die älter als die Aufbewahrungsfrist sind, dauerhaft gelöscht und können nicht wiederhergestellt werden.
+++

### Was ist das Minimum an TTL, das ich für einen Data-Lake-Erlebnisereignis-Datensatz konfigurieren kann?

+++Antwort
Die TTL für einen Data-Lake-Erlebnisereignis-Datensatz beträgt mindestens 30 Tage. Der Data Lake dient während der ersten Aufnahme und Verarbeitung als Verarbeitungs-Backup- und Wiederherstellungssystem. Daher müssen Daten mindestens 30 Tage nach der Aufnahme im Data Lake verbleiben, bevor sie abgelaufen sein können.
+++

### Was passiert, wenn ich einige Data-Lake-Felder länger aufbewahren muss, als meine TTL-Richtlinie es zulässt?

+++Antwort
Verwenden Sie Data Distiller, um bestimmte Felder über die TTL Ihres Datensatzes hinaus beizubehalten und gleichzeitig Ihre Nutzungsbeschränkungen zu einzuhalten. Erstellen Sie einen Auftrag, der regelmäßig nur die erforderlichen Felder in einen abgeleiteten Datensatz schreibt. Dieser Workflow gewährleistet die Einhaltung einer kürzeren TTL bei gleichzeitiger Beibehaltung kritischer Daten für die erweiterte Verwendung.

Weitere Informationen finden Sie im Handbuch [Erstellen abgeleiteter Datensätze mit SQL](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md).
+++

## Nächste Schritte {#next-steps}

Nachdem Sie nun gelernt haben, wie Sie TTL-Einstellungen für den Ablauf auf Zeilenebene verwalten, lesen Sie die folgende Dokumentation, um Ihr Verständnis der TTL-Verwaltung zu vertiefen:

- Aufbewahrungsaufträge: Erfahren Sie mit dem [Handbuch zur Datenlebenszyklus-Benutzeroberfläche“, wie Sie Datensatzgültigkeiten in der Experience Platform-Benutzeroberfläche planen und automatisieren ](../../hygiene/ui/dataset-expiration.md), oder überprüfen Sie die Konfigurationen zur Datensatzaufbewahrung und stellen Sie sicher, dass abgelaufene Datensätze gelöscht werden.
- [API-Endpunkthandbuch zur Datensatzgültigkeit](../../hygiene/api/dataset-expiration.md): Erfahren Sie, wie Sie ganze Datensätze und nicht nur Zeilen löschen können. Erfahren Sie, wie Sie die Datensatzgültigkeit mithilfe der API planen, verwalten und automatisieren können, um eine effiziente Datenaufbewahrung zu gewährleisten.
- [Datennutzungsrichtlinien - Übersicht](../../data-governance/policies/overview.md) Erfahren Sie, wie Sie Ihre Datenaufbewahrungsstrategie an umfassenderen Compliance-Anforderungen und Marketing-Nutzungsbeschränkungen ausrichten können.
