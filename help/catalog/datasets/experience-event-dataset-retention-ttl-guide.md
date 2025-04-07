---
title: Verwalten der Aufbewahrung von Erlebnisereignis-Datensätzen im Data Lake mithilfe von TTL
description: Erfahren Sie, wie Sie die Aufbewahrung von Erlebnisereignis-Datensätzen im Data Lake mithilfe von TTL-Konfigurationen (Time-to-Live) mit Adobe Experience Platform-APIs bewerten, festlegen und verwalten können. In diesem Handbuch wird erläutert, wie die TTL-Gültigkeit auf Zeilenebene die Richtlinien zur Datenaufbewahrung unterstützt, die Speichereffizienz optimiert und ein effektives Daten-Lifecycle-Management sicherstellt. Darüber hinaus bietet sie Anwendungsfälle und Best Practices, die Sie bei der effektiven Anwendung von TTL unterstützen.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: 767e9536862799e31d1ab5c77588d485f80c59e9
workflow-type: tm+mt
source-wordcount: '2407'
ht-degree: 1%

---

# Verwalten der Aufbewahrung von Erlebnisereignis-Datensätzen im Data Lake mithilfe von TTL

Effizientes Daten-Management ist für optimale Leistung, Kostenkontrolle und Datenintegrität von entscheidender Bedeutung. Verwenden Sie die TTL (Time-to-Live) zur Aufbewahrung von Erlebnisereignissen-Datensätzen, um eine Gültigkeit auf Zeilenebene durchzusetzen. Dabei werden veraltete Datensätze automatisch aus Datensätzen im Data Lake entfernt, während gleichzeitig eine optimale Speichereffizienz und Datenrelevanz sichergestellt wird.

In diesem Handbuch wird erläutert, wie Sie TTL mithilfe der Catalog Service-API auswerten, festlegen und verwalten können. Sie erfahren, wann und warum die TTL angewendet wird, wie TTL-Werte mithilfe von API-Aufrufen konfiguriert und aktualisiert werden und welche Best Practices die effektive Implementierung gewährleisten.

>[!IMPORTANT]
>
> TTL wurde entwickelt, um das Data Lifecycle Management und die Speichereffizienz zu optimieren. Es ist kein Compliance-Tool und sollte nicht für regulatorische Anforderungen herangezogen werden. Compliance erfordert häufig umfassendere Data-Governance-Strategien.

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
>
>TTL-Konfigurationen helfen Ihnen bei der Optimierung der Datenspeicherung basierend auf Berechtigungen. Während Profilspeicherdaten (die in Real-Time CDP verwendet werden) als veraltet betrachtet und nach 30 Tagen entfernt werden können, können dieselben Ereignisdaten im Data Lake für 12-13 Monate (oder länger basierend auf der Berechtigung) für Anwendungsfälle von Analytics und Data Distiller verfügbar bleiben.

### Branchenbeispiel {#industry-example}

Nehmen wir als Beispiel einen Video-Streaming-Service, der Benutzerinteraktionen wie Videoansichten, Suchen und Empfehlungen verfolgt. Obwohl aktuelle Interaktionsdaten für die Personalisierung von entscheidender Bedeutung sind, verlieren ältere Aktivitätsprotokolle (z. B. Interaktionen von vor mehr als einem Jahr) an Relevanz. Durch die Verwendung der Gültigkeit auf Zeilenebene entfernt Experience Platform automatisch veraltete Protokolle, sodass nur aktuelle und aussagekräftige Daten für Analysen und Empfehlungen verwendet werden.

## TTL-Eignung bewerten

Bevor Sie eine Aufbewahrungsrichtlinie anwenden, prüfen Sie, ob Ihr Datensatz ein guter Kandidat für die Gültigkeit auf Zeilenebene ist. Beachten Sie Folgendes:

- Datenrelevanz im Zeitverlauf: Bieten ältere Daten einen Wert oder sind sie veraltet?
- Auswirkungen auf nachgelagerte Prozesse: Wirkt sich das Entfernen von Daten auf die Berichterstellung, Analysen oder Integrationen aus?
- Speicherkosten im Vergleich zum Aufbewahrungswert: Rechtfertigt der Wert älterer Daten die Speicherkosten?

