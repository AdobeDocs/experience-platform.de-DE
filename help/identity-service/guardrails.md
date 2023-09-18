---
keywords: Experience Platform; Identität; Identitätsdienst; Fehlerbehebung; Limits; Richtlinien; Einschränkung
title: Limits für Identity Service
description: Dieses Dokument enthält Informationen zu Verwendung und Quotenbegrenzungen für Identity Service-Daten, die Sie bei der Optimierung Ihrer Verwendung des Identitätsdiagramms unterstützen.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: a9b5ab28d00941b7531729653eb630a61b5446fc
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 57%

---

# Leitplanken für [!DNL Identity Service]Daten

Dieses Dokument enthält Informationen über die Verwendung und die Ratenbeschränkungen für [!DNL Identity Service]-Daten, um Ihnen bei der optimalen Nutzung des Identitätsdiagramms zu helfen. Bei der Überprüfung der folgenden Leitplanken wird davon ausgegangen, dass Sie die Daten korrekt modelliert haben. Wenden Sie sich bei Fragen zum Modellieren Ihrer Daten an Ihren Kundenbetreuer.

## Erste Schritte

Die folgenden Experience Platform-Dienste sind an der Modellierung von Identitätsdaten beteiligt:

* [Identitäten](home.md): Überbrücken von Identitäten aus unterschiedlichen Datenquellen, während sie in Platform aufgenommen werden.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Erstellen einheitlicher Verbraucherprofile anhand von Daten aus mehreren Quellen.

## Datenmodellbeschränkungen

Die folgenden Tabellen enthalten Anleitungen zu Leitlinien für statische Beschränkungen sowie zu berücksichtigende Validierungsregeln für Identity-Namespaces.

### Statische Beschränkungen

In der folgenden Tabelle sind statische Beschränkungen für Identitätsdaten aufgeführt.

