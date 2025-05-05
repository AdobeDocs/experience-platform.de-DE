---
keywords: Experience Platform;Identität;Identity Service;Fehlerbehebung;Leitplanken;Richtlinien;Limit;
title: Leitplanken für Identity Service
description: Dieses Dokument enthält Informationen zur Verwendung und zu den Ratenbeschränkungen für Identity Service-Daten, damit Sie die Verwendung des Identitätsdiagramms optimieren können.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1586'
ht-degree: 39%

---

# Leitplanken für [!DNL Identity Service] Daten

Dieses Dokument enthält Informationen über die Verwendung und die Ratenbeschränkungen für [!DNL Identity Service]-Daten, um Ihnen bei der optimalen Nutzung des Identitätsdiagramms zu helfen. Bei der Überprüfung der folgenden Leitplanken wird davon ausgegangen, dass Sie die Daten korrekt modelliert haben. Wenden Sie sich bei Fragen zum Modellieren Ihrer Daten an Ihren Kundenbetreuer.

>[!IMPORTANT]
>
>Überprüfen Sie zusätzlich zu dieser Seite mit Leitplanken Ihre Lizenzberechtigungen in Ihrem Kundenauftrag und [ entsprechenden ](https://helpx.adobe.com/de/legal/product-descriptions.html)Produktbeschreibung) die tatsächlichen Nutzungsbeschränkungen.

## Erste Schritte

Die folgenden Experience Platform-Dienste sind an der Modellierung von Identitätsdaten beteiligt:

* [Identitäten](home.md): Bridge-Identitäten aus unterschiedlichen Datenquellen bei der Aufnahme in Experience Platform.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Erstellen einheitlicher Verbraucherprofile anhand von Daten aus mehreren Quellen.

## Datenmodellbeschränkungen

Die folgenden Tabellen enthalten Anleitungen zu Leitlinien für statische Beschränkungen sowie zu berücksichtigende Validierungsregeln für Identity-Namespaces.

### Statische Beschränkungen

In der folgenden Tabelle sind statische Beschränkungen für Identitätsdaten aufgeführt.

| Leitplanke | Limit | Anmerkungen |
| --- | --- | --- |
| Anzahl der Identitäten in einem Diagramm | 50 | Wenn ein Diagramm mit 50 verknüpften Identitäten aktualisiert wird, wendet Identity Service einen „first-in, first-out“-Mechanismus an und löscht die älteste Identität, um Platz für die neueste Identität für dieses Diagramm zu schaffen (**Hinweis**: Das Echtzeit-Kundenprofil ist nicht betroffen). Das Löschen basiert auf Identitätstyp und Zeitstempel. Die Beschränkung wird auf Sandbox-Ebene angewendet. Weitere Informationen finden Sie im Abschnitt zu [Grundlagen zur Löschlogik](#deletion-logic). |
| Anzahl der Links zu einer Identität für eine einzelne Batch-Aufnahme | 50 | Ein einzelner Batch kann anormale Identitäten enthalten, die unerwünschte Diagrammzusammenführungen verursachen. Um dies zu verhindern, nimmt Identity Service keine Identitäten auf, die bereits mit 50 oder mehr Identitäten verknüpft sind. |
| Anzahl der Identitäten in einem XDM-Eintrag | 20 | Die erforderliche Mindestanzahl von XDM-Einträgen beträgt zwei. |
| Anzahl der benutzerdefinierten Namespaces | Keine | Die Anzahl der benutzerdefinierten Namespaces, die Sie erstellen können, ist unbegrenzt. |
| Anzahl der Zeichen für einen Namespace-Anzeigenamen oder ein Identitätssymbol | Keine | Die Anzahl der Zeichen eines Namespace-Anzeigenamens oder Identitätssymbols ist unbegrenzt. |

{style="table-layout:auto"}

### Überprüfung des Identitätswerts

In der folgenden Tabelle sind die vorhandenen Regeln aufgeführt, die Sie befolgen müssen, um eine erfolgreiche Überprüfung Ihres Identitätswerts sicherzustellen.

| Namespace | Validierungsregel | Systemverhalten bei Verletzung einer Regel |
| --- | --- | --- |
| ECID | <ul><li>Der Identitätswert einer ECID muss genau 38 Zeichen betragen.</li><li>Der Identitätswert einer ECID darf nur aus Zahlen bestehen.</li></ul> | <ul><li>Wenn der Identitätswert der ECID nicht genau 38 Zeichen beträgt, wird der Eintrag übersprungen.</li><li>Wenn der Identitätswert der ECID nicht-numerische Zeichen enthält, wird der Eintrag übersprungen.</li></ul> |
| Nicht-ECID | <ul><li>Der Identitätswert darf 1024 Zeichen nicht überschreiten.</li><li>Identitätswerte dürfen nicht „null“, „anonym“, „ungültig“ oder eine leere Zeichenfolge sein (z. B.: &quot;&quot;, &quot;&quot;, &quot;„).</li></ul> | <ul><li>Wenn der Identitätswert 1024 Zeichen überschreitet, wird der Eintrag übersprungen.</li><li>Die Identität wird bei der Aufnahme blockiert.</li></ul> |

{style="table-layout:auto"}

### Aufnahme von Identity-Namespaces

Ab dem 31. März 2023 blockiert Identity Service die Aufnahme der Adobe Analytics ID (AAID) für neue Kundinnen und Kunden. Diese Identität wird normalerweise über die [Adobe Analytics-Quelle](../sources/connectors/adobe-applications/analytics.md) und die [Adobe Audience Manager-Quelle](../sources//connectors/adobe-applications/audience-manager.md) aufgenommen und ist überflüssig, da die ECID denselben Webbrowser darstellt. Wenn Sie diese Standardkonfiguration ändern möchten, wenden Sie sich an Ihr Adobe-Accountteam.

## Performance-Garantien {#performance-guardrails}

Identity Service überwacht eingehende Daten kontinuierlich, um eine hohe Leistung und Zuverlässigkeit in jedem Maßstab zu gewährleisten. Ein kurzer Zustrom von Erlebnisereignisdaten kann jedoch zu Leistungseinbußen und Latenzzeiten führen. Adobe ist für eine solche Leistungsbeeinträchtigung nicht verantwortlich.

## Verstehen der Löschlogik, wenn ein Identitätsdiagramm bei Kapazität aktualisiert wird {#deletion-logic}

Wenn ein vollständiges Identitätsdiagramm aktualisiert wird, löscht Identity Service die älteste Identität im Diagramm, bevor die neueste Identität hinzugefügt wird. Dies dient der Gewährleistung der Genauigkeit und Relevanz von Identitätsdaten. Dieser Löschvorgang folgt zwei Hauptregeln:

### Regel 1: Löschung wird basierend auf dem Identitätstyp eines Namespace priorisiert

Die Löschpriorität lautet wie folgt:

1. Cookie-ID
2. Geräte-ID
3. Geräteübergreifende ID, E-Mail und Telefon

### Regel 2: Löschung basiert auf dem Zeitstempel, der in der Identität gespeichert ist

Jede in einem Diagramm verknüpfte Identität hat einen eigenen Zeitstempel. Wenn ein vollständiges Diagramm aktualisiert wird, löscht Identity Service die Identität mit dem ältesten Zeitstempel.

Wenn ein vollständiges Diagramm mit einer neuen Identität aktualisiert wird, bestimmen diese beiden Regeln gemeinsam, welche der älteren Identitäten gelöscht wird. Identity Service löscht zunächst die älteste Cookie-ID, dann die älteste Geräte-ID und schließlich die älteste geräteübergreifende ID/E-Mail/Telefon.

>[!NOTE]
>
>Wenn die zu löschende Identität mit mehreren anderen Identitäten im Diagramm verknüpft ist, werden auch die Verknüpfungen, die diese Identität verbinden, gelöscht.

### Auswirkungen auf die Implementierung

In den folgenden Abschnitten werden die Auswirkungen beschrieben, die die Löschlogik auf Identity Service, das Echtzeit-Kundenprofil und WebSDK hat.

#### Identity Service: Änderungen am Identitätstyp des benutzerdefinierten Namespace

Wenden Sie sich an Ihr Adobe-Konto-Team, um eine Änderung des Identitätstyps anzufordern, wenn Ihre Produktions-Sandbox Folgendes enthält:

* Ein benutzerdefinierter Namespace, in dem die Personen-IDs (z. B. CRMIDs) als Cookie-/Geräte-Identitätstyp konfiguriert sind.
* Ein benutzerdefinierter Namespace, in dem Cookie-/Geräte-IDs als geräteübergreifender Identitätstyp konfiguriert sind.

Sobald diese Funktion verfügbar ist, werden Diagramme, die die Beschränkung von 50 Identitäten überschreiten, auf bis zu 50 Identitäten reduziert. Für Real-Time CDP B2C Edition konnte dies zu einem minimalen Anstieg der Anzahl der Profile führen, die sich für eine Zielgruppe qualifizieren, da diese Profile zuvor von der Segmentierung und Aktivierung ignoriert wurden.

#### Echtzeit-Kundenprofil: Auswirkungen auf adressierbare Zielgruppen

Daten werden nur im Identity Service gelöscht, nicht jedoch im Echtzeit-Kundenprofil.

* Dieses Verhalten könnte daher mehr Profile mit einer einzelnen ECID erstellen, da die ECID nicht mehr Teil des Identitätsdiagramms ist.
* Damit Sie innerhalb Ihrer adressierbaren Zielgruppen-Berechtigungsnummern bleiben, wird empfohlen, Ablauf von [pseudonymen Profildaten“ zu aktivieren](../profile/pseudonymous-profiles.md) um Ihre alten Profile zu löschen.

#### Echtzeit-Kundenprofil und WebSDK: Primäre Identitätslöschung

Wenn Sie Ihre authentifizierten Ereignisse gegen die CRMID beibehalten möchten, wird empfohlen, Ihre primären IDs von ECID zu CRMID zu ändern. Anweisungen zum Implementieren dieser Änderung finden Sie in den folgenden Dokumenten:

* [Konfigurieren der Identitätszuordnung für Experience Platform-Tags](../tags/extensions/client/web-sdk/data-element-types.md#identity-map).
* [Identitätsdaten in der Experience Platform Web SDK](../web-sdk/identity/overview.md#using-identitymap)

### Beispielszenarien

#### Beispiel 1: Typisch großes Diagramm

*Diagrammhinweise:*

* `t` = Zeitstempel.
* Der Wert eines Zeitstempels entspricht der Neuigkeit einer bestimmten Identität. Beispielsweise stellt `t1` die erste verknüpfte Identität (älteste) dar und `t51` die neueste verknüpfte Identität.

In diesem Beispiel löscht Identity Service zuerst die vorhandene Identität mit dem ältesten Zeitstempel, bevor das Diagramm auf der linken Seite mit einer neuen Identität aktualisiert werden kann. Da die älteste Identität jedoch eine Geräte-ID ist, überspringt Identity Service diese Identität, bis er zum Namespace mit einem Typ gelangt, der höher in der Liste mit Löschprioritäten ist, was in diesem Fall `ecid-3` ist. Sobald die älteste Identität mit einer höheren Löschpriorität entfernt wurde, wird das Diagramm mit einer neuen Verknüpfung, `ecid-51`, aktualisiert.

* In dem seltenen Fall, dass es zwei Identitäten mit demselben Zeitstempel und Identitätstyp gibt, sortiert Identity Service die IDs nach [XID](./api/list-native-id.md) und führt den Löschvorgang durch.

![Ein Beispiel für die älteste Identität, die gelöscht wird, um die neueste Identität aufzunehmen](./images/graph-limits-v3.png)

#### Beispiel 2: „Graph split“

>[!BEGINTABS]

>[!TAB Eingehendes Ereignis]

*Diagrammhinweise:*

* Im folgenden Diagramm wird davon ausgegangen, dass `timestamp=50` 50 Identitäten im Identitätsdiagramm vorhanden sind.
* `(...)` gibt die anderen Identitäten an, die bereits innerhalb des Diagramms verknüpft sind.

In diesem Beispiel wird ECID:32110 aufgenommen und mit einem großen Diagramm bei `timestamp=51` verknüpft, wodurch die Beschränkung von 50 Identitäten überschritten wird.

![](./images/guardrails/before-split.png)

>[!TAB Löschvorgang]

Daher löscht Identity Service die älteste Identität basierend auf Zeitstempel und Identitätstyp. In diesem Fall wird ECID:35577 nur aus dem Identitätsdiagramm gelöscht.

![](./images/guardrails/during-split.png)

>[!TAB Diagrammausgabe]

Durch das Löschen von ECID:35577 werden auch die Edges gelöscht, die CRMID:60013 und CRMID:25212 mit der jetzt gelöschten ECID:35577 verknüpft haben. Dieser Löschvorgang führt dazu, dass das Diagramm in zwei kleinere Diagramme aufgeteilt wird.

![](./images/guardrails/after-split.png)

>[!ENDTABS]

#### Beispiel 3: „Hub-and-Spoke“

>[!BEGINTABS]

>[!TAB Eingehendes Ereignis]

*Diagrammhinweise:*

* Im folgenden Diagramm wird davon ausgegangen, dass `timestamp=50` 50 Identitäten im Identitätsdiagramm vorhanden sind.
* `(...)` gibt die anderen Identitäten an, die bereits innerhalb des Diagramms verknüpft sind.

Aufgrund der Löschlogik können auch einige „Hub“-Identitäten gelöscht werden. Diese Hub-Identitäten beziehen sich auf Knoten, die mit mehreren individuellen Identitäten verknüpft sind, deren Verknüpfung andernfalls aufgehoben würde.

Im folgenden Beispiel wird ECID:21011 aufgenommen und mit dem Diagramm unter `timestamp=51` verknüpft, wodurch die Beschränkung von 50 Identitäten überschritten wird.

![](./images/guardrails/hub-and-spoke-start.png)

>[!TAB Löschvorgang]

Daher löscht Identity Service die älteste Identität nur aus dem Identitätsdiagramm, in diesem Fall ECID:35577. Das Löschen von ECID:35577 führt auch zum Löschen der folgenden Elemente:

* Die Verknüpfung zwischen CRMID: 60013 und der jetzt gelöschten ECID:35577, was zu einem Szenario mit einer Diagrammaufspaltung führt.
* IDFA: 32110, IDFA: 02383 und die verbleibenden Identitäten, die von `(...)` repräsentiert werden. Diese Identitäten werden gelöscht, da sie einzeln nicht mit anderen Identitäten verknüpft sind und daher nicht in einem Diagramm dargestellt werden können.

![](./images/guardrails/hub-and-spoke-process.png)

>[!TAB Diagrammausgabe]

Schließlich liefert der Löschvorgang zwei kleinere Diagramme.

![](./images/guardrails/hub-and-spoke-result.png)

>[!ENDTABS]

## Nächste Schritte

Weitere Informationen über [!DNL Identity Service] finden Sie in der folgenden Dokumentation:

* [[!DNL Identity Service] – Übersicht](home.md)
* [Identitätsdiagramm-Viewer](features/identity-graph-viewer.md)

In der folgenden Dokumentation finden Sie weitere Informationen zu anderen Experience Platform-Services-Leitplanken, zu End-to-End-Latenzinformationen und Lizenzinformationen aus Real-Time CDP-Produktbeschreibungsdokumenten:

* [Real-Time CDP-Leitplanken](/help/rtcdp/guardrails/overview.md)
* [End-to-End-Latenzdiagramme](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=de#end-to-end-latency-diagrams) für verschiedene Experience Platform-Services.
* [Real-Time Customer Data Platform (B2C Edition - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