Wenn historische Aufzeichnungen für langfristige Analysen oder Geschäftsvorgänge unerlässlich sind, ist TTL möglicherweise nicht der richtige Ansatz. Durch die Überprüfung dieser Faktoren wird sichergestellt, dass die TTL mit Ihren Datenaufbewahrungsanforderungen übereinstimmt, ohne die Datenverfügbarkeit zu beeinträchtigen.

## Planen von Abfragen {#plan-queries}

Vor der Anwendung der TTL ist es wichtig, die Datensatzgröße und Datenrelevanz zu bewerten und zu bewerten, wie viele historische Daten aufbewahrt werden sollten. In der folgenden Abbildung wird der vollständige Prozess der Implementierung von TTL beschrieben, von der Planung von Abfragen bis zur Überwachung der Effektivität der Datenspeicherung.

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

### Überprüfen der aktuellen TTL-Einstellungen

Um mit der TTL-Verwaltung zu beginnen, überprüfen Sie zunächst die aktuellen TTL-Einstellungen. Stellen Sie eine GET-Anfrage an den `/ttl/{datasetId}`-Endpunkt, um die standardmäßigen, maximalen und minimalen TTL-Einstellungen für einen Datensatz abzurufen. Dieser Schritt ist erforderlich, da TTL-Regeln je nach Datensatztyp variieren können.

>[!TIP]
>
>Die Experience Platform-Gateway-URL und der Basispfad für die Catalog Service-API sind: `https://platform.adobe.io/data/foundation/catalog`.

**API-Format**

```http
GET /ttl/{DATASET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Eine vom System generierte Zeichenfolge, die einen Datensatz eindeutig identifiziert. Verwenden Sie den `/datasets`-Endpunkt, um eine Datensatz-ID zu finden. Anweisungen [ Filtern von Antworten für relevante Datensätze finden Sie ](../api/list-objects.md) Handbuch zur List Catalog Objects API . |

**Anfrage**

Mit der folgenden Anfrage werden die TTL-Einstellungen Ihrer Organisation für einen bestimmten Datensatz abgerufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/5ba9452f7de80408007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird die TTL-Konfiguration für den Datensatz zurückgegeben, einschließlich der standardmäßigen, maximalen und minimalen TTL-Werte für `adobe_lakeHouse`- und `adobe_unifiedProfile`.

+++Auswählen, um die Antwort anzuzeigen

```json
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P30D"
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P7D"
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Eigenschaft | Beschreibung |
|--------------|-------------|
| `defaultValue` | Der Standard-TTL-Zeitraum, der angewendet wird, wenn keine benutzerdefinierte TTL festgelegt ist. |
| `maxValue` | Die längste für den Datensatz zulässige TTL. Wenn null, gibt es keine Obergrenze. |
| `minValue` | Die kürzeste zulässige TTL, um die Einhaltung von Systemrichtlinien sicherzustellen. |

<!-- Q) what is the default Max and Min values and are they system-imposed? -->

### Festlegen der TTL für einen Datensatz {#set-ttl}

