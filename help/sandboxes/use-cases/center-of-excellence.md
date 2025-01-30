---
title: Aktivieren eines Kompetenzzentrums mithilfe von Sandbox-Tools
description: Aktivieren Sie mithilfe von Sandbox-Tools ein Kompetenzzentrum, indem Sie ein „goldenes Sandbox“-Paket erstellen, um Best Practices für mehrere Sandboxes zu standardisieren.
exl-id: 6f242ad5-bb02-4a6d-b255-d196dd5fe4b8
source-git-commit: d4df5606228347b5fb69fdaa24c637c329099895
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 7%

---

# Aktivieren eines Kompetenzzentrums mithilfe von Sandbox-Tools

Aktivieren Sie mithilfe von Sandbox-Tools ein Kompetenzzentrum, indem Sie ein „goldenes Sandbox“-Paket erstellen, um Best Practices für mehrere Sandboxes zu standardisieren.

![Übersicht über den Export von Paketen über verschiedene Organisationen hinweg](../images/use-cases/packages-across-orgs.png){zoomable="yes"}

## Gründe für diesen Anwendungsfall {#why-this-use-case}

Viele große Unternehmen oder Unternehmen verwenden mehrere Sandboxes für verschiedene Organisationen, Teams, Regionen oder Entwicklungsumgebungen. Mit der Leistungsfähigkeit der [Sandbox-Tools](../ui/sandbox-tooling.md) können Sie ein „goldenes“ Sandbox-Paket erstellen, um Konsistenz, Compliance und die Abstimmung der Standards Ihres Unternehmens über mehrere Sandboxes hinweg sicherzustellen.

Dieses goldene Sandbox-Paket schafft ein Kompetenzzentrum für die effiziente gemeinsame Nutzung wichtiger Konfigurationen. Mithilfe von Sandbox-Tools können Sie Ihr Paket einfach über mehrere Sandboxes hinweg importieren. Sie können Ihr Paket auch für weitere Organisationen freigeben, um eine weit reichende Konsistenz zu gewährleisten.

Führen Sie die in diesem Anwendungsbeispiel beschriebenen Schritte aus, um Ihr eigenes goldenes Sandbox-Paket zu erstellen.

## Branchenbeispiel {#industry-example}

Nehmen wir als Beispiel eine Bank, die in verschiedenen Regionen wie Nordamerika, Europa und Afrika tätig ist. Jeder Markt bzw. jede Region verfügt über eine eigene Adobe Experience Platform-Instanz. Diese Bank möchte ein zentralisiertes Datenmodell beibehalten, das von einem globalen Architektenteam verwaltet wird, in dem eine einzige Version des Datenmodells über alle Märkte hinweg verteilt werden kann.

Diese Bank verwendet Sandbox-Tools, um ein goldenes Sandbox-Paket zu erstellen und zu pflegen. Dies hilft bei der Entwicklungseffizienz, ermöglicht konsistente Datenmodelle und stellt die Konsistenz über alle Regionen hinweg sicher.

## Voraussetzungen und Planung {#prerequisites-and-planning}

Beachten Sie bei der Planung der Einrichtung eines eigenen Kompetenzzentrums in Ihrem Unternehmen die folgenden Voraussetzungen bei Ihrem Planungsprozess:

- Ermitteln Sie die Best Practices und Konfigurationen, die Sie in Ihr Paket aufnehmen müssen.
- Erstellen Sie eine Sandbox mit allen relevanten und validierten Konfigurationen, die als goldene Sandbox festgelegt werden sollen.
- Gewinnen Sie bei Bedarf einen Beitrag der Stakeholder und stimmen Sie Ihren grundlegenden Standards zu.

### Benutzeroberflächenfunktionen, Platform-Komponenten und Experience Cloud-Produkte, die Sie verwenden werden {#ui-functionality-and-elements}

