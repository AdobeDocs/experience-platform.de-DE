---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform, 11. November 2020
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: d6b603e2918b502635b11fb1aa693a4b4311c125
workflow-type: tm+mt
source-wordcount: '2126'
ht-degree: 24%

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

Weitere Informationen finden Sie im Handbuch zur Migration von [Data Lake](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] nutzt [Adobe Admin Console](https://adminconsole.adobe.com)-Produktprofile, um Benutzer mit Berechtigungen und Sandboxes zu verknüpfen. Berechtigungen steuern den Zugriff auf verschiedene Platform-Funktionen, einschließlich Datenmodellierung, Profil-Management und Sandbox-Verwaltung.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Berechtigungen | In the [!DNL Admin Console], the  tab within a [!DNL Platform] product profile allows you customize which [!DNL Platform] capabilities are available for the users attached to that profile. Zu den verfügbaren Kategorien für Berechtigungen gehören: **[!UICONTROL Datenmodellierung]**, **[!UICONTROL Data Management]**, **[!UICONTROL Profil-Management]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Datenüberwachung]**, **[!UICONTROL Sandbox-Administration]**********************,Data Ingestion, Data Science Workspace,Abfrage Service, und Data Governance. |
| Zugriff auf Sandboxes | The **[!UICONTROL Permissions]** tab within a [!DNL Platform] product profile can grant users access to specific sandboxes. Zusätzliche Informationen finden Sie im Abschnitt zu [Sandboxes](#sandboxes) unten. |

Weiterführende Informationen finden Sie unter [Zugriffskontrolle – Übersicht](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] ist ein in [!DNL Experience Platform]integrierte Anwendungsdienst. It allows you to leverage [!DNL Platform] to deliver the best offer and experience to your customers across all touch points at the right time.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Zentralisierte Angebot-Bibliothek | Die Oberfläche, auf der Sie die verschiedenen Elemente erstellen und verwalten, aus denen Ihre Angebot bestehen, und deren Regeln und Einschränkungen definieren. |
| Angebot-Entscheidungsmodul | The Offer Decision Engine leverages [!DNL Platform] data and [!DNL Real-time Customer Profiles], along with the Offer Library, in order to select the right time, customers and channels to which offers will be delivered. |

Weitere Informationen finden Sie in der [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=de) Dokumentation.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] wurde entwickelt, um Anwendungen für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und implementieren, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. In order to address this need, [!DNL Experience Platform] provides sandboxes which partition a single [!DNL Platform] instance into separate virtual environments to help develop and evolve digital experience applications.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Produktions-Sandbox | [!DNL Experience Platform] stellt eine einzelne Produktions-Sandbox bereit, die weder gelöscht noch zurückgesetzt werden kann. Die Gesamtzahl der verfügbaren Sandboxen, Produktion und Nichtproduktion wird durch die erworbene Lizenz bestimmt. |
| Nicht-Produktions-Sandboxes | Multiple non-production sandboxes can be created for a single [!DNL Platform] instance, allowing you to test features, run experiments, and make custom configurations without impacting your production sandbox. |
| Sandbox-Wechsler | In the [!DNL Experience Platform] user interface, the sandbox switcher in the top-left corner of the screen allows you to switch between available sandboxes through a dropdown menu. Der Sandbox-Umschalter bietet außerdem eine Suchfunktion, mit der Sie durch verfügbare Sandboxen filtern können. |
| `x-sandbox-name`-Kopfzeile | All calls to [!DNL Experience Platform] APIs must now include the new `x-sandbox-name` header, whose value references the `name` attribute of the sandbox the operation will take place in. |

Weiterführende Informationen finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten dem Experience Data Model (XDM) zuzuordnen, umzuformen und zu validieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Iterative Operationen | [!DNL Data Prep] Mapper unterstützt jetzt die Durchführung iterativer Vorgänge in einer Hierarchie. |
| Mapper-Funktion | [!DNL Data Prep] Mapper kann jetzt **kein** Attribut aus der Quelle in die Zielgruppe XDM kopieren. |

For more information, please see the [[!DNL Data Prep] overview](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace verwendet maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Data Science Workspace ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen. Data Science Workspace erreicht dies unter anderem durch den Einsatz von [!DNL JupyterLab]. [!DNL JupyterLab] ist eine Web-basierte Benutzeroberfläche für [[!DNL Project Jupyter]](https://jupyter.org/) und ist eng in Adobe Experience Platform integriert. It provides an interactive development environment for data scientists to work with [!DNL Jupyter] notebooks, code, and data.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| [!DNL JupyterLab] Rezept-Builder-Vorlage | Verwendung der Notebook-zu-Rezept-Anforderungen und Versionen aktualisiert. [!DNL Python] Das ML Runtime-Basisbild wurde aktualisiert und verwendet nun ausschließlich [!DNL Python] 3.6.7 und eine [!DNL Conda] Umgebung. |

Weitere Informationen finden Sie im Dokument zum [Erstellen eines Skripts mit Jupyter-Notebooks](../../data-science-workspace/jupyterlab/create-a-recipe.md).

## [!DNL Destinations] Dienst {#destinations}

In der [ Echtzeit-Kundendatenplattform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner auf nahtlose Weise aktivieren.

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| Microsoft Bing | Das Microsoft Bing-Ziel unterstützt Sie beim Ausführen von Retargeting und der Audience zielgerichteter digitaler Kampagnen in der Microsoft Display-Werbung. |
| The Trade Desk | Der Trade Desk ist eine Selbstbedienungsplattform für Anzeigenkäufer, mit der sie zielgerichtete digitale Kampagnen über Display-, Video- und mobile Inventurquellen hinweg ausführen können. |

<!-- | Braze | Braze is a comprehensive customer engagement platform that power relevant and memorable experiences between customers and the brands they love. |  -->

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| UX-Updates zu Zieldetails | Der CDP-Zielarbeitsablauf in Echtzeit umfasst jetzt die Inline-Überwachung, damit Sie sehen können, welche Batch-Aktivierungen erfolgreich waren. Diese Funktion ermöglicht es Benutzern, Probleme direkt im Arbeitsablauf für Batch-Ziele über Warnungen und ein Dashboard zur Überwachung von Fehlern in der Verarbeitungspipeline zu beheben. |
| Obligatorische Felder | Benutzer können Felder als Pflichtfelder markieren, wobei sichergestellt wird, dass nur Felder exportiert werden, die das Pflichtfeld enthalten. |

<!-- | File scheduling | For both email based and cloud storage destinations, users can create a one-time export or create daily snapshots. |
| File encryption | For file based destinations, users can now add encryption to their exported files. | -->

Weiterführende Informationen finden Sie in der [Übersicht zu Zielen](../../rtcdp/destinations/destinations-overview.md).

## Intelligent Services {#intelligent-services}

Mit Intelligent Services können Marketing-Analysten und -Experten die Vorteile von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen nutzen. So können Marketing-Analysten mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für die Anforderungen der Firma erstellen, ohne dass hierfür Kenntnisse aus der Datenwissenschaft erforderlich ist.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Dataset Consumer Experience Ereignisses (CEE) | Das Erstellen eines CEE-Datensatzes unterstützt jetzt das Hinzufügen von Identitätsfeldern zum Datensatz mit dem Schema-Editor. Attribution AI und Customer AI verwenden die primäre Identität zur Kombination von Ereignissen. |

Weitere Informationen finden Sie im Abschnitt zum [Hinzufügen von Identitätsfeldern zu einem Datensatz](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) im Vorbereitungshandbuch für intelligente Dienste.

### Attribution AI

Attribution AI als Teil von Intelligent Services ist ein algorithmischer Zuordnungsdienst mit mehreren Kanälen, der den Einfluss und die inkrementelle Auswirkung von Kundeninteraktionen auf bestimmte Ergebnisse berechnet.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Datenquellenlink | Der Link zur ursprünglichen Datensatzquelle kann angezeigt und von der rechten Leiste einer ausgewählten Dienstinstanz aus navigiert werden. |
| Instanzname bearbeiten | Sie können jetzt den Namen einer vorhandenen Attribution AI-Instanz ändern. |
| Kloninstanz | Kopiert die derzeit ausgewählte Dienstinstanz-Einrichtung und lässt Änderungen zu. |
| Instanzkonfigurationsparameter ändern | Sie können jetzt die Konfiguration einer vorhandenen Attribution AI-Instanz ändern, wenn diese noch nicht mit der Bewertung begonnen hat. |
| Einmalig | Sie können jetzt Ad-hoc-Modellbewertungen in Ihren Attribution AI-Instanzen auslösen. |
| Durch Spalten weiterleiten | Sie können jetzt zusätzliche Spalten konfigurieren, die zu den Rohdaten für das Ausgabeergebnis hinzugefügt werden, um zusätzliche Dimensionen zu BI-Ansichten hinzuzufügen. |
| Instanz-Aktivierung und Deaktivierung der Aktivierung | Sie können jetzt die geplante Modellschulung und -bewertung Ihrer Attribution AI-Instanzen aktivieren und deaktivieren. |
| Berechtigungsverfolgung | Sie können die Gesamtanzahl der von Ihrem Konto verwendeten Zuordnungseinblicke im Container Instanz erstellen ermitteln. |
| Touchpoint-Aufschlüsselung nach Position | Ein neues Erkennungsdiagramm, das eine Analyse von Touchpoints nach Konversionspfaden bereitstellt. |
| Top-Umrechnungspfade | Ein neues Einblicke-Diagramm auf der Registerkarte &quot;Analyse&quot;des Pfads. Das Diagramm enthält eine Liste der fünf wichtigsten Umrechnungspfade, die die Sequenz der Marketing-Kanal-Touchpoints anzeigen, die zu den meisten Umrechnungen führten. |
| Touchpoint-Effektivität | Bietet ausführliche Einblicke in die drei wichtigsten Variablen, mit denen Ihr Modell die Touchpoint-Effektivität misst. Bei den Variablen handelt es sich um das Verhältnis zwischen berührten positiven und negativen Pfaden, Touchpoint-Effizienz und Touchpoint-Lautstärke. |

For more information, please read the [Attribution AI overview](../../intelligent-services/attribution-ai/overview.md).

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

For more information, please read the [Customer AI overview](../../intelligent-services/customer-ai/overview.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen und anderen Kanälen miteinander kombiniert. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten zu einer einheitlichen Ansicht zusammenzuführen, die Ihnen einen umsetzbaren Zeitstempel für jede Kundeninteraktion bietet.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Arbeitsablauf für Zusammenführungsrichtlinien aktualisiert | Plattform hat die Konfiguration der Richtlinie zum Zusammenführen zu einem neuen schrittweisen Arbeitsablauf aktualisiert. Dieser Arbeitsablauf ermöglicht es den Benutzern, Datenfragmente aus mehreren Profil-Datensätzen zusammenzuführen und die Priorität für die Zusammenführung der Daten in diesen Datensätzen festzulegen, um eine umfassende Ansicht der einzelnen Daten zu erstellen. Die Benutzer können ausgewählte XDM-Profil-Datensätze zusammenführen, indem sie die entsprechende Zusammenführungsmethode (mit Zeitstempel sortiert oder mit Dataset-Priorität) auswählen und ExperienceEvent-Datensätze an die Profil-Datasets anhängen. |
| Vereinigung Schema Ansicht | In der Benutzeroberfläche &quot;Experience Platform&quot;können Benutzer leichter Informationen zu allen Schemas und Datensätzen finden, die zum Schema der Vereinigung beitragen, sowie zu Oberflächenattributen wie Identitäts- und Beziehungsfeldern. Diese Updates verbessern die Fehlerbehebung und die Überprüfung der ordnungsgemäßen Konfiguration von Profilen, der richtigen Zuordnung von Identitäten und der erfolgreichen Erfassung von Daten. |

Weitere Informationen zum Echtzeit-Profil von Kunden, einschließlich Übungen und Best Practices für die Arbeit mit [!DNL Profile] Daten, finden Sie in der Übersicht über das [Echtzeit-Profil](../../profile/home.md)von Kunden.

## [!DNL Sources] {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Quellen**
| Funktion | Beschreibung |
| — | — |
| [!DNL Shopify] | Sie können jetzt eine Verbindung [!DNL Shopify] mit [!DNL Experience Platform] der [!DNL Flow Service] API oder der Benutzeroberfläche herstellen. See the [Shopify connector overview](../../sources/connectors/ecommerce/shopify.md) for more information. |

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbindungsinformationen aktualisieren | Sie können nun die Namen, Beschreibungen und Anmeldeinformationen vorhandener Batch-Verbindungen mit der [!DNL Flow Service] API und der Benutzeroberfläche aktualisieren. Weitere Informationen finden Sie im Lernprogramm zum [Aktualisieren von Verbindungen mithilfe der Flow Service API](../../sources/tutorials/api/update.md) und zum [Bearbeiten von Kontodetails mithilfe der Benutzeroberfläche](../../sources/tutorials/ui/monitor.md). |
| Verbindungen löschen | Stapelverbindungen, die Fehler enthalten oder unnötig geworden sind, können jetzt mit der [!DNL Flow Service] API und der Benutzeroberfläche gelöscht werden. Weitere Informationen finden Sie im Lernprogramm zum [Löschen von Verbindungen mithilfe der Flow Service API](../../sources/tutorials/api/delete.md) und zum [Löschen von Konten über die Benutzeroberfläche](../../sources/tutorials/ui/delete-accounts.md). |
| Hierarchische Zuordnung | Sie können eine hierarchische Quelldatei, wie JSON oder Parquet, während des Datenerfassungsprozesses Vorschau haben. Weitere Informationen finden Sie im Lernprogramm zum [Konfigurieren eines Datenflusses für Cloud-Datenspeicherung-Connectors in der Benutzeroberfläche](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) . |
| API-Unterstützung für die Zuordnung in Streaming-Quellen | Sie können jetzt APIs verwenden, um Zuordnungsfunktionen mit Streaming-Quellen auszuführen. |
| API-Unterstützung für benutzerdefinierte Trennzeichen für Cloud-Datenspeicherung-Quellen | Sie können jetzt nicht CSV-getrennte Datenspeicherung mit Cloud-Quellen erfassen. Sie können beliebige Trennzeichen für einzelne Spalten verwenden, z. B. Tabulatoren, Kommas, Senkrechtstriche oder Hashwerte, um einfache Dateien in einem beliebigen Format zu erfassen. |
| Sandbox-Unterstützung für Adobe Audience Manager Connector | Der Audience Manager-Anschluss ist jetzt sandbox-fähig. Benutzer können den Connector aktivieren, um Audience Manager-Datensätze an die Sandbox ihrer Wahl zu leiten (einschließlich Nicht-Produktions-Sandboxes). Die Konfiguration ist auf eine Sandbox pro IMS Org beschränkt. |
| UX-Verbesserungen | Dateibasierte Erfassung ist jetzt über den Quellkatalog verfügbar. |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).