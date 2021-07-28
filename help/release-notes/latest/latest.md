---
title: Adobe Experience Platform – Versionshinweise
description: Experience Platform - Versionshinweise für den 28. Juli 2021.
doc-type: release notes
last-update: July 28, 2021
author: ens60013
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: dc01e03975fdda375b31f44edc8459fa32b5a61b
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 65%

---


# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 28. Juli 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Data Science Workspace](#dsw)
- [Experience-Datenmodell (XDM)](#xdm)
- [Quellen](#sources)

## Data Science Workspace {#dsw}

Data Science Workspace nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Data Science Workspace ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Bibliotheks- und Betriebssystem-Updates | Data Science Workspace hat umfangreiche Bibliotheks- und Betriebssystemaktualisierungen vorgenommen, um die Funktionalität und Benutzerfreundlichkeit zu verbessern. Dazu gehören JupyterLab 1.2.20, Python 3.7, Pandas 1.2.4, Tensorflow 2.4.1 mit CUDA 11- und CUDNN 8-Unterstützung und mehr. Informationen zum Anzeigen der verfügbaren Bibliotheken in JupyterLab finden Sie im Abschnitt [Unterstützte Bibliotheken](../../data-science-workspace/jupyterlab/overview.md#supported-libraries) in der JupyterLab Notebook-Übersichtsdokumentation. |

Weitere allgemeine Informationen zu Data Science Workspace finden Sie im Abschnitt [Übersicht über Data Science Workspace](../../data-science-workspace/home.md).

## Experience-Datenmodell (XDM) {#xdm}

Das Experience-Datenmodell (XDM) ist eine Open-Source-Spezifikation, die dazu dient, die Leistung digitaler Erlebnisse zu verbessern. Es bietet gemeinsame Strukturen und Definitionen für Daten in Form von Schemas, die es jeder Anwendung ermöglichen, mit Platform-Diensten zu kommunizieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Filter für die Telekommunikationsbranche | Beim Hinzufügen von Feldergruppen zu einem Schema in der Benutzeroberfläche können Sie jetzt nach der Telekommunikationsbranche filtern. Im [Entitätsdiagramm zur Telekommunikationsbranche (ERD)](../../xdm/schema/industries/telecom.md) finden Sie ein empfohlenes Datenmodell für Telekommunikationsanwendungsfälle. |

Allgemeine Informationen zu XDM in Platform finden Sie in der [XDM-Systemübersicht](../../xdm/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| ------- | ----------- |
| Wechsel von Betaquellen zu allgemeiner Verfügbarkeit | Die folgenden Quellen wurden von der Betaversion auf allgemeine Verfügbarkeit umgestellt: <ul><li>[[!DNL Amazon Redshift]](../../sources/connectors/databases/redshift.md)</li><li>[[!DNL Azure Table Storage]](../../sources/connectors/databases/ats.md)</li><li>[[!DNL PayPal]](../../sources/connectors/payments/paypal.md)</li></ul> |
| [!DNL Salesforce Marketing Cloud] (Beta) | Sie können [!DNL Salesforce Marketing Cloud] jetzt über die [!DNL Flow Service]-API oder die Benutzeroberfläche mit Experience Platform verbinden. Weiterführende Informationen dazu finden Sie unter [[!DNL Salesforce Marketing Cloud] Connectoren – Übersicht](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
