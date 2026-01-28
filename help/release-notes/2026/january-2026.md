---
title: Adobe Experience Platform – Versionshinweise Januar 2026
description: Versionshinweise Januar 2026 für Adobe Experience Platform.
source-git-commit: 9a3fbe281195041cf7444c5b6ec185395ff5ad23
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 16%

---


# Adobe Experience Platform – Versionshinweise

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Versionsdatum: Mittwoch, 27. Januar 2026**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

<!-- - [Agent Orchestrator](#agent-orchestrator) -->

- [Ziele](#destinations)
- [Echtzeit-Kundenprofil](#real-time-customer-profile)
- [Schemata](#schemas)
- [Segmentierungs-Service](#segmentation-service)
- [Quellen](#sources)

<!-- ## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator enables you to build and deploy AI-powered agents that can automate workflows and interact with customers across multiple channels.

**New or updated features**

| Feature | Description |
| --- | --- |
| Trial motion for Adobe Experience Platform Agents | **Select customers now have access to Adobe Experience Platform Agents for a complimentary trial**, enabling them to explore and interact with these Agents through the AI Assistant interface powered by Adobe Experience Platform Agent Orchestrator. The trial offers hands-on experience with AI Agents that operate within the context of customers' existing Experience Cloud products and environments, allowing teams to evaluate value before committing to a full purchase. Adobe Experience Platform Agents are guided by user input and oversight and respect existing product-level access controls, ensuring users can only perform actions or view data for which they are authorized within the underlying Experience Cloud applications.|

{style="table-layout:auto"}

For more information, see the [Agent Orchestrator documentation](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator). -->

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| --- | --- |
| Level Destination Connector jetzt verfügbar | Das [!DNL Kevel] Streaming-Ziel für Adobe Experience Platform ermöglicht es Kunden, Adobe-Zielgruppen direkt in die UserDB- und Segment Management-APIs von [!DNL Kevel] zu aktivieren, um das Targeting in Echtzeit zur Zeit der Anzeigenentscheidung zu unterstützen. [[!DNL Kevel]](https://www.kevel.com/) bietet die KI-fähige Technologie und fachkundige Anleitung, die innovativen Commerce-Führungskräften dabei helfen, in Einzelhandelsmedien zu starten, zu skalieren und erfolgreich zu sein. Die Retail Media Cloud von [!DNL Kevel] ermöglicht zielgerichtete, zuordenbare, anpassbare Anzeigenformate für Onsite- und Offsite-Werbung. |
| Index Exchange-Ziel-Connector jetzt verfügbar | Verwenden Sie diesen Ziel-Connector, um Zielgruppensegmente aus Adobe Experience Platform direkt in die programmgesteuerte Werbeplattform von [!DNL Index Exchange] zu exportieren. [!DNL Index] ist eine globale Plattform für Werbeangebote, mit der Medieninhaber den Wert ihrer Inhalte auf jedem Bildschirm maximieren können. Mit über 20 Jahren Branchenführerschaft verbindet [!DNL Index] die weltweit größten Marken mit erstklassigen Experience Makers, um hochwertige Kundenerlebnisse zu schaffen. |
| Unterstützung regionaler Endpunkte für Braze-Verbindungen | Alle [regionsspezifischen Endpunkte](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) die von [!DNL Braze] unterstützt werden, sind jetzt während des Zielkonfigurationsflusses zur Auswahl verfügbar. Fragen Sie Ihren [!DNL Braze], welche Endpunktinstanz Sie verwenden sollten. |
| Wöchentliche und monatliche Planungsunterstützung für [Liveramp Onboarding](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling) | Sie können jetzt wöchentliche und monatliche Exportpläne für das Liveramp-Onboarding-Ziel konfigurieren. <br> Diese Version wird schrittweise eingeführt und wird am 30. Januar abgeschlossen sein. |
| Verbessertes Aktivierungserlebnis für [The Trade Desk](../../destinations/catalog/advertising/tradedesk.md)- und [Microsoft Bing](../../destinations/catalog/advertising/bing.md)-Ziele | Die Trade Desk- und Microsoft Bing-Ziele enthalten jetzt vordefinierte obligatorische Zuordnungen für ein optimiertes Aktivierungserlebnis.  <br> Diese Version wird schrittweise eingeführt und wird am 30. Januar abgeschlossen sein. |

<!-- |AES256 encryption support for [Amazon S3](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) destinations | You can now configure AES256 encryption for your Amazon S3 exports. Two options are available: <br><br>**[!UICONTROL Default]**: If you don't have any custom policies applied on your buckets, data will be encrypted at rest when it lands in S3 with the AES256 algorithm. However, if you have custom policies applied, Experience Platform will respect those policies and Amazon S3 will continue to apply whichever custom encryption policies you have configured.<br><br>**[!UICONTROL SSE-S3/AES256]**: Experience Platform adds the `s3:x-amz-server-side-encryption": "AES256` header in the export and data will be encrypted at rest when it lands in S3 with the AES256 algorithm. | -->


**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Die Limits für Leitplanken für [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md)-Ziele wurden aktualisiert | Die maximale Anzahl von Zielgruppen, die einem einzelnen Adobe Target-Ziel zugeordnet werden können, wurde von 50 auf 250 erhöht. Dadurch wird Adobe Target an das standardmäßige Zielgruppenlimit für andere Ziele angepasst, was eine größere Flexibilität für Zielgruppenaktivierungs-Workflows bietet. Sie können jetzt mehr Zielgruppen für Adobe Target-Ziele aktivieren, ohne mehrere Datenflüsse erstellen zu müssen. |
| [Ziele bearbeiten](/help/destinations/ui/edit-destination.md) und [Marketing-Aktionen bearbeiten](/help/destinations/ui/edit-activation.md#edit-marketing-actions) allgemeine Verfügbarkeit | Die Option zum Bearbeiten von Zielen und Marketing-Aktionen steht jetzt allen Benutzenden zur Verfügung. |
| Anzeigenamen von Feldern im Zuordnungsschritt umschalten [Schritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) | Beim Zuordnen von Schemafeldern zu einem Ziel können Sie jetzt zwischen der Anzeige des vollständigen XDM-Feldnamens und der Anzeige nur des Anzeigenamens umschalten. <br> ![Bildschirmaufzeichnung mit Umschalten des Anzeigenamens.](/help/release-notes/2026/assets/january/show-display-names.gif) |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Ziele - Übersicht](../../destinations/home.md).

## Echtzeit-Kundenprofil {#real-time-customer-profile}

Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen sowie anderen Kanälen miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige, Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [Streaming-Kapazität](/help/landing/license-usage-and-guardrails/capacity.md) Durchsetzung | Experience Platform erzwingt jetzt Streaming-Durchsatzkapazitäten für das Echtzeit-Kundenprofil und Identity Service. Wenn Kunden ihre vertraglich vereinbarte Streaming-Kapazität überschreiten, werden Daten in eine Warteschlange gestellt und in einer First-in-First-out-Weise verarbeitet. Dies stellt eine vorhersehbare Systemleistung sicher und verhindert, dass Kapazitätsverletzungen die Datenaufnahmequalität beeinträchtigen. Wichtige Hinweise: <ul><li>Streaming-Upserts sind im Data Lake bei Kapazitätsüberschreitung nicht verfügbar</li><li>Diese Durchsetzung gilt nicht für Kunden mit Adobe Journey Optimizer-Lizenzen</li><li>Die in die Warteschlange gestellten Daten werden sequenziell verarbeitet, sobald Kapazität verfügbar ist.</li></ul> Weitere Informationen finden Sie unter [Kapazitätsübersicht](/help/landing/license-usage-and-guardrails/capacity.md). |
| Einstellung der Entitätssuche | Die Verwendung der Entitätssuch-API für Erlebnisereignisse wird jetzt für alle Kunden von Real-Time CDP Prime nicht mehr unterstützt. Diese Einstellung hilft bei der Anpassung von Real-Time CDP an die Lizenzierungsfunktion. Kunden von Real-Time CDP Ultimate, die diese Funktion verwenden möchten, können sich an die Kundenunterstützung von Adobe wenden, um diese Funktion erneut zu aktivieren.  Weitere Informationen finden Sie im [Entitäten-API-Handbuch](/help/profile/api/entities.md). |
| Überwachen des Status des Profilaufnahmevorgangs | Sie können jetzt den Fortschrittsprozentsatz auf Auftragsebene für die Datenflussausführungen zur Batch-Profilaufnahme überwachen. Diese Funktion bietet Echtzeiteinblicke in den aktuellen Fortschritt von Batch-Erfassungsvorgängen, einschließlich wichtiger Checkpoints, die anzeigen, ob die Aufnahme für die Kundensegmentierung und die Adobe Journey Optimizer-Suche bereit ist. Bei großen Aufnahmen, deren Verarbeitung mehrere Stunden dauern kann, hilft Ihnen diese Fortschrittstransparenz zu verstehen, ob der Vorgang normal verläuft oder auf Probleme stößt, wodurch die Unsicherheit bei der Datenverarbeitung reduziert wird.Weitere Informationen finden Sie im [Handbuch zum Überwachen von Profilen](/help/dataflows/ui/monitor-profiles.md). |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [[!DNL Real-Time Customer Profile] Übersicht](../../profile/home.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Teilmenge von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Zielgruppen können auf Datensatzdaten (z. B. demografische Informationen) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Aktualisierung der Gültigkeit externer Zielgruppendaten | Externe Zielgruppen (z. B. CSV-Uploads) unterstützen jetzt eine Funktion zum Erzwingen einer Aktualisierung der Datenablaufeinstellungen. Mit dieser Funktion können Benutzer den Ablauf von Daten für externe Zielgruppen manuell aktualisieren, was eine bessere Kontrolle über die Verwaltung des Zielgruppen-Lebenszyklus ermöglicht. Dies ist besonders nützlich für Zielgruppen, die über den ursprünglichen Datenablaufzeitraum hinaus bestehen bleiben müssen oder eine Reaktivierung benötigen, ohne die Daten erneut hochzuladen. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt [Zielgruppenportal - Übersicht](../../segmentation/ui/audience-portal.md#audience-summary). |

Weitere Informationen finden Sie in der [[!DNL Segmentation Service] Übersicht](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Quellen**

| Quelle | Beschreibung |
| --- | --- |
| [[!DNL Oracle Eloqua]](/help/sources/connectors/marketing-automation/eloqua.md) V2-Quelle | Ein neuer [!DNL Oracle Eloqua]-Quell-Connector ist jetzt verfügbar, der den [veralteten Connector“ &#x200B;](/help/sources/connectors/marketing-automation/oracle-eloqua.md). Dieser aktualisierte Connector bietet erweiterte Funktionen und eine höhere Zuverlässigkeit für die Aufnahme von Daten aus [!DNL Oracle Eloqua] in Experience Platform. Kunden, die den vorhandenen Connector verwenden, sollten zur neuen Implementierung migrieren, da bestehende Verbindungen nicht mehr funktionieren. Der neue Connector unterstützt alle Einrichtungs- und Konfigurationsschritte, die für die Verbindung mit [!DNL Oracle Eloqua] und die Aufnahme von Daten zur Marketing-Automatisierung erforderlich sind. |
| [[!DNL Salesforce Marketing Cloud]](/help/sources/connectors/marketing-automation/sfmc.md) V2-Quelle | Ein neuer [!DNL Salesforce Marketing Cloud]-Quell-Connector ist jetzt verfügbar, der den [veralteten Connector“ &#x200B;](/help/sources/connectors/marketing-automation/salesforce-marketing-cloud.md). Dieser aktualisierte Connector bietet eine verbesserte Leistung und zusätzliche Funktionen für die Aufnahme von Daten aus [!DNL Salesforce Marketing Cloud] in Experience Platform. Kunden, die den vorhandenen Connector verwenden, sollten zur neuen Implementierung wechseln. Der neue Connector enthält umfassende Einrichtungsanweisungen für die Verbindung mit [!DNL Salesforce Marketing Cloud] und die Aufnahme von Daten zur Marketing-Automatisierung. |

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).

