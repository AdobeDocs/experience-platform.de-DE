---
title: Adobe Experience Platform – Versionshinweise November 2020
description: Die Versionshinweise von November 2020 für Adobe Experience Platform.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2178'
ht-degree: 20%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: Donnerstag, 11. November 2020**

Neue Funktionen in Adobe Experience Platform:

- [Adobe Experience Platform Data Lake-Migration](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Aktualisierungen vorhandener Funktionen:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform Data Lake-Migration {#migration}

Während Adobe den Data Lake von Gen1 auf Gen2 migriert, können Benutzende aus dem Data Lake lesen, aber alle Funktionen, die in den Data Lake schreiben, sind betroffen. Adobe wird sich mit Systemadministratoren in Verbindung setzen, um die Auswirkungen der Migration im Detail zu besprechen und die Migrationsdaten und -zeiten für bestimmte Organisationen zu bestätigen.

Weitere Informationen finden Sie im [Data Lake-Migrationshandbuch](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] nutzt [Adobe Admin Console](https://adminconsole.adobe.com)-Produktprofile, um Benutzende mit Berechtigungen und Sandboxes zu verknüpfen. Berechtigungen steuern den Zugriff auf eine Vielzahl von Experience Platform-Funktionen, einschließlich Datenmodellierung, Profilverwaltung und Sandbox-Administration.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Berechtigungen | In der [!DNL Admin Console] können Sie auf der Registerkarte innerhalb eines [!DNL Experience Platform] Produktprofils anpassen, welche [!DNL Experience Platform]-Funktionen für die mit diesem Profil verbundenen Benutzer verfügbar sind. Zu den verfügbaren Berechtigungskategorien gehören: **[!UICONTROL Datenmodellierung]**, **[!UICONTROL Datenverwaltung]**, **[!UICONTROL Profilverwaltung]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Datenüberwachung]**, **[!UICONTROL Sandbox-Administration]**, **[!UICONTROL Datenaufnahme]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Query Service]** und **&#x200B;**&#x200B;Data Governance **&#x200B;**. |
| Zugriff auf Sandboxes | Die **[!UICONTROL Berechtigungen]** in einem [!DNL Experience Platform] Produktprofil kann Benutzern Zugriff auf bestimmte Sandboxes gewähren. Zusätzliche Informationen finden Sie im Abschnitt zu [Sandboxes](#sandboxes) unten. |

Weiterführende Informationen finden Sie unter [Zugriffskontrolle – Übersicht](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] ist ein in [!DNL Experience Platform] integrierter Anwendungs-Service. Sie ermöglicht es Ihnen, [!DNL Experience Platform] zu nutzen, um Ihren Kunden über alle Berührungspunkte hinweg zur richtigen Zeit das beste Angebot und Erlebnis zu bieten.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Zentralisierte Angebotsbibliothek | Die Benutzeroberfläche, in der Sie die verschiedenen Elemente erstellen und verwalten, aus denen Ihre Angebote bestehen, und deren Regeln und Einschränkungen definieren. |
| Offer Decisioning-Engine | Die Offer Decisioning-Engine nutzt [!DNL Experience Platform] Daten und [!DNL Real-Time Customer Profiles] sowie die Angebotsbibliothek, um den richtigen Zeitpunkt, die richtigen Kunden und die richtigen Kanäle für das Unterbreiten von Angeboten auszuwählen. |

Weitere Informationen finden Sie in der [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=de).

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] wurde entwickelt, um Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um diesem Bedarf gerecht zu werden, stellt [!DNL Experience Platform] Sandboxes bereit, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Produktions-Sandbox | [!DNL Experience Platform] bietet eine einzelne Produktions-Sandbox, die nicht gelöscht oder zurückgesetzt werden kann. Die Gesamtzahl der verfügbaren Sandboxes, Produktion und produktionsfremd, wird durch die erworbene Lizenz bestimmt. |
| Nicht-Produktions-Sandboxes | Für eine einzelne [!DNL Experience Platform]-Instanz können mehrere Nicht-Produktions-Sandboxes erstellt werden, sodass Sie Funktionen testen, Experimente durchführen und benutzerdefinierte Konfigurationen vornehmen können, ohne die Produktions-Sandbox zu beeinträchtigen. |
| Sandbox-Wechsler | In der [!DNL Experience Platform] Benutzeroberfläche können Sie mit dem Sandbox-Umschalter in der oberen linken Ecke des Bildschirms über ein Dropdown-Menü zwischen verfügbaren Sandboxes wechseln. Der Sandbox-Umschalter bietet außerdem eine Suchfunktion, mit der Sie durch verfügbare Sandboxes filtern können. |
| `x-sandbox-name`-Kopfzeile | Alle Aufrufe [!DNL Experience Platform] -APIs müssen jetzt die neue `x-sandbox-name`-Kopfzeile enthalten, deren Wert auf das `name` Attribut der Sandbox verweist, in der der Vorgang ausgeführt wird. |

Weiterführende Informationen finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Iterative Vorgänge | [!DNL Data Prep] Mapper unterstützt jetzt die Durchführung iterativer Vorgänge in einer Hierarchie. |
| Mapper-Funktion | [!DNL Data Prep] Mapper hat jetzt die Möglichkeit, **nicht** ein Attribut aus der Quelle in das Ziel-XDM zu kopieren. |

Weitere Informationen finden Sie unter [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Der Data Science Workspace ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen. Eine der Möglichkeiten, wie Data Science Workspace dies erreicht, ist die Verwendung von [!DNL JupyterLab]. [!DNL JupyterLab] ist eine Web-basierte Benutzeroberfläche für [[!DNL Project Jupyter]](https://jupyter.org/) und ist eng in Adobe Experience Platform integriert. Es bietet eine interaktive Entwicklungsumgebung für Datenwissenschaftler, die mit [!DNL Jupyter] Notebooks, Code und Daten arbeiten möchten.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| [!DNL JupyterLab] Recipe Builder-Vorlage | Notebook-Rezepturanforderungen und aktualisierte Versionen. [!DNL Python] Basisimage der ML-Laufzeitumgebung wurde aktualisiert, sodass es ausschließlich [!DNL Python] 3.6.7 und eine [!DNL Conda]-Umgebung verwendet. |

Weitere Informationen finden Sie im Dokument unter [Erstellen eines Rezepts mit Jupyter-Notebooks](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] {#destinations}

In [Real-Time Customer Data Platform](../../rtcdp/overview.md) sind Ziele vorgefertigte Integrationen mit Zielplattformen, die Daten nahtlos für diese Partner aktivieren.

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| Hartlöten | Braze ist eine umfassende Plattform zur Kundeninteraktion, die relevante und einprägsame Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht. |
| Microsoft Bing | Das Microsoft Bing-Ziel hilft Ihnen bei der Ausführung von Retargeting- und zielgruppenorientierten digitalen Kampagnen in Microsoft Display Advertising. |
| The Trade Desk | The Trade Desk ist eine Self-Service-Plattform für Anzeigenkäufer, mit der sie Retargeting- und zielgruppenorientierte digitale Kampagnen über Display-, Video- und mobile Inventarquellen hinweg durchführen können. |

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| UX-Updates für Zieldetails | Der Ziel-Workflow von Real-Time CDP umfasst jetzt eine Inline-Überwachung, damit Sie sehen können, welche Batch-Aktivierungen erfolgreich waren. Diese Funktion ermöglicht es Benutzenden, Probleme direkt im Workflow für Batch-Ziele über Warnhinweise und ein Überwachungs-Dashboard zu beheben, um Fehler in der Verarbeitungs-Pipeline zu verfolgen. |
| Dateiverschlüsselung | Für dateibasierte Ziele können Benutzerinnen und Benutzer jetzt ihren exportierten Dateien eine Verschlüsselung hinzufügen. |
| Dateiplanung | Sowohl für E-Mail-basierte als auch für Cloud-Speicher-Ziele können Benutzerinnen und Benutzer einen einmaligen Export erstellen oder tägliche Momentaufnahmen erstellen. |
| Pflichtfelder | Benutzerinnen und Benutzer können Felder als Pflichtfelder markieren, sodass nur Felder exportiert werden, die das Pflichtfeld enthalten. |

Weiterführende Informationen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Intelligent Services {#intelligent-services}

Mit Intelligent Services können Marketing-Analysten und -Experten die Vorteile von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen nutzen. So können Marketing-Analysefachleute mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für die Anforderungen der Firma erstellen, ohne dass hierfür Kenntnisse aus der Datenwissenschaft erforderlich sind.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Datensatz für Customer Experience Events (CEE) | Das Erstellen eines CEE-Datensatzes unterstützt jetzt das Hinzufügen von Identitätsfeldern zum Datensatz mit dem Schema-Editor. Attributions-KI und Kunden-KI verwenden die primäre Identität zum Kombinieren von Ereignissen. |

Weitere Informationen finden Sie im Abschnitt zum [ von Identitätsfeldern zu einem Datensatz ](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) Intelligent Services-Datenvorbereitungshandbuch.

### Attributions-KI

Attribution AI ist Teil von Intelligent Services und bietet einen mehrere Kanäle umfassenden algorithmischen Attributions-Service, der den Einfluss und die inkrementelle Auswirkung von Kundeninteraktionen auf bestimmte Ergebnisse berechnet.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Link zur Datenquelle | Der Link zur ursprünglichen Datensatzquelle kann in der rechten Leiste einer ausgewählten Service-Instanz angezeigt und aufgerufen werden. |
| Instanznamen bearbeiten | Sie können jetzt den Namen einer vorhandenen Attribution AI-Instanz ändern. |
| Instanz klonen | Kopiert die aktuell ausgewählte Dienstinstanz und ermöglicht Änderungen. |
| Konfigurationsparameter der Instanz ändern | Sie können jetzt die Konfiguration einer vorhandenen Attribution AI-Instanz ändern, wenn sie noch nicht mit der Bewertung begonnen hat. |
| Einmalige Punktzahl | Sie können jetzt Ad-hoc-Modellbewertung in Ihren Attribution AI-Instanzen Trigger machen. |
| Durchlauf durch Spalten | Sie können jetzt zusätzliche Spalten konfigurieren, die den Rohausgabe-Score-Dateien hinzugefügt werden, um zusätzliche Dimensionen zu BI-Tool-Ansichten hinzuzufügen. |
| Instanzaktivierung und -deaktivierung | Sie können jetzt das geplante Modell-Training und die Bewertung Ihrer Attribution AI-Instanzen aktivieren und deaktivieren. |
| Berechtigungsverfolgung | Die Gesamtmenge der von Ihrem Konto verwendeten Attribution Insights finden Sie im Container Instanz erstellen . |
| Touchpoint-Aufschlüsselung nach Position | Ein neues Insights-Diagramm, das eine Analyse von Touchpoints nach Konversionspfadpositionen bietet. |
| Top-Konversionspfade | Ein neues Insights-Diagramm auf der Registerkarte Pfadanalyse . Das Diagramm enthält eine Liste der fünf wichtigsten Konversionspfade, die die Sequenz der Marketing-Kanal-Touchpoints zeigen, die zu den meisten Konversionen geführt haben. |
| Touchpoint-Effektivität | Bietet detaillierte Einblicke in die drei wichtigsten Variablen, mit denen Ihr Modell die Touchpoint-Effektivität misst. Die Variablen sind das Verhältnis von positiven und negativen Pfaden, Touchpoint-Effizienz und Touchpoint-Volumen. |

Weitere Informationen finden Sie im Abschnitt [Übersicht über Attributions-KI](../../intelligent-services/attribution-ai/overview.md).

### Kunden-KI

Kunden-KI als Teil von Intelligent Services bietet Marketing-Experten die Möglichkeit, Kundenprognosen auf individueller Ebene mit Erläuterungen zu generieren. Mithilfe von Einflussfaktoren kann Customer AI vorhersagen, was ein Kunde wahrscheinlich tun wird und warum. Darüber hinaus können Marketing-Experten von Prognosen und Einblicken durch Customer AI profitieren, um Kundenerlebnisse durch Bereitstellung der am besten geeigneten Angebote und Botschaften zu personalisieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Link zur Datenquelle | Der Link zur ursprünglichen Datensatzquelle kann in der rechten Leiste einer ausgewählten Service-Instanz angezeigt und aufgerufen werden. |
| Instanznamen bearbeiten | Sie können den Namen einer vorhandenen Customer AI-Instanz ändern. |
| Konfigurationsparameter der Instanz ändern | Sie können jetzt die Konfiguration einer bestehenden Kunden-KI-Instanz ändern, falls sie noch keine Bewertung gestartet hat. |
| Instanz klonen | Kopiert die aktuell ausgewählte Dienstinstanz und ermöglicht Änderungen. |
| Berechtigungsverfolgung | Die Gesamtzahl der von Kunden-KI für Ihr Konto bewerteten Profile finden Sie im Container „Instanz erstellen“. |
| Prognoseziel | Die Flexibilität bei der Erstellung eines Prognoseziels wurde durch neue Optionen erhöht, mit denen vorhergesagt werden kann, ob etwas „eintritt“ oder „nicht eintritt“. Darüber hinaus wurden die Optionen hinzugefügt, mit denen vorhergesagt werden kann, ob „alle“ Ereignisse eintreten oder „eines“ der Ereignisse eintritt, wenn mehrere Ereignisse verwendet werden. |
| Drilldown für Einflussfaktoren | Neigungs-Top-Einflussfaktor-Buckets enthalten jetzt Drill-Downs. Drilldown-Menüs sind eine tiefer gehende Zusammenfassung der Werte für die wichtigsten Einflussfaktoren innerhalb eines Neigungs-Buckets. |

Weitere Informationen finden Sie im Abschnitt [Kunden-KI - Übersicht](../../intelligent-services/customer-ai/overview.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. [!DNL Profile] können Sie Ihre unterschiedlichen Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige, Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Aktualisierter Workflow für Zusammenführungsrichtlinien | Experience Platform hat die Konfiguration der Zusammenführungsrichtlinie auf einen neuen schrittweisen Workflow aktualisiert. Dieser Workflow ermöglicht es Benutzenden, Datenfragmente aus mehreren Profildatensätzen zusammenzuführen und Prioritäten für die Art und Weise festzulegen, wie Daten über diese Datensätze hinweg zusammengeführt werden, um eine umfassende Ansicht jedes einzelnen Profils zu erstellen. Benutzer können ausgewählte XDM-Datensätze mit einzelnen Profilen zusammenführen, indem sie die entsprechende Zusammenführungsmethode auswählen (Zeitstempel geordnet oder Datensatzpriorität) und ExperienceEvent-Datensätze an die Profildatensätze anhängen. |
| Vereinigungsschemaansicht | In der Experience Platform-Benutzeroberfläche können Benutzende Informationen zu allen Schemata und Datensätzen, die zum Vereinigungsschema beitragen, sowie Attribute von Oberflächenschlüsseln wie Identitäts- und Beziehungsfelder leichter finden. Diese Aktualisierungen verbessern die Möglichkeit, Probleme zu beheben und zu überprüfen, ob Profile korrekt konfiguriert und Identitäten korrekt zugeordnet wurden und Daten erfolgreich aufgenommen wurden. |

Weitere Informationen zum Echtzeit-Kundenprofil, einschließlich Tutorials und Best Practices für die Arbeit mit [!DNL Profile], finden Sie [ der Übersicht zum Echtzeit-Kundenprofil](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kann Daten aus externen Quellen aufnehmen und ermöglicht es Ihnen gleichzeitig, diese Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Quellen**

| Funktion | Beschreibung |
| ------- | ----------- |
| [!DNL Shopify] | Sie können [!DNL Shopify] jetzt mit [!DNL Experience Platform] über die [!DNL Flow Service]-API oder die Benutzeroberfläche verbinden. Weitere Informationen dazu finden Sie [ „Übersicht ](../../sources/connectors/ecommerce/shopify.md) Shopify-Connectors“. |

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbindungsinformationen aktualisieren | Sie können jetzt die Namen, Beschreibungen und Anmeldeinformationen vorhandener Batch-Verbindungen mithilfe der [!DNL Flow Service]-API und der Benutzeroberfläche aktualisieren. Weitere Informationen finden Sie im Tutorial zum [Aktualisieren von Verbindungen mithilfe der Flow Service-](../../sources/tutorials/api/update.md) und [Bearbeiten von Kontodetails mithilfe der Benutzeroberfläche](../../sources/tutorials/ui/monitor.md). |
| Verbindungen löschen | Batch-Verbindungen, die Fehler enthalten oder unnötig geworden sind, können jetzt mithilfe der [!DNL Flow Service]-API und der Benutzeroberfläche gelöscht werden. Weitere Informationen finden Sie im Tutorial [Löschen von Verbindungen mithilfe der Flow Service-API](../../sources/tutorials/api/delete.md) und [Löschen von Konten mithilfe der Benutzeroberfläche](../../sources/tutorials/ui/delete-accounts.md). |
| Hierarchische Zuordnung | Sie können während der Datenaufnahme eine Vorschau einer hierarchischen Quelldatei anzeigen, z. B. JSON oder Parquet. Weitere Informationen finden Sie im Tutorial [Konfigurieren eines Datenflusses für Cloud-Speicher-Connectoren in ](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) Benutzeroberfläche“. |
| API-Unterstützung für die Zuordnung in Streaming-Quellen | Sie können jetzt APIs verwenden, um Zuordnungsfunktionen mit Streaming-Quellen durchzuführen. |
| API-Unterstützung für benutzerdefinierte Trennzeichen für Cloud-Speicherquellen | Sie können jetzt Dateien ohne CSV-Trennzeichen mithilfe von Cloud-Speicherquellen erfassen. Sie können jedes einzelne Spaltentrennzeichen wie Tabulator, Komma, senkrechte Striche, Semikolon oder Hash verwenden, um flache Dateien in jedem Format zu erfassen. |
| Sandbox-Unterstützung für Adobe Audience Manager Connector | Der Audience Manager-Connector ist jetzt Sandbox-fähig. Benutzerinnen und Benutzer können den Connector aktivieren, um Audience Manager-Datensätze an die Sandbox ihrer Wahl (einschließlich Nicht-Produktions-Sandboxes) weiterzuleiten. Die Konfiguration ist auf eine Sandbox pro Organisation beschränkt. |
| UX-Verbesserungen | Die dateibasierte Aufnahme ist jetzt über den Quellkatalog zugänglich. |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
