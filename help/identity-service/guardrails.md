---
keywords: Experience Platform; Identität; Identitätsdienst; Fehlerbehebung; Limits; Richtlinien; Einschränkung
title: Limits für Identity Service
description: Dieses Dokument enthält Informationen zu Verwendung und Quotenbegrenzungen für Identity Service-Daten, die Sie bei der Optimierung Ihrer Verwendung des Identitätsdiagramms unterstützen.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: e6d0f0d0bc3de2f6da4e4269811d254db4fa3303
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 11%

---

# Limits [!DNL Identity Service] data

Dieses Dokument enthält Informationen zu Verwendung und Quotenbegrenzungen für [!DNL Identity Service] Daten, die Ihnen bei der Optimierung Ihrer Verwendung des Identitätsdiagramms helfen. Bei der Überprüfung der folgenden Leitlinien wird davon ausgegangen, dass Sie die Daten korrekt modelliert haben. Wenden Sie sich bei Fragen zum Modellieren Ihrer Daten an Ihren Kundenbetreuer.

## Erste Schritte

Die folgenden Experience Platform-Dienste sind an der Modellierung von Identitätsdaten beteiligt:

* [Identitäten](home.md): Bridge-Identitäten aus unterschiedlichen Datenquellen, während sie in Platform erfasst werden.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Erstellen Sie einheitliche Verbraucherprofile anhand von Daten aus mehreren Quellen.

## Datenmodellbeschränkungen

Die folgenden Tabellen enthalten Anleitungen zu Limits für statische Limits sowie zu berücksichtigende Validierungsregeln für Identitäts-Namespaces.

### Statische Beschränkungen

In der folgenden Tabelle sind statische Beschränkungen für Identitätsdaten aufgeführt.

| Beschränkung | Limit | Anmerkungen |
| --- | --- | --- |
| Anzahl der Identitäten in einem Diagramm | 150 | Die Begrenzung wird auf Sandbox-Ebene angewendet. Das Identitätsdiagramm wird nach Erreichen des Grenzwerts nicht mehr aktualisiert. |
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

Ab dem 31. Januar 2023 blockiert Identity Service die Erfassung von Adobe Analytics ID (AAID) für neue Kunden. Diese Identität wird normalerweise über die [Adobe Analytics-Quelle](../sources/connectors/adobe-applications/analytics.md) und [Adobe Audience Manager-Quelle](../sources//connectors/adobe-applications/audience-manager.md) und ist redundant, da die ECID denselben Webbrowser darstellt. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie diese Standardkonfiguration ändern möchten.

## Nächste Schritte

Weitere Informationen zu [!DNL Identity Service]:

* [[!DNL Identity Service] – Übersicht](home.md)
* [Identitätsdiagramm-Viewer](ui/identity-graph-viewer.md)
