---
title: Adobe Experience Platform – Versionshinweise November 2020
description: Die Versionshinweise von November 2020 für Adobe Experience Platform.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2176'
ht-degree: 21%

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
- [[!DNL Destinations] Service](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform Data Lake-Migration {#migration}

Während Adobe den Data Lake von Gen1 zu Gen2 migriert, können Benutzer zwar vom Data Lake aus lesen, aber alle Funktionen, die in den Data Lake schreiben, sind betroffen. Adobe wird sich an die Systemadministratoren wenden, um die Auswirkungen der Migration ausführlich zu erörtern und die Migrationsdaten und -zeiten für bestimmte Organisationen zu bestätigen.

Weitere Informationen finden Sie im [Data Lake-Migrationshandbuch](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] nutzt [Adobe Admin Console](https://adminconsole.adobe.com) -Produktprofile, um Benutzer mit Berechtigungen und Sandboxes zu verknüpfen. Berechtigungen steuern den Zugriff auf verschiedene Platform-Funktionen, einschließlich Datenmodellierung, Profil-Management und Sandbox-Verwaltung.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Berechtigungen | Auf der Registerkarte &quot;[!DNL Admin Console]&quot;in einem [!DNL Platform] -Produktprofil können Sie anpassen, welche [!DNL Platform]-Funktionen für die mit diesem Profil verknüpften Benutzer verfügbar sind. Zu den verfügbaren Berechtigungskategorien gehören: **[!UICONTROL Datenmodellierung]**, **[!UICONTROL Datenverwaltung]**, **[!UICONTROL Profilverwaltung]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Datenüberwachung]**, **[!UICONTROL Sandbox-Administration]**, **[!UICONTROL Ziele]**, **[!UICONTROL Datenaufnahme]**, **[!UICONTROL Data Science Workspace 17},**[!UICONTROL  Query Service ]**und**[!UICONTROL  Data Governance ]**.]** |
| Zugriff auf Sandboxes | Die Registerkarte **[!UICONTROL Berechtigungen]** in einem [!DNL Platform] -Produktprofil kann Benutzern Zugriff auf bestimmte Sandboxes gewähren. Zusätzliche Informationen finden Sie im Abschnitt zu [Sandboxes](#sandboxes) unten. |

Weiterführende Informationen finden Sie unter [Zugriffskontrolle – Übersicht](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] ist ein in [!DNL Experience Platform] integrierter Anwendungs-Service. Dadurch können Sie mit [!DNL Platform] das beste Angebot und Erlebnis für Ihre Kunden über alle Touchpoints hinweg zur richtigen Zeit bereitstellen.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Zentralisierte Angebotsbibliothek | Die Oberfläche, auf der Sie die verschiedenen Elemente erstellen und verwalten, aus denen Ihre Angebote bestehen, und deren Regeln und Begrenzungen definieren. |
| Angebotsentscheidungen-Engine | Die Offer Decisioning-Engine nutzt [!DNL Platform] -Daten und [!DNL Real-Time Customer Profiles] zusammen mit der Angebotsbibliothek, um die richtige Zeit, Kunden und Kanäle für die Bereitstellung von Angeboten auszuwählen. |

Weitere Informationen finden Sie in der Dokumentation zu [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=de) .

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] wurde entwickelt, um Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um dies zu erreichen, stellt [!DNL Experience Platform] Sandboxes bereit, die eine einzelne [!DNL Platform] -Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu unterstützen.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Produktions-Sandbox | [!DNL Experience Platform] stellt eine einzelne Produktions-Sandbox bereit, die weder gelöscht noch zurückgesetzt werden kann. Die Gesamtzahl der verfügbaren Sandboxes, Produktion und Nicht-Produktion wird durch die erworbene Lizenz bestimmt. |
| Nicht-Produktions-Sandboxes | Für eine einzelne [!DNL Platform] -Instanz können mehrere Nicht-Produktions-Sandboxes erstellt werden, sodass Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen können, ohne die Produktions-Sandbox zu beeinträchtigen. |
| Sandbox-Wechsler | In der Benutzeroberfläche von [!DNL Experience Platform] können Sie über den Sandbox-Umschalter in der oberen linken Ecke des Bildschirms über ein Dropdown-Menü zwischen verfügbaren Sandboxes wechseln. Der Sandbox-Umschalter bietet außerdem eine Suchfunktion, mit der Sie nach verfügbaren Sandboxes filtern können. |
| `x-sandbox-name`-Kopfzeile | Alle Aufrufe von [!DNL Experience Platform] -APIs müssen jetzt die neue Kopfzeile `x-sandbox-name` enthalten, deren Wert auf das Attribut `name` der Sandbox verweist, in der der Vorgang ausgeführt werden soll. |

Weiterführende Informationen finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Iterative Vorgänge | [!DNL Data Prep] Mapper unterstützt jetzt die Ausführung iterativer Operationen auf einer Hierarchie. |
| Zuordnungsfunktion | [!DNL Data Prep] Der Mapper hat jetzt die Möglichkeit, ein Attribut **nicht** aus der Quelle in das Ziel-XDM zu kopieren. |

Weitere Informationen finden Sie unter [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Der Data Science Workspace ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen. Eine der Möglichkeiten, wie Data Science Workspace dies erreicht, ist die Verwendung von [!DNL JupyterLab]. [!DNL JupyterLab] ist eine webbasierte Benutzeroberfläche für [[!DNL Project Jupyter]](https://jupyter.org/) und ist eng in Adobe Experience Platform integriert. Es bietet eine interaktive Entwicklungsumgebung, in der Datenwissenschaftler mit [!DNL Jupyter] Notebooks, Code und Daten arbeiten können.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| [!DNL JupyterLab] Vorlage für den Rezeptersteller | Verwendung und Versionen von Notebook- und Rezept-Anforderungen wurden aktualisiert. [!DNL Python] ML Runtime-Basisbild wurde aktualisiert, um ausschließlich [!DNL Python] 3.6.7 und eine [!DNL Conda] -Umgebung zu verwenden. |

Weitere Informationen finden Sie im Dokument unter [Erstellen eines Rezepts mit Jupyter Notebooks](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] Service {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner nahtlos aktivieren.

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| Brase | Braze ist eine umfassende Kundeninteraktionsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht. |
| Microsoft Bing | Das Microsoft Bing-Ziel unterstützt Sie beim Ausführen von digitalen Kampagnen für Retargeting und Zielgruppen-Targeting in Microsoft Display Advertising. |
| The Trade Desk | Das Trade Desk ist eine Self-Service-Plattform für Anzeigenkäufer, mit der sie digitale Kampagnen für Zielgruppen und Zielgruppen aus Display-, Video- und mobilen Inventarquellen ausführen können. |

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| UX-Aktualisierungen für Zieldetails | Der Ziel-Workflow von Real-Time CDP umfasst jetzt die Inline-Überwachung, sodass Sie sehen können, welche Batch-Aktivierungen erfolgreich waren. Mit dieser Funktion können Benutzer Probleme direkt im Workflow für Batch-Ziele über Warnhinweise und ein Monitoring-Dashboard beheben, um Fehler in der Verarbeitungs-Pipeline zu verfolgen. |
| Dateiverschlüsselung | Bei dateibasierten Zielen können Benutzer ihren exportierten Dateien jetzt Verschlüsselung hinzufügen. |
| Dateiplanung | Sowohl für E-Mail-basierte als auch Cloud-Speicher-Ziele können Benutzer einen einmaligen Export erstellen oder tägliche Momentaufnahmen erstellen. |
| Obligatorische Felder | Benutzer können Felder als Pflichtfelder markieren, um sicherzustellen, dass nur Felder exportiert werden, die das Pflichtfeld enthalten. |

Weiterführende Informationen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Intelligent Services {#intelligent-services}

Mit Intelligent Services können Marketing-Analysten und -Experten die Vorteile von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen nutzen. So können Marketing-Analysefachleute mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für die Anforderungen der Firma erstellen, ohne dass hierfür Kenntnisse aus der Datenwissenschaft erforderlich sind.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Datensatz &quot;Consumer Experience Events&quot;(CEE) | Das Erstellen eines CEE-Datensatzes unterstützt jetzt das Hinzufügen von Identitätsfeldern zum Datensatz mit dem Schema Editor. Attribution AI und Customer AI verwenden die primäre Identität zur Kombination von Ereignissen. |

Weitere Informationen finden Sie im Abschnitt zum Hinzufügen von Identitätsfeldern zu einem Datensatz ](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) im Handbuch zur Datenvorbereitung für Intelligent Services.[

### Attributions-KI

Attribution AI als Teil von Intelligent Services ist ein algorithmischer Attributionsdienst mit mehreren Kanälen, der den Einfluss und die inkrementelle Auswirkung von Kundeninteraktionen auf bestimmte Ergebnisse berechnet.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Datenquellenlink | Der Link zur ursprünglichen Datensatzquelle kann in der rechten Leiste einer ausgewählten Dienstinstanz angezeigt und zu navigiert werden. |
| Name der Instanz bearbeiten | Sie können jetzt den Namen einer bestehenden Attribution AI-Instanz ändern. |
| Instanz klonen | Kopiert die derzeit ausgewählte Dienstinstanz-Einrichtung und lässt Änderungen zu. |
| Konfigurationsparameter der Instanz ändern | Sie können jetzt die Konfiguration einer vorhandenen Attribution AI-Instanz ändern, wenn diese noch nicht mit der Auswertung begonnen hat. |
| Einmalige Auswertung | Sie können jetzt die Ad-hoc-Modellbewertung in Ihren Attribution AI-Instanzen Trigger haben. |
| Übergeben von Spalten | Sie können jetzt zusätzliche Spalten konfigurieren, die zu den Rohwertdateien für die Ausgabe hinzugefügt werden, um den BI-Tool-Ansichten zusätzliche Dimensionen hinzuzufügen. |
| Aktivierung und Deaktivierung der Instanz | Sie können jetzt die geplante Modellschulung und -bewertung Ihrer Attribution AI-Instanzen aktivieren und deaktivieren. |
| Entitäts-Tracking | Sie können die Gesamtanzahl der von Ihrem Konto verwendeten Attributionseinblicke im Container der Instanz erstellen finden. |
| Touchpoint-Aufschlüsselung nach Position | Ein neues Einblicke-Diagramm, das eine Analyse von Touchpoints nach Konversionspfadpositionen bereitstellt. |
| Top-Konversionspfade | Ein neues Einblicke-Diagramm auf der Registerkarte Pfadanalyse . Das Diagramm enthält eine Liste der fünf wichtigsten Konversionspfade, die die Sequenz der Marketing-Kanal-Touchpoints anzeigen, die zu den meisten Konversionen geführt haben. |
| Touchpoint-Effektivität | Bietet umfassende Einblicke in die drei wichtigsten Variablen, mit denen Ihr Modell die Touchpoint-Effektivität misst. Die Variablen sind das Verhältnis zwischen berührten positiven und negativen Pfaden, Touchpoint-Effizienz und Touchpoint-Lautstärke. |

Weitere Informationen finden Sie in der [Attribution AI-Übersicht](../../intelligent-services/attribution-ai/overview.md).

### Kunden-KI

Customer AI als Teil von Intelligent Services bietet Marketing-Experten die Möglichkeit, Kundenprognosen auf individueller Ebene mit Erklärungen zu generieren. Mithilfe von Einflussfaktoren kann Customer AI vorhersagen, was ein Kunde wahrscheinlich tun wird und warum. Darüber hinaus können Marketing-Experten von Prognosen und Einblicken durch Customer AI profitieren, um Kundenerlebnisse durch Bereitstellung der am besten geeigneten Angebote und Botschaften zu personalisieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Datenquellenlink | Der Link zur ursprünglichen Datensatzquelle kann in der rechten Leiste einer ausgewählten Dienstinstanz angezeigt und zu navigiert werden. |
| Name der Instanz bearbeiten | Sie können den Namen einer vorhandenen Customer AI-Instanz ändern. |
| Konfigurationsparameter der Instanz ändern | Sie können jetzt die Konfiguration einer vorhandenen Customer AI-Instanz ändern, wenn diese noch keine Auswertung gestartet hat. |
| Instanz klonen | Kopiert die derzeit ausgewählte Dienstinstanz-Einrichtung und lässt Änderungen zu. |
| Entitäts-Tracking | Sie finden die Gesamtzahl der Profile, die von Customer AI für Ihr Konto bewertet wurden, im Container Instanz erstellen . |
| Vorhersageziel | Die Flexibilität beim Erstellen eines Prognoseziels wurde durch neue Optionen erhöht, um vorherzusagen, ob etwas &quot;eintritt&quot;oder &quot;nicht eintritt&quot;. Darüber hinaus wurden die Optionen hinzugefügt, mit denen vorhergesagt werden kann, ob &quot;alle&quot;Ereignisse eintreten oder eines der Ereignisse eintritt, wenn mehrere Ereignisse verwendet werden. |
| Drilldown für Einflussfaktoren | Propensity Top-Einflussfaktor-Buckets enthalten jetzt Drilldowns. Drilldowns sind eine tiefergehende Zusammenfassung der Werte für jeden der wichtigsten Einflussfaktoren innerhalb eines Tendenzbehälter. |

Weitere Informationen finden Sie in der [Übersicht über Customer AI](../../intelligent-services/customer-ai/overview.md) .

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit [!DNL Profile] können Sie Ihre unterschiedlichen Kundendaten in einer einheitlichen Ansicht zusammenfassen, die eine verwertbare, mit Zeitstempel versehene Übersicht über jede Kundeninteraktion bietet.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Aktualisierter Workflow für Zusammenführungsrichtlinien | Platform hat die Konfiguration der Zusammenführungsrichtlinie auf einen neuen schrittweisen Workflow aktualisiert. Dieser Workflow ermöglicht es Benutzern, Datenfragmente aus mehreren Profildatensätzen zusammenzuführen und Prioritäten für die Zusammenführung von Daten aus diesen Datensätzen festzulegen, um eine umfassende Ansicht jedes Einzelnen zu erstellen. Benutzer können ausgewählte individuelle XDM-Profil-Datensätze zusammenführen, indem sie die entsprechende Zusammenführungsmethode auswählen (Zeitstempel geordnet oder Datensatzpriorität) und ExperienceEvent-Datensätze an die Profil-Datensätze anhängen. |
| Vereinigungsschemaansicht | In der Experience Platform-Benutzeroberfläche können Benutzer leichter Informationen zu allen Schemas und Datensätzen finden, die zum Vereinigungsschema beitragen, sowie wichtige Oberflächenattribute wie Identitäts- und Beziehungsfelder. Diese Aktualisierungen verbessern die Fehlerbehebung und die Überprüfung der korrekten Konfiguration von Profilen, der korrekten Zuordnung von Identitäten und der erfolgreichen Erfassung von Daten. |

Weitere Informationen zum Echtzeit-Kundenprofil, einschließlich Tutorials und Best Practices für die Arbeit mit [!DNL Profile] -Daten, finden Sie in der [Übersicht zum Echtzeit-Kundenprofil](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten mithilfe von [!DNL Platform] -Diensten strukturieren, beschriften und erweitern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Quellen**

| Funktion | Beschreibung |
| ------- | ----------- |
| [!DNL Shopify] | Sie können [!DNL Shopify] jetzt mit [!DNL Experience Platform] über die [!DNL Flow Service]-API oder die Benutzeroberfläche verbinden. Weitere Informationen finden Sie unter [Übersicht über den Shopify-Connector](../../sources/connectors/ecommerce/shopify.md) . |

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbindungsinformationen aktualisieren | Sie können jetzt die Namen, Beschreibungen und Anmeldeinformationen vorhandener Batch-Verbindungen mithilfe der API [!DNL Flow Service] und der Benutzeroberfläche aktualisieren. Weitere Informationen finden Sie im Tutorial zum Aktualisieren von Verbindungen mithilfe der Flow Service-API](../../sources/tutorials/api/update.md) und zum Bearbeiten von Kontodetails mithilfe der Benutzeroberfläche ](../../sources/tutorials/ui/monitor.md).[[ |
| Verbindungen löschen | Batch-Verbindungen, die Fehler enthalten oder unnötig geworden sind, können jetzt mit der [!DNL Flow Service] -API und der -Benutzeroberfläche gelöscht werden. Weitere Informationen finden Sie im Tutorial zum [Löschen von Verbindungen mithilfe der Flow Service-API](../../sources/tutorials/api/delete.md) und zum [ Löschen von Konten mithilfe der Benutzeroberfläche](../../sources/tutorials/ui/delete-accounts.md). |
| Hierarchische Zuordnung | Sie können während der Datenerfassung eine Vorschau einer hierarchischen Quelldatei wie JSON oder Parquet anzeigen. Weitere Informationen finden Sie im Tutorial zum Konfigurieren eines Datenflusses für Cloud-Speicher-Connectoren in der Benutzeroberfläche ](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) .[ |
| API-Unterstützung für die Zuordnung in Streaming-Quellen | Sie können jetzt APIs verwenden, um Zuordnungsfunktionen mit Streaming-Quellen auszuführen. |
| API-Unterstützung für benutzerdefinierte Trennzeichen für Cloud-Speicher-Quellen | Sie können jetzt nicht CSV-getrennte Dateien mithilfe von Cloud-Speicher-Quellen erfassen. Sie können ein beliebiges Trennzeichen für einzelne Spalten wie Tabulatoren, Kommas, senkrechte Striche, Semikolons oder Hash verwenden, um flache Dateien in jedem beliebigen Format zu erfassen. |
| Sandbox-Unterstützung für Adobe Audience Manager-Connector | Der Audience Manager-Connector ist jetzt Sandbox-unterstützt. Benutzer können den Connector aktivieren, um Audience Manager-Datensätze an die Sandbox ihrer Wahl zu leiten (einschließlich Nicht-Produktions-Sandboxes). Die Konfiguration ist auf eine Sandbox pro Organisation beschränkt. |
| UX-Verbesserungen | Die dateibasierte Erfassung ist jetzt über den Quellkatalog verfügbar. |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
