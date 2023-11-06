---
title: Real-Time CDP-Schutzmechanismen
description: Erfahren Sie mehr über die Datensicherungen in den verschiedenen Diensten und Bereichen von Real-Time CDP.
source-git-commit: c6daa645743331ba6fdf8f79e432ae150ee1ff9e
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 11%

---

# Real-Time CDP-Schutzmechanismen

Limits sind Schwellenwerte, die die Datennutzung und Systemnutzung, Leistungsoptimierung und Vermeidung von Fehlern oder unerwarteten Ergebnissen in Real-Time CDP unterstützen. Leitplanken können sich auf Ihre Nutzung oder Verwendung von Daten und Verarbeitung im Zusammenhang mit Ihren Lizenzierungsberechtigungen beziehen.

Beginnen Sie hier und folgen Sie den unten stehenden Links, um alle Limits über die verschiedenen Dienste und Bereiche von Real-Time CDP hinweg zu verstehen:

* [Schutzmaßnahmen bei der Datenaufnahme](/help/ingestion/guardrails.md)
* [Limits für die [!DNL Edge Network Server API]](/help/server-api/guardrails.md)
* [Limits [!DNL Real-Time Customer Profile] Daten und Segmentierung](/help/profile/guardrails.md)
* [Leitplanken für  [!DNL Identity Service] Daten](/help/identity-service/guardrails.md)
* [Limits [!DNL Query Service]](/help/query-service/guardrails.md)
* [Limits für die Datenaktivierung über Ziele](/help/destinations/guardrails.md)

>[!TIP]
>
>Weitere Informationen finden Sie unter [diese Seite](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html) für Informationen zu Limits für andere Experience Platform-Apps, z. B. [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=de) und [Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics.html?lang=de), und [End-to-End-Latenzdiagramme](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) für verschiedene Experience Platform-Dienste.

## Schutzarten {#guardrail-types}

Beachten Sie, dass die beiden Schutzmechanismen für alle Real-Time CDP-Bereiche und -Dienste gelten:

| Schutztyp | Beschreibung |
|----------|---------|
| **Leistungsgarantie (weiche Begrenzung)** | Leistungsgarantien sind Nutzungsbeschränkungen, die sich auf das Scoping Ihrer Anwendungsfälle beziehen. Wenn Sie die Leistungsgarantien überschreiten, kann es zu Leistungseinbußen und Latenzzeiten kommen. Adobe ist nicht für eine solche Leistungsbeeinträchtigung verantwortlich. Kunden, die eine Leistungsgarantie konsequent überschreiten, können zusätzliche Kapazität lizenzieren, um Leistungsbeeinträchtigungen zu vermeiden. |
| **Systemerzwungene Limits (Hard Limit)** | Systemerzwungene Limits werden von der Real-Time CDP-Benutzeroberfläche oder -API erzwungen. Dies sind Beschränkungen, die Sie nicht überschreiten können, da die Benutzeroberfläche und API Sie davon abhält oder einen Fehler zurückgibt. |

{style="table-layout:auto"}

## Lizenzierung und Berechtigungsinformationen für Real-Time CDP {#product-descriptions}

Darüber hinaus finden Sie in den folgenden Produktbeschreibungslinks Lizenzierungs- und Berechtigungsinformationen, die auf der von Ihnen erworbenen Real-Time CDP-Bearbeitung und -Ebene basieren:

* [Alle Produktbeschreibungen der Adobe](https://helpx.adobe.com/de/legal/product-descriptions.html)
* [Real-time Customer Data Platform (B2C Edition - Prime und Ultimate Packages)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P Edition - Prime und Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B Edition - Prime und Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

## Nächste Schritte

Nach dem Verständnis der Limits, die für verschiedene Bereiche und Dienste von Real-Time CDP gelten, können Sie mit einem [Beispielanwendungsfall einer Real-Time CDP-Implementierung](/help/rtcdp/get-started.md).
