---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise zur Experience Platform
doc-type: release notes
last-update: July 15, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 1e420d26f89150999f356f9cf5af94d434076c2b
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 46%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 15. Juli 2020**

Aktualisierungen vorhandener Funktionen in der Adobe Experience Platform:

<!-- - [Data Governance](#governance) -->
- [Echtzeit-Kundenprofil](#profile)
- [Segmentierungsdienst](#segmentation)
- [Quellen](#sources)

<!-- ## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**New features**

| Feature    | Description  |
| -----------| ---------- |
| Automatic policy enforcement in [!DNL Real-time Customer Data Platform] | Data usage policies are now automatically enforced in [!DNL Real-time CDP] when violating actions occur, including activating segments to destinations. When a policy violation is triggered, users get real-time visibility into usage restrictions within the activation workflow, indicating what data they cannot use and why.<br><br>See the section on [enforcing data usage compliance](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance) within the overview on [!DNL Data Governance] in [!DNL Real-time CDP] for more information. |
| Adobe Audience Manager integration | Any segments that are shared with [!DNL Audience Manager] from [!DNL Platform] inherit any applied data usage labels as [!DNL Data Export Controls], and vice versa. See the [!DNL Audience Manager] documentation for specific [mappings between usage labels and Data Export Controls](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep). |
| Custom data usage labels | You can now create custom data usage labels using the Policy Service API or in the UI. See the [labels overview](../../data-governance/labels/overview.md) for more information. |

See the [Data Governance overview](../../data-governance/home.md) for more information on the service.

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform enables you to drive coordinated, consistent, and relevant experiences for your customers no matter where or when they interact with your brand. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] allows you to consolidate your disparate customer data into a unified view offering an actionable, timestamped account of every customer interaction.

**New features**

| Feature | Description |
| ------- | ----------- |
| Data usage policy enforcement | In [!DNL Real-time Customer Data Platform], data usage policy violations are automatically surfaced when a violating action in the [!UICONTROL Profile] workspace is attempted. See the [release notes for Data Governance](#governance) for more information on automatic policy enforcement. | 

-->

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service provides a user interface and RESTful API that allows you to build segments and generate audiences from your [!DNL Real-time Customer Profile] data. These segments are centrally configured and maintained on [!DNL Platform], making them readily accessible by any Adobe application.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Streaming-Segmentierung | Streaming-Segmentierung kann jetzt als Benutzer in ein Segment eingeordnet werden, wenn Daten eingehen, [!DNL Platform]wodurch die Segmentqualifizierungszeit erheblich verkürzt wird. Durch Streaming-Segmentierung wird auch die manuelle Ausführung von Segmentierungsaufträgen erleichtert. |

<!-- | Data usage policy enforcement | In [!DNL Real-time Customer Data Platform], data usage policy violations are automatically surfaced when a violating action in the [!UICONTROL Segments] workspace is attempted. See the [release notes for Data Governance](#governance) for more information on automatic policy enforcement. | -->

For more information on [!DNL Segmentation Service], please see the [Segmentation overview](../../segmentation/home.md)

## Quellen {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten lassen sich aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Experience Platform bietet eine RESTful-API und eine interaktive Benutzeroberfläche, damit Sie für verschiedene Datenanbieter bequem Quellverbindungen einrichten können. Diese Quellverbindungen ermöglichen Ihnen das Authentifizieren und Verbinden mit externen Speichersystemen und CRM-Diensten, das Festlegen von Zeiten für Erfassungsläufe und das Verwalten des Datendurchsatzes bei der Erfassung.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| API- und UI-Unterstützung für das Löschen von Datenflüssen | Datenflüsse, die mit Fehlern gemacht wurden oder unnötig geworden sind, können jetzt über APIs oder über die Benutzeroberfläche gelöscht werden. |
| API- und UI-Unterstützung für einmalige Erfassung | Eine einmalige Erfassung für Datenflüsse, bei der nur das Datum des Beginns angegeben und keine weitere Erfassung geplant ist, kann jetzt über APIs oder über die Benutzeroberfläche ausgeführt werden. |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
