---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform Oktober 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: ab87cac94ae69acde3be75ae95b11cf003a274e9
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 35%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: Oktober 2020**

- [Datenvorgabe](#data-prep)
- [Quellen](#sources)

## Datenvorgabe {#data-prep}

Data Prep ermöglicht es Datenentwicklern, Daten dem Experience Data Model (XDM) zuzuordnen, umzuformen und zu validieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| `is_set` durchführen | Mit der `is_set` Funktion können Sie überprüfen, ob ein Attribut in den Quelldaten vorhanden ist. `is_set` kann in Verbindung mit `is_empty` der Überprüfung sowohl des Vorkommens des Attributs als auch des Vorkommens des Werts innerhalb des Attributs verwendet werden. |
| `get_values` durchführen | Die `get_values` Funktion ermöglicht es Ihnen, die Werte aus der Eingabemap für einen beliebigen Schlüssel abzurufen. |

For more information, please read the [Data Prep overview](../../data-prep/home.md).

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