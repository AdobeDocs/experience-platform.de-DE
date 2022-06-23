---
title: Juni 2022 - Adobe Experience Platform-Versionshinweise
description: Die Versionshinweise für Adobe Experience Platform vom Juni 2022.
source-git-commit: 314cd79185748e848bcb06fb21bfe4fea37a8853
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 44%

---

# Adobe Experience Platform – Versionshinweise

**Releasedatum: 22. Juni 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [Query Service](#query-service)
- [Quellen](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen an [!DNL Data Prep] Recommendations | [!DNL Data Prep] Recommendations ist jetzt schlauer und schneller. Neue Validierungsprüfungen reduzieren die häufigsten Zuordnungsfehler erheblich und reduzieren so die Time-to-Value. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu [!DNL Data Prep] finden Sie in der [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## [!DNL Data Science Workspace] {#dsw}

 Data Science Workspace nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Data Science Workspace ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen. Eine der Möglichkeiten, dies mit Data Science Workspace zu erreichen, ist die Verwendung von JupyterLab. JupyterLab ist eine Web-basierte Benutzeroberfläche für <a href="https://jupyter.org/" target="_blank">Project Jupyter</a> und ist eng in Adobe Experience Platform integriert. Sie bietet eine interaktive Entwicklungsumgebung für Datenwissenschaftler, die mit Jupyter-Notebooks, -Code und -Daten arbeiten möchten.

| Funktion | Beschreibung |
| --- | --- |
| JupyterLab Launcher | Der JupyterLab Launcher enthält jetzt Starter für Spark 3.2 Notebooks. Spark 2.4 Notebook-Starter werden jetzt durch Spark 3.2 Notebooks ersetzt und werden Teil dieser Version sein. |
| Spark 3.2 | Neue Scala (Spark)- und PySpark-Rezepte verwenden jetzt Spark 3.2 |
| Kernels | Scala (Spark) Notebooks werden jetzt über den Scala-Kernel erstellt. PySpark-Notebooks werden jetzt über den Python-Kernel erstellt. Der Spark- und PySpark-Kernel sind veraltet und werden in einer nachfolgenden Version entfernt. |
| Rezepte | Neue PySpark- und Spark-Rezepte folgen jetzt dem Docker-Workflow ähnlich wie Python- und R-Rezepte. |

{style=&quot;table-layout:auto&quot;}

Weitere allgemeine Informationen zu Data Science Workspace finden Sie unter [Übersichtsdokumentation](../../data-science-workspace/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ----------- | ----------- |
| (Beta) Destination SDK-Unterstützung für [[!DNL Google Cloud Storage]](../../destinations/destination-sdk/server-and-file-configuration.md#gcs-example) dateibasierte Ziele und [konfigurierbare Dateinamen](../../destinations/destination-sdk/file-based-destination-configuration.md#file-name-configuration). | Sie können jetzt die Destination SDK verwenden, um Google Cloud-Speicher-Ziele zu erstellen und benutzerdefinierte Dateinamen für exportierte Dateien über Dateinamenmakros zu definieren. <br><br> Die Unterstützung für dateibasierte Ziele im Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern. |
| Segmentspalte im Datenfluss führt zu Batch-Zielen aus. | Für Datenflüsse, die zu Batch-Zielen ausgeführt werden, zeigt die Benutzeroberfläche jetzt den Namen des Segments an, das mit jedem Datenfluss verknüpft ist. Mehr dazu [Datenfluss wird zu Batch-Zielen ausgeführt](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations). |

{style=&quot;table-layout:auto&quot;}

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [(Beta) Google Ad Manager 360](../../destinations/catalog/advertising/google-ad-manager-360-connection.md) | Die [!DNL Google Ad Manager 360] Verbindung aktiviert Batch-Upload für [!DNL publisher provided identifiers] (PPID) nach [!DNL Google Ad Manager 360]über [!DNL Google Cloud Storage] <br><br>Dieses Ziel befindet sich derzeit in der Betaversion und steht nur einer begrenzten Anzahl von Kunden zur Verfügung. So fordern Sie Zugriff auf die [!DNL Google Ad Manager 360] Verbindung herstellen, kontaktieren Sie Ihren Kundenbetreuer und geben Sie Ihre [!DNL IMS Organization ID]. |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | Aktivieren Sie Profile für zielgerichtete Media-Umfragen und Feedback-Erfassung, um Kundenanforderungen und Erwartungen besser zu verstehen. |
| [[!DNL Adobe Advertising Cloud DSP]](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | Die Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) Mit dem Ziel können Sie authentifizierte Erstanbietersegmente für zugelassene Advertiser und Benutzer freigeben, damit die Kampagne für DSP aktiviert werden kann. |

{style=&quot;table-layout:auto&quot;}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Data Science Workspace oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Beschriftung von Ad-hoc-Schemata | Verwalten Sie den Zugriff auf vertrauliche Daten, indem Sie Beschriftungen auf Datenfelder von Ad-hoc-Schemata anwenden, die automatisch durch CTAS-Abfragen von Query Service generiert werden. Sie können die Verwendung bestimmter Felder oder Datensätze von Ad-hoc-Schemata einschränken, um den Zugriff auf vertrauliche personenbezogene Daten und persönlich identifizierbare Informationen zu steuern. Mithilfe der attributbasierten Zugriffssteuerungsfunktion können Sie Ad-hoc-Schemafelder über die Platform-Benutzeroberfläche beschriften. |
| `FLATTEN` Einstellung | Wenn Sie über BI-Tools von Drittanbietern eine Verbindung zu einer Datenbank herstellen, wird die `FLATTEN` Durch die Einstellung werden verschachtelte Datenstrukturen in separate Spalten reduziert, wobei der Attributname zum Spaltennamen wird, der die Zeilenwerte enthält. Dies verbessert die Benutzerfreundlichkeit von Ad-hoc-Schemata und verringert den erforderlichen Arbeitsaufwand zum Abrufen, Analysieren, Transformieren und Berichten von Daten in BI-Tools, die keine verschachtelten Datenstrukturen unterstützen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Query Services finden Sie im Abschnitt [Query Service - Übersicht](../../query-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Beta-Version der [!DNL Mixpanel]-Quelle | Sie können jetzt die [!DNL Mixpanel] zur Erfassung von Analysedaten aus Ihrer [!DNL Mixpanel] -Konto auf Experience Platform. Siehe [[!DNL Mixpanel] Quelldokumentation](../../sources/connectors/analytics/mixpanel.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