| Leitplanke | Limit | Anmerkungen |
| --- | --- | --- |
| (Aktuelles Verhalten) Anzahl der Identitäten in einem Diagramm | 150 | Die Beschränkung wird auf Sandbox-Ebene angewendet. Sobald die Anzahl der Identitäten 150 oder mehr erreicht hat, werden keine neuen Identitäten hinzugefügt und das Identitätsdiagramm wird nicht aktualisiert. Diagramme können Identitäten größer als 150 anzeigen, wenn sie eine oder mehrere Diagramme mit weniger als 150 Identitäten verbinden. **Hinweis**: Die maximale Anzahl von Identitäten in einem Identitätsdiagramm **für jedes einzelne zusammengeführte Profil** as 50. Zusammengeführte Profile, die auf Identitätsdiagrammen mit mehr als 50 Identitäten basieren, werden aus dem Echtzeit-Kundenprofil ausgeschlossen. Weitere Informationen finden Sie im Handbuch unter [Limits für Profildaten](../profile/guardrails.md). |
| (Bevorstehendes Verhalten) Anzahl der Identitäten in einem Diagramm [!BADGE Beta]{type=Informative} | 50 | Wenn ein Diagramm mit 50 verknüpften Identitäten aktualisiert wird, wendet Identity Service einen „First-in-First-out“-Mechanismus an und löscht die älteste Identität, um Platz für die neueste Identität zu schaffen. Das Löschen basiert auf Identitätstyp und Zeitstempel. Die Beschränkung wird auf Sandbox-Ebene angewendet. Weitere Informationen finden Sie im Abschnitt unter [die Löschlogik verstehen](#deletion-logic). |
| Anzahl der Identitäten in einem XDM-Eintrag | 20 | Die erforderliche Mindestanzahl von XDM-Einträgen beträgt zwei. |
| Anzahl der benutzerdefinierten Namespaces | Keine | Die Anzahl der benutzerdefinierten Namespaces, die Sie erstellen können, ist unbegrenzt. |
| Anzahl der Zeichen für einen Namespace-Anzeigenamen oder ein Identitätssymbol | Keine | Die Anzahl der Zeichen eines Namespace-Anzeigenamens oder Identitätssymbols ist unbegrenzt. |

### Überprüfung des Identitätswerts

In der folgenden Tabelle sind die vorhandenen Regeln aufgeführt, die Sie befolgen müssen, um eine erfolgreiche Überprüfung Ihres Identitätswerts sicherzustellen.

| Namespace | Validierungsregel | Systemverhalten bei Verletzung einer Regel |
| --- | --- | --- |
| ECID | <ul><li>Der Identitätswert einer ECID muss genau 38 Zeichen betragen.</li><li>Der Identitätswert einer ECID darf nur aus Zahlen bestehen.</li></ul> | <ul><li>Wenn der Identitätswert der ECID nicht genau 38 Zeichen beträgt, wird der Eintrag übersprungen.</li><li>Wenn der Identitätswert der ECID nicht-numerische Zeichen enthält, wird der Eintrag übersprungen.</li></ul> |
| Nicht-ECID | Der Identitätswert darf 1024 Zeichen nicht überschreiten. | Wenn der Identitätswert 1024 Zeichen überschreitet, wird der Eintrag übersprungen. |

### Aufnahme von Identity-Namespaces

Ab dem 31. März 2023 blockiert Identity Service die Aufnahme der Adobe Analytics ID (AAID) für neue Kundinnen und Kunden. Diese Identität wird normalerweise über die [Adobe Analytics-Quelle](../sources/connectors/adobe-applications/analytics.md) und die [Adobe Audience Manager-Quelle](../sources//connectors/adobe-applications/audience-manager.md) aufgenommen und ist überflüssig, da die ECID denselben Webbrowser darstellt. Wenn Sie diese Standardkonfiguration ändern möchten, wenden Sie sich an Ihr Adobe-Accountteam.

## [!BADGE Beta]{type=Informative} Grundlegendes zur Löschungslogik, wenn ein Identitätsdiagramm bei Erreichen der Kapazität aktualisiert wird {#deletion-logic}

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

>[!BEGINSHADEBOX]

**Eine visuelle Darstellung der Löschlogik**

![Ein Beispiel für die älteste Identität, die gelöscht wird, um die neueste Identität aufzunehmen](./images/graph-limits-v3.png)

*Diagrammnotizen:*

* `t` = Zeitstempel.
* Der Wert eines Zeitstempels entspricht der Neuigkeit einer bestimmten Identität. Beispiel: `t1` stellt die erste verknüpfte Identität (älteste) dar und `t51` würde die neueste verknüpfte Identität darstellen.

In diesem Beispiel löscht Identity Service zuerst die vorhandene Identität mit dem ältesten Zeitstempel, bevor das Diagramm auf der linken Seite mit einer neuen Identität aktualisiert werden kann. Da die älteste Identität jedoch eine Geräte-ID ist, überspringt Identity Service diese Identität, bis er zum Namespace mit einem Typ gelangt, der höher in der Liste mit Löschprioritäten ist, was in diesem Fall `ecid-3` ist. Sobald die älteste Identität mit einer höheren Löschpriorität entfernt wurde, wird das Diagramm mit einer neuen Verknüpfung, `ecid-51`, aktualisiert.

* In dem seltenen Fall, dass es zwei Identitäten mit demselben Zeitstempel und Identitätstyp gibt, sortiert Identity Service die IDs basierend auf [XID](./api/list-native-id.md) und führen Löschung durch.

>[!ENDSHADEBOX]

### Auswirkungen auf die Implementierung

In den folgenden Abschnitten werden die Implikationen erläutert, die die Löschlogik für Identity Service, Echtzeit-Kundenprofil und WebSDK hat.

#### Identity Service: Änderung des benutzerdefinierten Namespace-Identitätstyps

Wenden Sie sich an Ihr Adobe-Account-Team, um eine Änderung des Identitätstyps anzufordern, wenn Ihre Produktions-Sandbox Folgendes enthält:

* Ein benutzerdefinierter Namespace, bei dem die Personen-IDs (z. B. CRM-IDs) als Cookie-/Geräte-Identitätstyp konfiguriert sind.
* Ein benutzerdefinierter Namespace, bei dem Cookie-/Geräte-IDs als geräteübergreifender Identitätstyp konfiguriert sind.

Sobald diese Funktion verfügbar ist, werden Diagramme, die die Grenze von 50 Identitäten überschreiten, auf bis zu 50 Identitäten reduziert. Bei Real-Time CDP B2C Edition konnte dies zu einem minimalen Anstieg der Anzahl der Profile führen, die sich für eine Zielgruppe qualifizieren, da diese Profile zuvor in Segmentierung und Aktivierung ignoriert wurden.

#### Echtzeit-Kundenprofil: Pseudonyme Profileinrichtung

Das Löschen erfolgt nur für Daten im Identity Service, nicht aber für Echtzeit-Kundenprofile.

* Dieses Verhalten könnte folglich mehr Profile mit einer einzigen ECID erstellen, da die ECID nicht mehr Teil des Identitätsdiagramms ist.
* Damit Sie sich innerhalb Ihrer adressierbaren Zielgruppen-Berechtigungsnummern befinden, sollten Sie die Option [pseudonyme Profildaten ablaufen](../profile/pseudonymous-profiles.md) , um Ihre alten Profile zu löschen.

#### Echtzeit-Kundenprofil und WebSDK: Primäres Löschen von Identitäten

Wenn Sie Ihre authentifizierten Ereignisse mit der CRM-ID vergleichen möchten, sollten Sie Ihre primären IDs von ECID in CRM-ID ändern. In den folgenden Dokumenten finden Sie Anweisungen zur Implementierung dieser Änderung:

* [Identitätszuordnung für Experience Platform-Tags konfigurieren](../tags/extensions/client/web-sdk/data-element-types.md#identity-map).
* [Identitätsdaten im Experience Platform Web SDK](../edge/identity/overview.md#using-identitymap)

## Nächste Schritte

Weitere Informationen über [!DNL Identity Service] finden Sie in der folgenden Dokumentation:

* [[!DNL Identity Service] – Übersicht](home.md)
* [Identitätsdiagramm-Viewer](ui/identity-graph-viewer.md)
