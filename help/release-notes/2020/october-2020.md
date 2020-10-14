---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform Oktober 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: fc1174c8435c1afc3c58dd748daf89f387a19980
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 31%

---


# Adobe Experience Platform – Versionshinweise

**Release-Datum: 14. Oktober 2020**

- [Datenvorgabe](#data-prep)
- [Echtzeit-Kundenprofil](#profile)
- [Segmentierungsdienst](#segmentation)
- [Quellen](#sources)

## Datenvorgabe {#data-prep}

Data Prep ermöglicht es Datenentwicklern, Daten dem Experience Data Model (XDM) zuzuordnen, umzuformen und zu validieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| `is_set` durchführen | Mit der `is_set` Funktion können Sie überprüfen, ob ein Attribut in den Quelldaten vorhanden ist. `is_set` kann in Verbindung mit `is_empty` der Überprüfung sowohl des Vorkommens des Attributs als auch des Vorkommens des Werts innerhalb des Attributs verwendet werden. |
| `get_values` durchführen | Die `get_values` Funktion ermöglicht es Ihnen, die Werte aus der Eingabemap für einen beliebigen Schlüssel abzurufen. |

For more information, please read the [Data Prep overview](../../data-prep/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten zu einer einheitlichen Ansicht zusammenzuführen, die Ihnen einen umsetzbaren Zeitstempel für jede Kundeninteraktion bietet.

| Funktion | Beschreibung |
| ------- | ----------- |
| API-Ergänzungen zur Profil-Vorschau | Die Profil Vorschau API (`/previewsamplestatus`) bietet jetzt die Möglichkeit, eine Aufschlüsselung der gesamten Profil-Fragmente in Ihrer IMS-Organisation Ansicht und die Ansicht der Verteilung von Profil-Fragmenten über Identitäts-Namensraum hinweg. |
| Updates der Vereinigung Schema Ansicht | In der Benutzeroberfläche &quot;Experience Platform&quot;können Benutzer leichter Informationen zu allen Schemas und Datensätzen finden, die zum Schema der Vereinigung beitragen, sowie zu Oberflächenattributen wie Identitäts- und Beziehungsfeldern. Diese Updates verbessern die Fehlerbehebung und die Überprüfung der ordnungsgemäßen Konfiguration von Profilen, der richtigen Zuordnung von Identitäten und der erfolgreichen Erfassung von Daten. |

Weitere Informationen [!DNL Real-time Customer Profile]einschließlich Übungen und Best Practices für die Arbeit mit [!DNL Profile] Daten finden Sie in der Übersicht über das [Echtzeit-Kundenerlebnis](../../profile/home.md).

## Segmentierungsdienst {#segmentation}

Adobe Experience Platform Segmentation Service provides a user interface and RESTful API that allows you to build segments and generate audiences from your [!DNL Real-time Customer Profile] data. These segments are centrally configured and maintained on [!DNL Platform], making them readily accessible by any Adobe application.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Entfernung der Segmentierungsgrenze für Streaming | Die Beschränkung für den Lookback-Zeitraum von sieben Tagen wurde entfernt. |

For more information on [!DNL Segmentation Service], please see the [Segmentation overview](../../segmentation/home.md)

## Quellen {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Hierarchische Zuordnung | Sie können eine hierarchische Quelldatei, wie JSON oder Parquet, während des Datenerfassungsprozesses Vorschau haben. |
| SSH-Authentifizierungsunterstützung für SFTP | Sie können Ihr SFTP-Konto mit [!DNL Platform] RSA/DSA Open SSH-Schlüsseln verbinden. See the [SFTP overview](../../sources/connectors/cloud-storage/ftp-sftp.md) for more information. |
| UX-Verbesserungen | Sie können Ihren Datensatz [!DNL Profile] während der Datenerfassung aktivieren. Weitere Informationen finden Sie im Tutorial zum DataFlow-Arbeitsablauf [für die](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) Cloud-Datenspeicherung. |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).