---
title: Real-Time CDP-Schutzmechanismen
description: Erfahren Sie mehr über die Datensicherungen in den verschiedenen Diensten und Bereichen von Real-Time CDP.
feature: Guardrails, Data Management, Data Ingestion, Data Export
exl-id: 377499b4-5707-4d50-94e3-02f88ad5bf2c
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 7%

---

# Real-Time CDP-Schutzmechanismen

Limits sind Schwellenwerte, die die Datennutzung und Systemnutzung, Leistungsoptimierung und Vermeidung von Fehlern oder unerwarteten Ergebnissen in Real-Time CDP unterstützen. Leitplanken können sich auf Ihre Nutzung oder Verwendung von Daten und Verarbeitung im Zusammenhang mit Ihren Lizenzierungsberechtigungen beziehen.

>[!IMPORTANT]
>
>Überprüfen Sie Ihre Lizenzberechtigungen in Ihrem Kundenauftrag und den entsprechenden [Produktbeschreibung](https://helpx.adobe.com/de/legal/product-descriptions.html) über die tatsächlichen Nutzungsbeschränkungen zusätzlich zu dieser Limits-Seite.

Beginnen Sie hier und folgen Sie den unten stehenden Links, um alle Limits über die verschiedenen Dienste und Bereiche von Real-Time CDP hinweg zu verstehen:

* [Schutzmaßnahmen bei der Datenaufnahme](/help/ingestion/guardrails.md)
* [Limits für die [!DNL Edge Network Server API]](/help/server-api/guardrails.md)
* [Limits [!DNL Real-Time Customer Profile] Daten und Segmentierung](/help/profile/guardrails.md)
* [Limits [!DNL Identity Service] data](/help/identity-service/guardrails.md)
* [Limits [!DNL Query Service]](/help/query-service/guardrails.md)
* [Limits für die Datenaktivierung über Ziele](/help/destinations/guardrails.md)
* [Limits für Real-Time CDP B2B](/help/rtcdp/b2b-guardrails.md)

>[!TIP]
>
>Außerdem Besuch [digitale Erlebnispläne](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html) für weitere Informationen wie [End-to-End-Latenzdiagramme](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) für verschiedene Experience Platform-Dienste.

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

## Schutzmechanismen für andere Experience Platform-Anwendungen  {#guardrails-other-aep-apps}

Ähnliche Schutzmechanismen gibt es auch für andere Experience Platform-Anwendungen. Weitere Informationen finden Sie unter den folgenden Links:

* [Limits in Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=en)
* [Customer Journey Analytics-Limits](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html)

## Nächste Schritte

Nach dem Verständnis der Limits, die für verschiedene Bereiche und Dienste von Real-Time CDP gelten, können Sie mit einem [Beispielanwendungsfall einer Real-Time CDP-Implementierung](/help/rtcdp/get-started.md).
