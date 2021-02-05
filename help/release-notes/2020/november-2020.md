---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform, 11. November 2020
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 23%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 11. November 2020**

Neue Funktionen in Adobe Experience Platform:

- [Adobe Experience Platform Data Lake Migration](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Aktualisierungen vorhandener Funktionen:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] Dienst](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform Data Lake Migration {#migration}

Während die Adobe den Data Lake von Gen1 zu Gen2 migriert, können Benutzer den Data Lake zwar lesen, aber alle Funktionen, die in den Data Lake schreiben, werden beeinträchtigt. Adobe wird sich an Systemadministratoren wenden, um die Auswirkungen der Migration ausführlich zu erörtern und die Migrationsdaten und -zeiten für bestimmte IMS-Organisationen zu bestätigen.

Weitere Informationen finden Sie im Handbuch [Datensee-Migration](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] nutzt [Adobe Admin Console](https://adminconsole.adobe.com)-Produktprofile, um Benutzer mit Berechtigungen und Sandboxes zu verknüpfen. Berechtigungen steuern den Zugriff auf verschiedene Platform-Funktionen, einschließlich Datenmodellierung, Profil-Management und Sandbox-Verwaltung.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Berechtigungen | Auf der Registerkarte in einem [!DNL Admin Console]-Profil können Sie anpassen, welche [!DNL Platform]-Funktionen für die an dieses Profil angehängten Benutzer verfügbar sind. [!DNL Platform] Zu den verfügbaren Kategorien für Berechtigungen gehören: **[!UICONTROL Datenmodellierung]**, **[!UICONTROL Data Management]**, **[!UICONTROL Profil-Management]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Datenüberwachung]**, **[!UICONTROL Sandbox-Administration]**, **[!UICONTROL Ziele&lt;a1 3/>,**[!UICONTROL  Dateneinbettung ]**,**[!UICONTROL  Data Science Workspace ]**,**[!UICONTROL  Abfrage Service ]**und**[!UICONTROL  Datenverwaltung ]**.]** |
| Zugriff auf Sandboxes | Die Registerkarte **[!UICONTROL Berechtigungen]** in einem [!DNL Platform]-Profil kann Benutzern Zugriff auf bestimmte Sandboxen gewähren. Zusätzliche Informationen finden Sie im Abschnitt zu [Sandboxes](#sandboxes) unten. |

Weiterführende Informationen finden Sie unter [Zugriffskontrolle – Übersicht](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] ist ein in  [!DNL Experience Platform]integrierte Anwendungsdienst. Damit können Sie [!DNL Platform] nutzen, um Ihren Kunden das beste Angebot und Erlebnis über alle Berührungspunkte zur richtigen Zeit bereitzustellen.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Zentralisierte Angebot-Bibliothek | Die Oberfläche, auf der Sie die verschiedenen Elemente erstellen und verwalten, aus denen Ihre Angebot bestehen, und deren Regeln und Einschränkungen definieren. |
| Angebot-Entscheidungsmodul | Die Angebot Decision Engine nutzt [!DNL Platform]-Daten und [!DNL Real-time Customer Profiles] zusammen mit der Angebot-Bibliothek, um den richtigen Zeitpunkt, Kunden und Kanal für die Bereitstellung der Angebot festzulegen. |

Weitere Informationen finden Sie in der [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=de) Dokumentation.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] wurde entwickelt, um Anwendungen für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und implementieren, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. [!DNL Experience Platform] stellt Sandboxes bereit, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Produktions-Sandbox | [!DNL Experience Platform] stellt eine einzelne Produktions-Sandbox bereit, die weder gelöscht noch zurückgesetzt werden kann. Die Gesamtzahl der verfügbaren Sandboxen, Produktion und Nichtproduktion wird durch die erworbene Lizenz bestimmt. |
| Nicht-Produktions-Sandboxes | Für eine einzelne [!DNL Platform]-Instanz können mehrere Sandboxen ohne Produktionscharakter erstellt werden, mit denen Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen können, ohne die Produktionssandbox zu beeinträchtigen. |
| Sandbox-Wechsler | In der Benutzeroberfläche [!DNL Experience Platform] können Sie mit dem Sandbox-Umschalter in der oberen linken Ecke des Bildschirms über ein Dropdown-Menü zwischen verfügbaren Sandboxen wechseln. Der Sandbox-Umschalter bietet außerdem eine Suchfunktion, mit der Sie durch verfügbare Sandboxen filtern können. |
| `x-sandbox-name`-Kopfzeile | Alle Aufrufe von APIs für [!DNL Experience Platform] müssen jetzt die neue `x-sandbox-name`-Kopfzeile enthalten, deren Wert auf das `name`-Attribut der Sandbox verweist, in der der Vorgang ausgeführt wird. |

Weiterführende Informationen finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten dem Experience Data Model (XDM) zuzuordnen, umzuformen und zu validieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Iterative Operationen | [!DNL Data Prep] Mapper unterstützt jetzt die Durchführung iterativer Vorgänge in einer Hierarchie. |
| Mapper-Funktion | [!DNL Data Prep] Mapper hat jetzt die Möglichkeit, ein Attribut aus der Quelle  **** nicht in die Zielgruppe XDM zu kopieren. |

Weitere Informationen finden Sie unter [[!DNL Data Prep] overview](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace verwendet maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Data Science Workspace ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen. Data Science Workspace erreicht dies unter anderem durch die Verwendung von [!DNL JupyterLab]. [!DNL JupyterLab] ist eine Web-basierte Benutzeroberfläche für [[!DNL Project Jupyter]](https://jupyter.org/) und ist eng in Adobe Experience Platform integriert. Es bietet eine interaktive Entwicklungs-Umgebung für Datenwissenschaftler, mit [!DNL Jupyter]-Notebooks, -Code und -Daten zu arbeiten.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| [!DNL JupyterLab] Rezept-Builder-Vorlage | Verwendung der Notebook-zu-Rezept-Anforderungen und Versionen aktualisiert. [!DNL Python] Das ML Runtime-Basisbild wurde aktualisiert und verwendet nun ausschließlich  [!DNL Python] 3.6.7 und eine  [!DNL Conda] Umgebung. |

Weitere Informationen finden Sie im Dokument [Erstellen eines Skripts mit Jupyter-Notebooks](../../data-science-workspace/jupyterlab/create-a-recipe.md).

## [!DNL Destinations] Dienst {#destinations}

In der [ Echtzeit-Kundendatenplattform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner auf nahtlose Weise aktivieren.

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| Klammern | Braze ist eine umfassende Kundenbindungsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht. |
| Microsoft Bing | Das Microsoft Bing-Ziel unterstützt Sie beim Ausführen von Retargeting und der Audience zielgerichteter digitaler Kampagnen in der Microsoft Display-Werbung. |
| The Trade Desk | Der Trade Desk ist eine Selbstbedienungsplattform für Anzeigenkäufer, mit der sie zielgerichtete digitale Kampagnen über Display-, Video- und mobile Inventurquellen hinweg ausführen können. |

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| UX-Updates zu Zieldetails | Der CDP-Zielarbeitsablauf in Echtzeit umfasst jetzt die Inline-Überwachung, damit Sie sehen können, welche Batch-Aktivierungen erfolgreich waren. Diese Funktion ermöglicht es Benutzern, Probleme direkt im Arbeitsablauf für Batch-Ziele über Warnungen und ein Dashboard zur Überwachung von Fehlern in der Verarbeitungspipeline zu beheben. |
| Dateiverschlüsselung | Bei dateibasierten Zielen können Benutzer ihren exportierten Dateien nun Verschlüsselung hinzufügen. |
| Dateiplanung | Sowohl für E-Mail- als auch für Cloud-Datenspeicherung-Ziele können Benutzer einen einmaligen Export erstellen oder tägliche Schnappschüsse erstellen. |
| Obligatorische Felder | Benutzer können Felder als Pflichtfelder markieren, wobei sichergestellt wird, dass nur Felder exportiert werden, die das Pflichtfeld enthalten. |

Weiterführende Informationen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Intelligent Services {#intelligent-services}

Mit Intelligent Services können Marketing-Analysten und -Experten die Vorteile von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen nutzen. So können Marketing-Analysten mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für die Anforderungen der Firma erstellen, ohne dass hierfür Kenntnisse aus der Datenwissenschaft erforderlich ist.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Dataset Consumer Experience Ereignisses (CEE) | Das Erstellen eines CEE-Datensatzes unterstützt jetzt das Hinzufügen von Identitätsfeldern zum Datensatz mit dem Schema-Editor. Attribution AI und Customer AI verwenden die primäre Identität zur Kombination von Ereignissen. |

Weitere Informationen finden Sie im Abschnitt [Hinzufügen von Identitätsfeldern zu einem Datensatz](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) im Handbuch zur Datenvorbereitung für intelligente Dienste.

### Attribution AI

Attribution AI als Teil von Intelligent Services ist ein algorithmischer Zuordnungsdienst mit mehreren Kanälen, der den Einfluss und die inkrementelle Auswirkung von Kundeninteraktionen auf bestimmte Ergebnisse berechnet.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Datenquellenlink | Der Link zur ursprünglichen Datensatzquelle kann angezeigt und von der rechten Leiste einer ausgewählten Dienstinstanz aus navigiert werden. |
| Instanzname bearbeiten | Sie können jetzt den Namen einer vorhandenen Attribution AI-Instanz ändern. |
| Kloninstanz | Kopiert die derzeit ausgewählte Dienstinstanz-Einrichtung und lässt Änderungen zu. |
| Instanzkonfigurationsparameter ändern | Sie können jetzt die Konfiguration einer vorhandenen Attribution AI-Instanz ändern, wenn diese noch nicht mit der Bewertung begonnen hat. |
| Einmalig | Sie können jetzt Ad-hoc-Modellbewertungen in Ihren Attribution AI-Instanzen Trigger erstellen. |
| Durch Spalten weiterleiten | Sie können jetzt zusätzliche Spalten konfigurieren, die zu den Rohdaten für das Ausgabeergebnis hinzugefügt werden, um zusätzliche Dimensionen zu BI-Ansichten hinzuzufügen. |
| Instanz-Aktivierung und Deaktivierung der Aktivierung | Sie können jetzt die geplante Modellschulung und -bewertung Ihrer Attribution AI-Instanzen aktivieren und deaktivieren. |
| Berechtigungsverfolgung | Sie können die Gesamtanzahl der von Ihrem Konto verwendeten Zuordnungseinblicke im Container Instanz erstellen ermitteln. |
| Touchpoint-Aufschlüsselung nach Position | Ein neues Erkennungsdiagramm, das eine Analyse von Touchpoints nach Konversionspfaden bereitstellt. |
| Top-Umrechnungspfade | Ein neues Einblicke-Diagramm auf der Registerkarte &quot;Analyse&quot;des Pfads. Das Diagramm enthält eine Liste der fünf wichtigsten Umrechnungspfade, die die Sequenz der Marketing-Kanal-Touchpoints anzeigen, die zu den meisten Umrechnungen führten. |
| Touchpoint-Effektivität | Bietet ausführliche Einblicke in die drei wichtigsten Variablen, mit denen Ihr Modell die Touchpoint-Effektivität misst. Bei den Variablen handelt es sich um das Verhältnis zwischen berührten positiven und negativen Pfaden, Touchpoint-Effizienz und Touchpoint-Lautstärke. |

Weitere Informationen finden Sie unter [Übersicht über Attribution AIS](../../intelligent-services/attribution-ai/overview.md).

### Customer AI

Customer AI bietet Marketing-Experten als Teil von Intelligent Services die Möglichkeit, Kundenvorhersagen auf individueller Ebene mit Erklärungen zu erstellen. Mithilfe von Einflussfaktoren kann Customer AI vorhersagen, was ein Kunde wahrscheinlich tun wird und warum. Darüber hinaus können Marketing-Experten von Prognosen und Einblicken durch Customer AI profitieren, um Kundenerlebnisse durch Bereitstellung der am besten geeigneten Angebote und Botschaften zu personalisieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Datenquellenlink | Der Link zur ursprünglichen Datensatzquelle kann angezeigt und von der rechten Leiste einer ausgewählten Dienstinstanz aus navigiert werden. |
| Instanzname bearbeiten | Sie können den Namen einer vorhandenen Kunden-AI-Instanz ändern. |
| Instanzkonfigurationsparameter ändern | Sie können jetzt die Konfiguration einer vorhandenen Kunden-AI-Instanz ändern, wenn noch keine Bewertung gestartet wurde. |
| Kloninstanz | Kopiert die derzeit ausgewählte Dienstinstanz-Einrichtung und lässt Änderungen zu. |
| Berechtigungsverfolgung | Sie können die Gesamtanzahl der Profil, die von der Kunden-API für Ihr Konto bewertet wurden, im Container Instanz erstellen ermitteln. |
| Prognoseziel | Die Flexibilität bei der Erstellung eines Prognoseziels wurde durch neue Optionen erhöht, um vorherzusagen, ob etwas &quot;eintritt&quot;oder &quot;nicht eintritt&quot;. Darüber hinaus wurden die Optionen hinzugefügt, mit denen vorhergesagt werden kann, ob &quot;alle&quot;oder &quot;eines der&quot;Ereignis bei Verwendung mehrerer Ereignis auftreten. |
| Drilldown für Einflussfaktoren | Propensity Top-Einflussfaktor-Behälter enthalten jetzt Drilldowns. Drilldowns sind eine tiefer gehende Zusammenfassung der Werte für jeden der wichtigsten einflussreichsten Faktoren in einem Tendenzbehälter. |

Weitere Informationen finden Sie unter [Übersicht über die Kundentelefonie](../../intelligent-services/customer-ai/overview.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen und anderen Kanälen miteinander kombiniert. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten zu einer einheitlichen Ansicht zusammenzuführen, die Ihnen einen umsetzbaren Zeitstempel für jede Kundeninteraktion bietet.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Arbeitsablauf für Zusammenführungsrichtlinien aktualisiert | Plattform hat die Konfiguration der Richtlinie zum Zusammenführen zu einem neuen schrittweisen Arbeitsablauf aktualisiert. Dieser Arbeitsablauf ermöglicht es den Benutzern, Datenfragmente aus mehreren Profil-Datensätzen zusammenzuführen und die Priorität für die Zusammenführung der Daten in diesen Datensätzen festzulegen, um eine umfassende Ansicht der einzelnen Daten zu erstellen. Die Benutzer können ausgewählte XDM-Profil-Datensätze zusammenführen, indem sie die entsprechende Zusammenführungsmethode (mit Zeitstempel sortiert oder mit Dataset-Priorität) auswählen und ExperienceEvent-Datensätze an die Profil-Datasets anhängen. |
| Vereinigung Schema Ansicht | In der Benutzeroberfläche &quot;Experience Platform&quot;können Benutzer leichter Informationen zu allen Schemas und Datensätzen finden, die zum Schema der Vereinigung beitragen, sowie zu Oberflächenattributen wie Identitäts- und Beziehungsfeldern. Diese Updates verbessern die Fehlerbehebung und die Überprüfung der ordnungsgemäßen Konfiguration von Profilen, der richtigen Zuordnung von Identitäten und der erfolgreichen Erfassung von Daten. |

Weitere Informationen zum Echtzeit-Profil von Kunden, einschließlich Schulungen und Best Practices für die Arbeit mit [!DNL Profile]-Daten, finden Sie im [Überblick über das Echtzeit-Profil von Kunden](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe der [!DNL Platform]-Dienste strukturieren, beschriften und erweitern können. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Quellen**

| Funktion | Beschreibung |
| ------- | ----------- |
| [!DNL Shopify] | Sie können [!DNL Shopify] jetzt mit [!DNL Experience Platform] über die [!DNL Flow Service]-API oder die Benutzeroberfläche verbinden. Weitere Informationen finden Sie unter [Übersicht über den Shopify Connector](../../sources/connectors/ecommerce/shopify.md). |

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbindungsinformationen aktualisieren | Sie können nun die Namen, Beschreibungen und Anmeldeinformationen vorhandener Batch-Verbindungen mit der API und der Benutzeroberfläche aktualisieren. [!DNL Flow Service] Weitere Informationen finden Sie im Lernprogramm zu [Aktualisieren von Verbindungen mit der Flow Service API](../../sources/tutorials/api/update.md) und [Bearbeiten von Kontodetails mithilfe der Benutzeroberfläche](../../sources/tutorials/ui/monitor.md). |
| Verbindungen löschen | Stapelverbindungen, die Fehler enthalten oder unnötig geworden sind, können jetzt mit der API und der Benutzeroberfläche gelöscht werden. [!DNL Flow Service] Weitere Informationen finden Sie im Lernprogramm zum Löschen von Verbindungen mit der Flow Service API](../../sources/tutorials/api/delete.md) und zum Löschen von Konten mit der Benutzeroberfläche](../../sources/tutorials/ui/delete-accounts.md).[[ |
| Hierarchische Zuordnung | Sie können eine hierarchische Quelldatei, wie JSON oder Parquet, während des Datenerfassungsprozesses Vorschau haben. Weitere Informationen finden Sie im Lernprogramm unter [Konfigurieren eines Datenflusses für Cloud-Datenspeicherung-Connectors in der Benutzeroberfläche](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |
| API-Unterstützung für die Zuordnung in Streaming-Quellen | Sie können jetzt APIs verwenden, um Zuordnungsfunktionen mit Streaming-Quellen auszuführen. |
| API-Unterstützung für benutzerdefinierte Trennzeichen für Cloud-Datenspeicherung-Quellen | Sie können jetzt nicht CSV-getrennte Datenspeicherung mit Cloud-Quellen erfassen. Sie können beliebige Trennzeichen für einzelne Spalten verwenden, z. B. Tabulatoren, Kommas, Senkrechtstriche oder Hashwerte, um einfache Dateien in einem beliebigen Format zu erfassen. |
| Sandbox-Unterstützung für Adobe Audience Manager Connector | Der Audience Manager-Anschluss ist jetzt sandbox-fähig. Benutzer können den Connector aktivieren, um Audience Manager-Datensätze an die Sandbox ihrer Wahl zu leiten (einschließlich Nicht-Produktions-Sandboxes). Die Konfiguration ist auf eine Sandbox pro IMS Org beschränkt. |
| UX-Verbesserungen | Dateibasierte Erfassung ist jetzt über den Quellkatalog verfügbar. |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).