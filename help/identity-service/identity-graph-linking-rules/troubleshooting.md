---
title: Fehlerbehebungshandbuch für Identitätsdiagramm-Verknüpfungsregeln
description: Erfahren Sie, wie Sie häufige Probleme in den Regeln zur Identitätsdiagrammverlinkung beheben können.
badge: Beta
source-git-commit: cb0e229ac68f53d33b83d54df4062469252f06a3
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 0%

---

# Fehlerbehebungshandbuch für Regeln zur Identitätsdiagrammzuordnung

>[!AVAILABILITY]
>
>Die Regelfunktion zur Verknüpfung von Identitätsdiagrammen befindet sich derzeit in der Beta-Phase. Wenden Sie sich an Ihr Adobe-Account-Team, um Informationen zu den Teilnahmekriterien zu erhalten. Die Funktion und die Dokumentation können sich ändern.

Beim Testen und Validieren der Verknüpfungsregeln von Identitätsdiagrammen können Probleme im Zusammenhang mit der Datenerfassung und dem Verhalten von Diagrammen auftreten. In diesem Dokument erfahren Sie, wie Sie einige häufige Probleme beheben können, die bei der Arbeit mit Regeln zur Identitätsdiagrammzuordnung auftreten können.

## Übersicht über den Datenerfassungsfluss {#data-ingestion-flow-overview}

Das folgende Diagramm zeigt eine vereinfachte Darstellung des Datenflusses in Adobe Experience Platform und Anwendungen. Verwenden Sie dieses Diagramm als Referenz, um ein besseres Verständnis des Inhalts dieser Seite zu erhalten.

![Ein Diagramm, wie die Datenerfassung im Identity Service abläuft.](../images/troubleshooting/dataflow_in_identity.png)

Es ist wichtig, die folgenden Faktoren zu beachten:

* Für Streaming-Daten beginnen Echtzeit-Kundenprofil, Identity Service und Data Lake mit der Verarbeitung der Daten, wenn die Daten gesendet werden. Die Wartezeit beim Abschluss der Datenverarbeitung hängt jedoch vom Dienst ab. Normalerweise dauert die Verarbeitung von Data Lake im Vergleich zu Profil und Identität länger.
   * Wenn die Daten beim Ausführen einer Abfrage für einen Datensatz auch nach einigen Stunden nicht angezeigt werden, werden die Daten wahrscheinlich nicht in Experience Platform erfasst.
* Bei Batch-Daten fließen alle Daten zuerst in den Data Lake, dann werden die Daten an Profil und Identität weitergeleitet, wenn der Datensatz für Profil und Identität aktiviert ist.
* Bei Problemen mit der Erfassung ist es wichtig, dass das Problem auf Dienstebene isoliert wird, um genaues Debugging und Fehlerbehebung zu erhalten. Es gibt drei mögliche Problemtypen, die berücksichtigt werden müssen:

| Ingestion-Problemtyp | Werden die Daten im Data Lake erfasst? | Werden die Daten im Profil erfasst? | Werden die Daten im Identity Service erfasst? |
| --- | --- | --- | --- |
| Allgemeine Aufnahmeproblematik | Nein | Nein | Nein |
| Grafikproblem | Ja | Ja | Nein |
| Problem mit Profilfragmenten | Ja | Nein | Ja |

## Probleme bei der Datenerfassung {#data-ingestion-issues}

>[!NOTE]
>
>* In diesem Abschnitt wird davon ausgegangen, dass die Daten erfolgreich in den Data Lake aufgenommen wurden und dass keine Syntax- oder anderen Fehler aufgetreten sind, die verhindern würden, dass die Daten überhaupt in Experience Platform aufgenommen werden.
>
>* Die Beispiele verwenden ECID als Cookie-Namespace und CRMID als Personen-Namespace.

### Meine Identitäten werden nicht in Identity Service erfasst{#my-identities-are-not-getting-ingested-into-identity-service}

Es gibt verschiedene Gründe, warum dies passieren könnte, unter anderem die folgenden:

* [Der Datensatz ist für Profil](../../catalog/datasets/enable-for-profile.md) nicht aktiviert.
* Der Datensatz wird übersprungen, da es nur eine Identität im Ereignis gibt.
* [Im Identity Service ](../guardrails.md#identity-value-validation) ist ein Überprüfungsfehler aufgetreten.
   * Beispielsweise könnte eine ECID die maximale Länge von 38 Zeichen überschritten haben.
* Standardmäßig sind [AAIDs von der Aufnahme ausgeschlossen](../guardrails.md#identity-namespace-ingestion).
* Die Identität wird aufgrund von [System-Limits](../guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated) entfernt.

Im Kontext von Regeln zur Zuordnung von Identitätsdiagrammen kann ein Datensatz vom Identity Service abgelehnt werden, da das eingehende Ereignis zwei oder mehr Identitäten mit demselben eindeutigen Namespace, aber einem anderen Identitätswert aufweist. Dieses Szenario tritt normalerweise aufgrund von Implementierungsfehlern auf.

Betrachten Sie das folgende Ereignis mit zwei Annahmen:

* Der Feldname CRMID wird als Identität mit dem Namespace CRMID markiert.
* Der Namespace CRMID ist als eindeutiger Namespace definiert.

Das folgende Ereignis gibt eine Fehlermeldung zurück, die angibt, dass die Aufnahme fehlgeschlagen ist.

<!-- because the ingestion of this erroneous event would have resulted in graph collapse. In the following event, two entities (Alice and Bob) are both associated with the same namespace (CRMID). -->

```json
{ 
  "_id": "random_string", 
  "eventType": "web browsing event", 
  "identityMap": { 
    "ECID": [ 
      { 
        "id": "11111111111111111111111111111111111111", 
        "primary": false 
      } 
    ], 
    "CRMID": [ 
      { 
        "id": "Alice", 
        "primary": true 
      } 
    ] 
  }, 
  "CRMID": "Bob", 
  "timestamp": "2024-08-17T15:22:51+00:00", 
  "web": { 
    "webPageDetails": { 
      "URL": "https://www.adobe.com/acrobat.html", 
      "name": "Adobe Acrobat" 
    } 
  } 
} 
```

**Schritte zur Fehlerbehebung**

Um diesen Fehler zu beheben, müssen Sie zunächst die folgenden Informationen erfassen:

* Der Identitätswert (`identity_value`), den Sie für die Aufnahme in das Identitätsdiagramm erwartet haben.
* Der Datensatz (`dataset_name`), in dem das Ereignis gesendet wurde.

Verwenden Sie als Nächstes [Adobe Experience Platform Query Service](../../query-service/home.md) und führen Sie die folgende Abfrage aus:

>[!TIP]
>
>Ersetzen Sie `dataset_name` und `identity_value` durch die erfassten Informationen.

```sql
  SELECT key, col.id as identityValue, timestamp, _id, identityMap, * 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id = 'identity_value' 
```

Suchen Sie nach der Ausführung Ihrer Abfrage den Ereignisdatensatz, von dem Sie erwartet haben, dass er ein Diagramm generiert, und überprüfen Sie dann, ob die Identitätswerte in derselben Zeile unterschiedlich sind. Sehen Sie sich das folgende Bild für ein Beispiel an:

![Eine unbenannte Abfrage, die zu duplizierten Namespaces führte.](../images/troubleshooting/duplicated_unique_namespace.png)

>[!NOTE]
>
>Wenn die beiden Identitäten identisch sind und das Ereignis über Streaming erfasst wird, deduplizieren sowohl Identity als auch Profile die Identität.

### Meine Erlebnisereignisfragmente werden nicht in das Profil aufgenommen {#my-experience-event-fragments-are-not-getting-ingested-into-profile}

Es gibt verschiedene Gründe, warum Ihre Erlebnisereignisfragmente nicht in das Profil aufgenommen werden, darunter:

* [Der Datensatz ist für Profil](../../catalog/datasets/enable-for-profile.md) nicht aktiviert.
* [Möglicherweise ist ein Überprüfungsfehler in Profil](../../xdm/classes/experienceevent.md) aufgetreten.
   * Beispielsweise muss ein Erlebnisereignis sowohl ein `_id` als auch ein `timestamp` enthalten.
   * Darüber hinaus muss der `_id` für jedes Ereignis (Datensatz) eindeutig sein.

Im Zusammenhang mit der Namespace-Priorität lehnt das Profil alle Ereignisse ab, die zwei oder mehr Identitäten mit der höchsten Namespace-Priorität enthalten. Wenn beispielsweise GAID nicht als eindeutiger Namespace markiert ist und zwei Identitäten mit einem GAID-Namespace und verschiedenen Identitätswerten eingehen, speichert Profil keines der Ereignisse.

**Schritte zur Fehlerbehebung**

Um diesen Fehler zu beheben, lesen Sie die im obigen Handbuch beschriebenen Schritte zur Fehlerbehebung unter [Fehlerbehebung bei Fehlern bei der Erfassung von Daten in Identity Service](#my-identities-are-not-getting-ingested-into-identity-service).

### Meine Erlebnisereignisfragmente werden erfasst, haben jedoch die &quot;falsche&quot;primäre Identität im Profil.

Die Namespace-Priorität spielt eine wichtige Rolle bei der Bestimmung der primären Identität durch Ereignisfragmente.

* Nachdem Sie Ihre [Identitätseinstellungen](./identity-settings-ui.md) für eine bestimmte Sandbox konfiguriert und gespeichert haben, verwendet das Profil die [Namespace-Priorität](namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events), um die primäre Identität zu bestimmen. Im Falle von identityMap verwendet das Profil dann nicht mehr das `primary=true` -Flag.
* Während Profile nicht mehr auf diese Markierung verweisen, können andere Dienste auf Experience Platform weiterhin die Markierung `primary=true` verwenden.

Damit [authentifizierte Benutzerereignisse](configuration.md#ingest-your-data) an den Personen-Namespace gebunden werden können, müssen alle authentifizierten Ereignisse den Personen-Namespace (CRMID) enthalten. Das bedeutet, dass der Personen-Namespace auch nach der Anmeldung eines Benutzers bei jedem authentifizierten Ereignis vorhanden sein muss.

Wenn Sie ein Profil in der Profilansicht suchen, wird möglicherweise weiterhin die Markierung `primary=true` &#39;events&#39; angezeigt. Dies wird jedoch ignoriert und vom Profil nicht verwendet.

AAIDs werden standardmäßig blockiert. Wenn Sie daher den Quell-Connector [Adobe Analytics ](../../sources/tutorials/ui/create/adobe-applications/analytics.md) verwenden, müssen Sie sicherstellen, dass die ECID höher als die ECID priorisiert ist, damit die nicht authentifizierten Ereignisse die primäre Identität ECID aufweisen.

**Schritte zur Fehlerbehebung**

* Um zu überprüfen, ob authentifizierte Ereignisse sowohl den Personen- als auch den Cookie-Namespace enthalten, lesen Sie die Schritte, die im Abschnitt [Fehlerbehebung bei Fehlern bei der Erfassung von Daten, die nicht in Identity Service aufgenommen werden](#my-identities-are-not-getting-ingested-into-identity-service) beschrieben sind.
* Um zu überprüfen, ob authentifizierte Ereignisse die primäre Identität des Personen-Namespace haben (z. B. CRMID), suchen Sie den Personen-Namespace im Profil-Viewer mithilfe der Zusammenführungsrichtlinie ohne Zuordnung (dies ist die Zusammenführungsrichtlinie, die kein privates Diagramm verwendet). Diese Suche gibt nur Ereignisse zurück, die mit dem Personen-Namespace verknüpft sind.

## Probleme mit dem Diagrammverhalten {#graph-behavior-related-issues}

In diesem Abschnitt werden häufig auftretende Probleme bezüglich des Verhaltens des Identitätsdiagramms beschrieben.

### Die Identität wird mit der &quot;falschen&quot;Person verknüpft

Der Identitätsoptimierungsalgorithmus berücksichtigt [die zuletzt eingerichteten Links und entfernt die ältesten Links](./identity-optimization-algorithm.md#identity-optimization-algorithm-details). Daher ist es möglich, dass ECIDs nach Aktivierung dieser Funktion von einer Person zu einer anderen neu zugeordnet (neu verknüpft) werden können. Gehen Sie wie folgt vor, um den Verlauf der Verknüpfung einer Identität im Zeitverlauf zu verstehen:

**Schritte zur Fehlerbehebung**

>[!NOTE]
>
>Die folgenden Schritte werden Informationen unter den folgenden Annahmen abrufen:
>
>* Es wird ein einzelner Datensatz verwendet (dabei werden nicht mehrere Datensätze abgefragt).
>
>* Die Daten werden nicht aus dem Data Lake gelöscht, da [Advanced Data Lifecycle Management](../../hygiene/home.md), [Privacy Service](../../privacy-service/home.md) oder andere Dienste, die Löschvorgänge durchführen, gelöscht werden.

Zunächst müssen Sie die folgenden Informationen erfassen:

* Das Identitäts-Symbol (namespaceCode) des Cookie-Namespace (z. B. ECID) und der Personen-Namespace (z. B. CRMID), die gesendet wurden.
   * Bei Web SDK-Implementierungen sind dies normalerweise die Namespaces, die in der identityMap enthalten sind.
   * Bei Implementierungen des Analytics-Quell-Connectors handelt es sich um die Cookie-ID, die in der identityMap enthalten ist. Die Personenkennung ist ein eVar, das als Identität gekennzeichnet ist.
* Der Datensatz, in dem das Ereignis gesendet wurde (dataset_name).
* Der Identitätswert des zu suchenden Cookie-Namespace (identity_value).

Bei Identitätssymbolen (namespaceCode) wird zwischen Groß- und Kleinschreibung unterschieden. Um alle Identitätssymbole für einen bestimmten Datensatz in der identityMap abzurufen, führen Sie die folgende Abfrage aus:

```sql
SELECT distinct explode(*)FROM (SELECT map_keys(identityMap) FROM dataset_name)
```

Wenn Sie den Identitätswert Ihrer Cookie-ID nicht kennen und nach einer Cookie-ID suchen möchten, die mit mehreren Personen-IDs verknüpft wäre, müssen Sie die folgende Abfrage ausführen. Bei dieser Abfrage wird ECID als Cookie-Namespace und CRMID als Personen-Namespace angenommen.

>[!BEGINTABS]

>[!TAB Web SDK-Implementierung]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct identityMap['CRMID'][0]['id']) as crmidCount FROM dataset_name GROUP BY identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

>[!TAB Implementierung des Analytics-Quell-Connectors]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct personID) as crmidCount FROM dataset_name group by identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

**Hinweis:** personID bezieht sich auf den Pfad des Deskriptors. Sie finden diese Informationen unter Schemata.

>[!ENDTABS]

Überprüfen Sie anschließend die Zuordnung des Cookie-Namespace in der Reihenfolge des Zeitstempels, indem Sie die folgende Abfrage ausführen:

>[!BEGINTABS]

>[!TAB Web SDK-Implementierung]

```sql
  SELECT identityMap['CRMID'][0]['id'] as personEntity, * 
  FROM dataset_name 
  WHERE identitymap['ECID'][0].id ='identity_value' 
  ORDER BY timestamp desc 
```

>[!TAB Implementierung des Analytics-Quell-Connectors]

```sql
SELECT _experience.analytics.customDimensions.eVars.eVar10 as personEntity, * 
FROM dataset_name 
WHERE identitymap['ECID'][0].id ='identity_value' 
ORDER BY timestamp desc 
```

**Hinweis**: In diesem Beispiel wird davon ausgegangen, dass `eVar10` als Identität markiert ist. Für Ihre Konfigurationen müssen Sie die eVar basierend auf der Implementierung Ihres Unternehmens ändern.

>[!ENDTABS]

### Der Identitätsoptimierungsalgorithmus funktioniert nicht erwartungsgemäß

**Schritte zur Fehlerbehebung**

Weitere Informationen finden Sie in der Dokumentation zum [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md) sowie in den Typen der unterstützten Diagrammstrukturen.

* Beispiele für unterstützte Diagrammstrukturen finden Sie im [Konfigurationshandbuch für Diagramme](./example-configurations.md) .
* Beispiele für nicht unterstützte Diagrammstrukturen finden Sie auch im [Implementierungshandbuch](./configuration.md#appendix) . Es können zwei Szenarien eintreten:
   * Kein einzelner Namespace für alle Profile.
   * Ein [&quot;dangling ID&quot;](./configuration.md#dangling-loginid-scenario) -Szenario tritt auf. In diesem Szenario kann Identity Service nicht ermitteln, ob die verwundbare ID mit einer der Personen-Entitäten in den Diagrammen verknüpft ist.

Sie können auch das Tool zur [Diagrammsimulation in der Benutzeroberfläche](./graph-simulation.md) verwenden, um Ereignisse zu simulieren und Ihre eigenen eindeutigen Namespace- und Namespace-Prioritätseinstellungen zu konfigurieren. Dies kann Ihnen dabei helfen, ein grundlegendes Verständnis dafür zu erhalten, wie sich der Identitätsoptimierungsalgorithmus verhalten sollte.

Wenn Ihre Simulationsergebnisse mit Ihren Erwartungen an das Diagrammverhalten übereinstimmen, können Sie überprüfen, ob Ihre [Identitätseinstellungen](./identity-settings-ui.md) mit den Einstellungen übereinstimmen, die Sie in Ihrer Simulation konfiguriert haben.

### Selbst nach dem Konfigurieren von Identitätseinstellungen werden in meiner Sandbox ausgeblendete Diagramme angezeigt.

Identitätsdiagramme entsprechen Ihrem konfigurierten eindeutigen Namespace und Ihrer Namespace-Priorität _nach_ der Speicherung der Einstellungen. Alle &quot;ausgeblendeten&quot;Diagramme, die _vor_ vorhanden sind, wenn Sie Ihre neuen Einstellungen speichern, sind davon nicht betroffen, bis neue Daten so erfasst werden, dass das ausgeblendete Diagramm aktualisiert wird. Die primäre Identität von Ereignisfragmenten im Echtzeit-Kundenprofil wird nicht aktualisiert, selbst wenn sich die Namespace-Priorität ändert.

**Schritte zur Fehlerbehebung**

Mit dem Viewer für Identitätsdiagramme ](../features/identity-graph-viewer.md) können Sie überprüfen, ob Ihr Diagramm vor oder nach Ihren Einstellungen erfasst wurde. [ Überprüfen Sie den letzten aktualisierten Zeitstempel unter [!UICONTROL Link-Eigenschaften] , um zu sehen, wann der Identity Service das Diagramm erfasst hat. Wenn der Zeitstempel vor der Konfiguration liegt, deutet dies darauf hin, dass das &quot;reduzierte&quot;Diagramm erstellt wurde, bevor die Funktion aktiviert wurde.

![Der Identitätsdiagramm-Viewer mit einem Beispieldiagramm.](../images/troubleshooting/graph_viewer.png)

### Ich möchte wissen, wie viele &quot;reduzierte&quot;Diagramme in meiner Sandbox vorhanden sind.

Verwenden Sie das Identitäts-Dashboard , um Einblicke in den Status Ihres Identitätsdiagramms zu erhalten, z. B. die Anzahl der Identitäten und Diagramme. Siehe Metrik &quot;Diagrammanzahl mit mehreren Namespaces&quot;für eine Anzahl von Diagrammen, die reduziert wurden. Hierbei handelt es sich um Diagramme, die zwei oder mehr Identitäten mit demselben Namespace enthalten. Wenn die Sandbox keine Daten enthält und Sie einen Namespace (z. B. CRMID) als eindeutig konfiguriert haben, wird erwartet, dass es keine Diagramme mit zwei oder mehr CRMIDs gibt. Im folgenden Beispiel sind zwei Diagramme mit zwei oder mehr E-Mail-Adressen enthalten.

![Das Identitäts-Dashboard mit Metriken zur Identitätsanzahl, zur Diagrammanzahl, zur Anzahl nach Namespace, zur Diagrammanzahl nach Größe und zur Diagrammanzahl von Diagrammen mit mehr als zwei Namespaces.](../images/troubleshooting/identity_dashboard.png)

Sie können eine detaillierte Aufschlüsselung des [Profil-Snapshot-Exportdatensatzes](../../dashboards/query.md) im Data Lake finden, indem Sie die folgende Abfrage ausführen:

>[!NOTE]
>
>* Ersetzen Sie `dataset_name` durch den tatsächlichen Namen Ihres Datensatzes.
>
>* Die Zahlen stimmen möglicherweise nicht genau überein. Das Identitäts-Dashboard basiert auf der Anzahl der Identitätsdiagramme und die folgende Abfrage basiert auf der Anzahl der Profile mit zwei oder mehr Identitäten. Die Daten werden unabhängig voneinander verarbeitet und vom Dienst aktualisiert.

```sql
  SELECT key, identityCountInGraph, count(identityCountInGraph) as graphCount 
  FROM (SELECT key, cardinality(value) as identityCountInGraph 
  FROM (SELECT explode(identityMap) 
  FROM dataset_name 
  WHERE cardinality(identityMap) > 1)) /* by definition, graphs have 2 or more identities */ 
  WHERE key not in ('ecid', 'aaid', 'idfa', 'gaid') /* filter out common device/cookie namespaces */ 
  GROUP BY 1, 2 
  ORDER BY 1, 2 asc 
```

Sie können die folgende Abfrage im Datensatz zum Exportieren von Profilmomentdaten verwenden, um Beispielidentitäten aus &quot;reduzierten&quot;Diagrammen zu erhalten.

```sql
  SELECT identityMap 
  FROM dataset_name 
  WHERE cardinality(identityMap['CRMID'])>1 /* any graphs with 2+ CRMID. Change CRMID namespace if needed */ 
```

>[!TIP]
>
>Die beiden oben aufgeführten Abfragen liefern erwartete Ergebnisse, wenn die Sandbox nicht für den gemeinsamen Gerätezeitansatz aktiviert ist, und unterscheiden sich von den Verknüpfungsregeln für Identitätsdiagramme.