>[!IMPORTANT]
>
>Die Zeilengültigkeit kann nur auf Ereignis-Datensätze angewendet werden, die ein Zeitreihenschema verwenden. Bevor Sie die TTL festlegen, überprüfen Sie, ob das Schema des Datensatzes `https://ns.adobe.com/xdm/data/time-series` erweitert, um sicherzustellen, dass die API-Anfrage erfolgreich ist. Verwenden Sie die Schema Registry-API, um die Schemadetails abzurufen und die `meta:extends`-Eigenschaft zu überprüfen. Eine Anleitung dazu finden [ in der ](../../xdm/api/schemas.md#lookup) zum Schema-Endpunkt .

Um die Aufbewahrung von Erlebnisereignis-Datensätzen für Ihren Datensatz zu konfigurieren, legen Sie einen neuen TTL-Wert fest, indem Sie eine PATCH-Anfrage an den `/v2/datasets/{ID}`-Endpunkt senden.

**API-Format**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Die ID des Datensatzes, für den Sie den TTL-Wert aktualisieren möchten. |

**Anfrage**

In der folgenden Beispielanfrage wird die `ttlValue` auf `P3M` festgelegt. Dadurch wird sichergestellt, dass Datensätze, die älter als drei Monate sind, automatisch gelöscht werden. Sie können die Aufbewahrungsfrist an Ihre Geschäftsanforderungen anpassen, indem Sie Werte wie `P6M` für sechs Monate oder `P12M` für ein Jahr verwenden.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
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

**Antwort**

Eine erfolgreiche Antwort zeigt die TTL-Konfiguration für den Datensatz an. Es enthält Details zu Ablaufeinstellungen auf Zeilenebene sowohl für `adobe_lakeHouse`- als auch für `adobe_unifiedProfile`.

+++Auswählen, um die Antwort anzuzeigen

```JSON
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Eigenschaft | Beschreibung |
|----------------------------------|-------------|
| `extensions` | Ein Container für zusätzliche Metadaten im Zusammenhang mit dem Datensatz. |
| `extensions.adobe_lakeHouse` | Gibt Einstellungen für die Speicherarchitektur an, einschließlich Ablaufkonfigurationen auf Zeilenebene |
| `rowExpiration` | Das -Objekt enthält TTL-Einstellungen, die die Aufbewahrungsfrist für den Datensatz definieren. |
| `rowExpiration.ttlValue` | Definiert die Dauer, bevor Datensätze im Datensatz automatisch entfernt werden. Verwendet das ISO-8601-Periodenformat (z. B. `P3M` für 3 Monate oder `P30D` für eine Woche). |
| `rowExpiration.valueStatus` | Die Zeichenfolge gibt an, ob die TTL-Einstellung ein standardmäßiger Systemwert oder ein benutzerdefinierter Wert ist, der von einem Benutzer festgelegt wird. Mögliche Werte sind: `default`, `custom`. |
| `rowExpiration.setBy` | Gibt an, wer die TTL-Einstellung zuletzt geändert hat. Mögliche Werte sind: `user` (manuell eingestellt) oder `service` (automatisch zugewiesen). |
| `rowExpiration.updated` | Der Zeitstempel der letzten TTL-Aktualisierung. Dieser Wert gibt an, wann die TTL-Einstellung zuletzt geändert wurde. |

### Aktualisieren der TTL {#update-ttl}

Verlängern oder verkürzen Sie die Aufbewahrungsfrist entsprechend Ihren Geschäftsanforderungen, indem Sie die TTL anpassen. Wenn Sie beispielsweise die zuvor erwähnte Video-Streaming-Plattform in Betracht ziehen, kann die Plattform die TTL zunächst auf drei Monate festlegen, um neue Interaktionsdaten für die Personalisierung sicherzustellen. Wenn ihre Analyse jedoch zeigt, dass Interaktionsmuster, die älter als drei Monate sind, immer noch wertvolle Einblicke bieten, können sie den TTL-Zeitraum auf sechs Monate verlängern, um ältere Aufzeichnungen für bessere Empfehlungsmodelle zu behalten.

Um einen vorhandenen TTL-Wert zu ändern, verwenden Sie die `PATCH` -Methode auf dem `/v2/datasets/{DATASET_ID}`-Endpunkt.

#### API-Format

```http
PATCH /v2/datasets/{DATASET_ID}
```

**Anfrage**

In der folgenden Anfrage wird die TTL auf sechs Monate (`P6M`) aktualisiert, wodurch die Aufbewahrungsfrist für Datensätze vor dem automatischen Löschen verlängert wird.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
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

<!-- Q) For Clarity, should this example show both data stores being updated by expanding the example payload above? -->

**Antwort**

```JSON
{  "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
              "ttlValue": "P6M",
              "valueStatus": "custom",
              "setBy": "user",
              "updated": "1737977766499"
            }
        },
        "adobe_unifiedProfile": {
            "rowExpiration": {
                "ttlValue": "P3M",
                "valueStatus": "custom",
                "setBy": "user",
                "updated": "17379754766355"
            }
        }
    }
}
```

## Best Practices für das Festlegen von TTL {#best-practices}

Die Auswahl des richtigen TTL-Werts ist entscheidend, um sicherzustellen, dass Ihre Richtlinie zur Aufbewahrung von Erlebnisereignis-Datensätzen ein ausgewogenes Verhältnis zwischen Datenaufbewahrung, Speichereffizienz und Analyseanforderungen aufweist. Eine zu kurze TTL kann zu Datenverlust führen, während eine zu lange TTL die Speicherkosten und die unnötige Datenakkumulation erhöhen kann. Stellen Sie sicher, dass die TTL mit dem Zweck Ihres Datensatzes übereinstimmt, indem Sie berücksichtigen, wie oft auf die Daten zugegriffen wird und wie lange sie relevant bleiben.

Die folgende Tabelle enthält allgemeine TTL-Empfehlungen, die auf dem Datensatztyp und den Nutzungsmustern basieren:

| Datensatztyp | Empfohlene TTL | Typische Anwendungsfälle |
|-----------------------------|------------------------|-------------------|
| Häufig aufgerufene Datensätze | 30-90 Tage | Benutzerinteraktionslogs, Website-Clickstream-Daten, kurzfristige Kampagnenleistungsdaten. |
| Archivieren von Datensätzen | 1 Jahr oder mehr | Protokolle zu Finanztransaktionen, Compliance-Daten, langfristige Trendanalysen, Datensätze zu maschinellen Lernprogrammen. |
| Vom Programm verwaltete Datensätze | Bis zu 13 Monate | Systemverwaltete Datensätze verfügen über vordefinierte TTL-Einschränkungen, die automatisch erzwungen werden, um die vom System auferlegten Beschränkungen einzuhalten. |
| Vom Kunden verwaltete Datensätze | 30 Tage - Max. TTL | Über die Benutzeroberfläche, APIs oder Data Distiller erstellte Datensätze. Die TTL muss mindestens 30 Tage betragen und innerhalb der definierten maximalen TTL liegen. |

Überprüfen Sie die TTL-Einstellungen regelmäßig, um sicherzustellen, dass sie weiterhin Ihren Speicherrichtlinien, Analyseanforderungen und Geschäftsanforderungen entsprechen.

### Wichtige Aspekte beim Festlegen von TTL

<!-- What are the default TTL limits for system-generated Profile Store and data lake datasets? -->

<!-- Q) Are the limits: 90 days for data in the Profile store and 13 months for data in the data lake? This is true for Journey Optimizer. -->

Befolgen Sie die folgenden Best Practices, um sicherzustellen, dass die TTL-Einstellungen mit Ihrer Datenaufbewahrungsstrategie übereinstimmen:

- TTL-Änderungen regelmäßig überprüfen. Jeder TTL-Update-Trigger erhält ein Audit-Ereignis. Verwenden Sie Auditprotokolle, um TTL-Änderungen für Compliance-, Data Governance- und Fehlerbehebungszwecke zu verfolgen.
- TTL entfernen, wenn Daten unbegrenzt aufbewahrt werden müssen. Um TTL zu deaktivieren, setzen Sie `ttlValue` auf `null`. Dadurch wird ein automatischer Ablauf verhindert und alle Datensätze werden dauerhaft beibehalten. Berücksichtigen Sie die Auswirkungen auf den Speicher, bevor Sie diese Änderung vornehmen.

<!-- Q) Are there any specific system constraints or impacts of setting TTL to null? -->

## Einschränkungen der TTL {#limitations}

Beachten Sie die folgenden Einschränkungen bei der Verwendung von TTL:

- **Die Aufbewahrung von Erlebnisereignis-Datensätzen mithilfe der TTL gilt für die Gültigkeit auf**, nicht für das Löschen von Datensätzen. TTL entfernt Datensätze basierend auf einer definierten Aufbewahrungsfrist, löscht jedoch nicht ganze Datensätze. Um einen Datensatz zu entfernen, verwenden Sie den [Endpunkt für die Datensatzgültigkeit](../../hygiene/api/dataset-expiration.md) oder das manuelle Löschen.
- **TTL kann nicht entfernt** nur aktualisiert werden. Nach der Anwendung kann die TTL nicht mehr gelöscht werden, Sie können [die Aufbewahrungsfrist ändern](#update-ttl) um sie zu verlängern oder zu verkürzen. Um Daten auf unbestimmte Zeit beizubehalten, legen Sie eine ausreichend lange TTL fest, anstatt zu versuchen, sie zu entfernen.
- **TTL ist kein Compliance-Tool**. TTL optimiert das Speicher- und Daten-Lifecycle-Management, erfüllt jedoch nicht die gesetzlichen Anforderungen an die Datenaufbewahrung. Implementieren Sie zur Compliance umfassendere Data-Governance-Strategien.

## Häufig gestellte Fragen zur Richtlinie zur Datensatzaufbewahrung {#faqs}

In diesem Abschnitt finden Sie Antworten auf häufig gestellte Fragen zu Richtlinien zur Datensatzaufbewahrung in Adobe Experience Platform.

### Auf welche Arten von Datensätzen kann ich Regeln für Aufbewahrungsrichtlinien anwenden?

+++Antwort
Sie können Aufbewahrungsrichtlinien auf Datensätze anwenden, die mithilfe der XDM ExperienceEvent-Klasse erstellt wurden. Für Profil-Services gelten Aufbewahrungsrichtlinien nur für Erlebnisereignis-Datensätze, die für das Profil aktiviert wurden.
+++

### Wie bald löscht der Auftrag zur Datensatzaufbewahrung Daten aus Data Lake-Services?

+++Antwort
Datensatz-TTLs werden wöchentlich ausgewertet und verarbeitet und dabei werden alle abgelaufenen Datensätze gelöscht. Ein Ereignis wird als abgelaufen betrachtet, wenn es vor mehr als 30 Tagen (Aufnahmedatum > 30 Tage) in Experience Platform aufgenommen wurde und sein Ereignisdatum die definierte Aufbewahrungsfrist (TTL) überschreitet.
+++

### Wie bald löscht der Vorgang zur Datensatzaufbewahrung Daten aus Profil-Services?

+++Antwort
Nach dem Festlegen einer Aufbewahrungsrichtlinie werden vorhandene Ereignisse in Experience Platform sofort gelöscht, wenn ihr Ereigniszeitstempel die Aufbewahrungsfrist (TTL) überschreitet. Neue Ereignisse werden gelöscht, sobald ihr Zeitstempel die Aufbewahrungsfrist überschreitet.

Wenn Sie beispielsweise am 15. Mai eine 30-Tage-Gültigkeit anwenden, passiert Folgendes:

- Neue Ereignisse erhalten bei ihrer Aufnahme eine Gültigkeit von 30 Tagen.
- Vorhandene Ereignisse mit einem Zeitstempel, der älter als der 15. April ist, werden sofort gelöscht.
- Vorhandene Ereignisse mit einem Zeitstempel nach dem 15. April laufen 30 Tage nach ihrem Zeitstempel ab (ein Ereignis vom 18. April würde beispielsweise am 18. Mai gelöscht).
+++

### Kann ich unterschiedliche Aufbewahrungsrichtlinien für Data Lake- und Profil-Services festlegen?

+++Antwort
Ja, Sie können unterschiedliche Aufbewahrungsrichtlinien für Data Lake- und Profil-Services festlegen. Die Aufbewahrungsfrist für Profile darf jedoch nicht kürzer sein als die für Data Lake festgelegte.
+++

### Wie kann ich meine aktuelle Datensatznutzung überprüfen?

+++Antwort
Sie können die neueste Datensatzspeichergröße für Data Lake- und Profilspeicher als separate Metriken im Inventar-Arbeitsbereich [!UICONTROL Datensatz] überprüfen. Sortieren Sie die Spalten, um die größten Datensätze zu identifizieren, und überprüfen Sie, ob Aufbewahrungsrichtlinien angewendet werden.

Weitere Informationen zur Verwendung auf Sandbox-Ebene finden Sie unter Lizenznutzungs-Dashboard . Weitere Informationen finden [ unter &quot;](../../dashboards/guides/license-usage.md)&quot;.
+++

### Wie kann ich überprüfen, ob der Datenaufbewahrungsauftrag erfolgreich war?

+++Antwort
Sie können den letzten Datenaufbewahrungsauftrag überprüfen, indem Sie dessen Zeitstempel in der [Benutzeroberfläche für die Datensatzaufbewahrungskonfiguration](./user-guide.md#data-retention-policy) oder auf der Seite „Dateninventar“ überprüfen.

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