Um diesen Anwendungsfall erfolgreich zu implementieren, müssen Sie mehrere Bereiche von Adobe Experience Platform verwenden. Vergewissern Sie sich, dass Sie über [ erforderlichen (attributbasierten Zugriffssteuerungsberechtigungen](../../access-control/abac/overview.md) für alle diese Bereiche verfügen, oder bitten Sie Ihren Systemadministrator, Ihnen die erforderlichen Berechtigungen zu gewähren.

- [Sandbox-Werkzeuge](../ui/sandbox-tooling.md)
- [Sandbox-Verwaltung](../ui/user-guide.md)
- [Datensätze](../../catalog/datasets/overview.md)
- [Schemata](../../xdm//home.md)
- [Zielgruppen](../../segmentation/home.md)
- [Journey aus Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

## Erreichen des Anwendungsfalls: Allgemeine Übersicht {#achieve-the-use-case-high-level}

1. Erstellen Sie die Basiskonfiguration , die Ihre Best Practices in einer goldenen Sandbox darstellt. Dazu können Objekte wie Datensätze, Schemata, Zielgruppen oder Journey gehören.
2. Exportieren Sie die Konfiguration mithilfe der Sandbox-Tools in ein Paket.
3. Importieren Sie dieses Paket in alle relevanten Sandboxes.
4. Wenn Sie mehrere Organisationen haben, geben Sie dieses Paket für alle Ihre Organisationen frei.
5. Überwachen Sie Importe und Exporte und verfolgen Sie Änderungen mithilfe von Auditprotokollen.
6. Aktualisieren Sie Ihre goldene Sandbox regelmäßig, wenn sich die Standards weiterentwickeln, um sicherzustellen, dass alle Sandboxes weiterhin mit den Best Practices übereinstimmen.

## Erreichen des Anwendungsfalls: Schrittweise Anweisungen {#step-by-step-instructions}

Lesen Sie die folgenden Abschnitte, die Links zu weiterführender Dokumentation enthalten, um die einzelnen Schritte in der oben stehenden allgemeinen Übersicht auszuführen.

### Goldene Sandbox erstellen

Der erste Schritt, um Ihr Kompetenzzentrum zu ermöglichen, besteht darin, Ihre goldene Sandbox zu erstellen. Diese Sandbox sollte die grundlegenden Konfigurationen enthalten, die für Ihre Best Practices stehen. Um diese goldene Sandbox zu erstellen, folgen Sie der Anleitung unter [Erstellen einer neuen Sandbox](../ui/user-guide.md#create-a-new-sandbox) in Experience Platform.

Beginnen Sie nach der Erstellung Ihrer Sandbox mit der Erstellung Ihrer grundlegenden Objektkonfigurationen, z[ B. ](../../xdm/ui/resources/schemas.md#create-a-new-schema), [Datensätze](../../catalog/datasets/user-guide.md#create-a-dataset) oder [Audiences](../../segmentation/ui/segment-builder.md). Prüfen Sie unbedingt Ihre Konfigurationen, bevor Sie fortfahren.

### Exportieren der Sandbox in ein Paket

Jetzt, da Ihre Sandbox Ihre grundlegenden Objektkonfigurationen enthält, kann sie mithilfe der Sandbox-Tools in ein Paket exportiert werden. Befolgen Sie die Anleitung unter [Exportieren einer gesamten Sandbox](../ui/sandbox-tooling.md#export-an-entire-sandbox) um Ihr Golden-Sandbox-Paket zu erstellen.

### Paket in relevante Sandboxes importieren

Nachdem Ihr Paket erstellt wurde, können Sie dieses Paket in Ihre entsprechenden Sandboxes importieren. Es empfiehlt sich, ein Paket, das eine gesamte Sandbox enthält, in eine leere Sandbox zu importieren. Mithilfe von Sandbox-Tools können Sie [ein ganzes Sandbox-Paket importieren](../../sandboxes/ui/sandbox-tooling.md#import-the-entire-sandbox-package) direkt auf Experience Platform in eine Sandbox importieren.

### Package-Freigabe für mehrere Organisationen

Mit Sandbox-Tools können Sie Pakete, die Sie erstellt haben, unternehmensübergreifend freigeben. Befolgen Sie die [Anleitung zur Paketfreigabe](../../sandboxes/ui/sharing-packages-across-orgs.md), um Ihr goldenes Sandbox-Paket freizugeben.

### Importe und Exporte mithilfe von Auditprotokollen überwachen

Beim Importieren oder Exportieren Ihres Pakets können Sie den Status der Aufträge mithilfe des Dashboards **[!UICONTROL Aufträge]** in Experience Platform überwachen. Weitere Informationen zu Überwachungsaufträgen finden Sie im Handbuch unter [Überwachung von Importdetails](../../sandboxes/ui/sandbox-tooling.md#monitor-import-details).

### Aktualisieren Sie die goldene Sandbox regelmäßig

Nachdem Sie Ihr goldenes Sandbox-Paket abgeschlossen haben, haben Sie ein standardisiertes Kompetenzzentrum eingerichtet, das Sie weiterhin in Sandboxes importieren oder unternehmensübergreifend freigeben können. Wenn sich Ihre Best Practices ändern und weiterentwickeln, ist es wichtig, die grundlegenden Objektkonfigurationen in Ihrer goldenen Sandbox regelmäßig zu aktualisieren. Wenn Sie Aktualisierungen an der Sandbox vornehmen, können Sie neue Iterationen Ihres goldenen Sandbox-Pakets erstellen, indem Sie demselben Prozess folgen.

>[!NOTE]
>
> Die oben genannten Schritte folgen dem Prozess in der Benutzeroberfläche von Experience Platform. Es ist möglich, dieselben Schritte mithilfe der -API über verschiedene Endpunkte hinweg auszuführen. Weitere Informationen zu `sandboxes` einzelnen Anfragen über [ API finden ](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/api/sandboxes#create) im `packages` [Endpunkthandbuch](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages).

## Andere durch Partnerdatenunterstützung ermöglichte Anwendungsfälle {#other-use-cases}

Erkunden Sie weitere Anwendungsfälle, die über Sandbox-Tools aktiviert sind:

- [Sichern von Objektkonfigurationen mithilfe von Sandbox-Tools](./backup-object-configuration.md)
