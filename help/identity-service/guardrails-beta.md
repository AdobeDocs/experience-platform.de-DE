---
title: Limits für Identity Service (mit Löschlogik)
description: Erfahren Sie mehr über Limits für Identity Service.
hide: true
hidefromtoc: true
source-git-commit: db8edbbc3ea5d8fcec3de95b9a37387bea493693
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 9%

---

# Limits [!DNL Identity Service] Daten (mit Löschlogik)

Dieses Dokument enthält Informationen zu Verwendung und Quotenbegrenzungen für [!DNL Identity Service] Daten, die Ihnen bei der Optimierung Ihrer Verwendung des Identitätsdiagramms helfen. Bei der Überprüfung der folgenden Leitplanken wird davon ausgegangen, dass Sie die Daten korrekt modelliert haben. Wenden Sie sich bei Fragen zum Modellieren Ihrer Daten an Ihren Kundenbetreuer.

## Erste Schritte

Die folgenden Experience Platform-Dienste sind an der Modellierung von Identitätsdaten beteiligt:

* [Identitäten](home.md): Überbrücken von Identitäten aus unterschiedlichen Datenquellen, während sie in Platform aufgenommen werden.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Erstellen einheitlicher Verbraucherprofile anhand von Daten aus mehreren Quellen.

## Datenmodellbeschränkungen

Die folgenden Tabellen enthalten Anleitungen zu Limits für statische Limits sowie zu berücksichtigende Validierungsregeln für Identitäts-Namespaces.

### Statische Beschränkungen

In der folgenden Tabelle sind statische Beschränkungen für Identitätsdaten aufgeführt.

| Leitplanke | Limit | Anmerkungen |
| --- | --- | --- |
| Anzahl der Identitäten in einem Diagramm [!BADGE Beta]{type=Informative} | 50 | Wenn ein Diagramm mit 50 verknüpften Identitäten aktualisiert wird, wendet Identity Service einen &quot;First-in-First-out&quot;-Mechanismus an und löscht die älteste Identität, um Platz für die neueste Identität zu schaffen. Das Löschen basiert auf Identitätstyp und Zeitstempel. Die Begrenzung wird auf Sandbox-Ebene angewendet. Lesen Sie die [Anhang](#appendix) für weitere Informationen dazu, wie Identity Service Identitäten löscht, sobald die Grenze erreicht ist. |
| Anzahl der Identitäten in einem XDM-Datensatz | 20 | Die erforderliche Mindestanzahl von XDM-Datensätzen beträgt zwei. |
| Anzahl der benutzerdefinierten Namespaces | Keine | Die Anzahl der benutzerdefinierten Namespaces, die Sie erstellen können, ist unbegrenzt. |
| Anzahl der Diagramme | Keine | Die Anzahl der Identitätsdiagramme, die Sie erstellen können, ist unbegrenzt. |
| Anzahl der Zeichen für einen Namespace-Anzeigenamen oder ein Identitätssymbol | Keine | Die Anzahl der Zeichen eines Namespace-Anzeigenamens oder Identitätssymbols ist unbegrenzt. |

### Überprüfung des Identitätswerts

In der folgenden Tabelle sind die vorhandenen Regeln aufgeführt, die Sie befolgen müssen, um eine erfolgreiche Überprüfung Ihres Identitätswerts sicherzustellen.

| Namespace | Validierungsregel | Systemverhalten bei Verletzung einer Regel |
| --- | --- | --- |
| ECID | <ul><li>Der Identitätswert einer ECID muss genau 38 Zeichen betragen.</li><li>Der Identitätswert einer ECID darf nur aus Zahlen bestehen.</li></ul> | <ul><li>Wenn der Identitätswert der ECID nicht genau 38 Zeichen beträgt, wird der Datensatz übersprungen.</li><li>Wenn der Identitätswert der ECID nicht numerische Zeichen enthält, wird der Datensatz übersprungen.</li></ul> |
| Nicht ECID | Der Identitätswert darf 1024 Zeichen nicht überschreiten. | Wenn der Identitätswert 1024 Zeichen überschreitet, wird der Datensatz übersprungen. |

### Erfassung von Identitäts-Namespaces

Ab dem 31. März 2023 blockiert Identity Service die Erfassung von Adobe Analytics ID (AAID) für neue Kunden. Diese Identität wird normalerweise über die [Adobe Analytics-Quelle](../sources/connectors/adobe-applications/analytics.md) und [Adobe Audience Manager-Quelle](../sources//connectors/adobe-applications/audience-manager.md) und ist redundant, da die ECID denselben Webbrowser darstellt. Wenn Sie diese Standardkonfiguration ändern möchten, wenden Sie sich an Ihr Adobe-Account-Team.

## Nächste Schritte

Weitere Informationen zu [!DNL Identity Service]:

* [[!DNL Identity Service] – Übersicht](home.md)
* [Identitätsdiagramm-Viewer](ui/identity-graph-viewer.md)

## Anhang {#appendix}

Der folgende Abschnitt enthält zusätzliche Informationen zu Limits für Identity Service.

### [!BADGE Beta]{type=Informative} Die Löschlogik bei der Aktualisierung eines Identitätsdiagramms bei Kapazität {#deletion-logic}

Wenn ein vollständiges Identitätsdiagramm aktualisiert wird, löscht Identity Service die älteste Identität im Diagramm, bevor die neueste Identität hinzugefügt wird. Dies dient der Gewährleistung der Genauigkeit und Relevanz von Identitätsdaten. Dieser Löschvorgang folgt zwei Hauptregeln:

#### Regel 1 Löschung wird basierend auf dem Identitätstyp eines Namespace priorisiert

Die Löschpriorität lautet wie folgt:

1. Cookie-ID
2. Geräte-ID
3. Geräteübergreifende ID, E-Mail und Telefon

#### Regel 2 Löschung basiert auf dem Zeitstempel, der in der Identität gespeichert ist.

Jede in einem Diagramm verknüpfte Identität hat einen eigenen Zeitstempel. Wenn ein vollständiges Diagramm aktualisiert wird, löscht Identity Service die Identität mit dem ältesten Zeitstempel.

Wenn ein vollständiges Diagramm mit einer neuen Identität aktualisiert wird, bestimmen diese beiden Regeln gemeinsam, welche ältere Identität gelöscht wird. Identity Service löscht zunächst die älteste Cookie-ID, dann die älteste Geräte-ID und schließlich die älteste geräteübergreifende ID/E-Mail/Telefon.

>[!NOTE]
>
>Wenn die zu löschende Identität mit mehreren anderen Identitäten im Diagramm verknüpft ist, werden auch die Links, die diese Identität verbinden, gelöscht.

Im folgenden Beispiel muss Identity Service zuerst die vorhandene Identität mit dem ältesten Zeitstempel löschen, bevor das Diagramm auf der linken Seite mit einer neuen Identität aktualisiert werden kann. Da die älteste Identität jedoch eine Geräte-ID ist, überspringt Identity Service diese Identität, bis sie zum Namespace mit einem Typ gelangt, der höher in der Liste mit Löschprioritäten ist, was in diesem Fall der Fall ist `ecid-3`. Sobald die älteste Identität mit einem höheren Löschprioritätstyp entfernt wurde, wird das Diagramm mit einem neuen Link aktualisiert. `ecid-51`.

>[!NOTE]
>
>In dem seltenen Fall, dass es zwei Identitäten mit demselben Zeitstempel und Identitätstyp gibt, sortiert Identity Service die IDs basierend auf XID und führt das Löschen durch.

![Ein Beispiel für die älteste Identität, die gelöscht wird, um die neueste Identität aufzunehmen](./images/graph-limits-v3.png)