---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform für den 31. März 2021.
doc-type: release notes
last-update: March 31, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 58382528cc787e8d2005c8c322904266880ad0b9
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 44%

---


# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 31. März 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Sandboxes]](#sandboxes)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten dem Experience Data Model (XDM) zuzuordnen, umzuformen und zu validieren.

| Funktion | Beschreibung |
| ------- | ----------- |
| `add_to_array` durchführen | Die Funktionalität zur Unterstützung von Arrays als Parameter wurde aktualisiert. |
| `to_array` durchführen | Die Funktionalität zur Unterstützung von Objekten als Parameter wurde aktualisiert. |

Weitere Informationen finden Sie unter [[!DNL Data Prep] overview](../../data-prep/home.md).

## [!DNL Sandboxes] {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und implementieren, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss.

Darum stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

| Funktion | Beschreibung |
| ------- | ----------- |
| (Beta) Mehrere Produktions-Sandboxen | Sie können jetzt mehrere Produktions-Sandboxen in Ihrem IMS-Org erstellen und verwalten und spezifische Produktions-Sandboxes unterschiedlichen Geschäftsfeldern, Marken, Projekten oder Regionen zuweisen. Weitere Informationen finden Sie in den Tutorials zum Erstellen einer Produktions-Sandbox [in der Benutzeroberfläche](../../sandboxes/ui/user-guide.md) oder [mit der API](../../sandboxes/api/create-sandbox.md). |

Weitere Informationen zu Sandboxes finden Sie unter [Übersicht über Sandboxes](../../sandboxes/home.md).

## Segmentierungs-Service {#segmentation}

Der Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und Audiencen aus Ihren [!DNL Real-time Customer Profile]-Daten generieren können. Diese Adoben werden zentral auf [!DNL Platform] konfiguriert und gepflegt, sodass sie für jede Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| (Beta) Edge-Segmentierung | Bei der Edge-Segmentierung werden Segmente in Echtzeit ausgewertet, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht. Weitere Informationen zur Kantensegmentierung finden Sie in der [Übersicht über die Segmentierungsbenutzeroberfläche](../../segmentation/ui/overview.md). |
| (Beta) Inkrementelle Segmentierung | Erhöht die Frische vorhandener Segmentdefinitionen, die in der Stapelsegmentierung ausgewertet werden, auf bis zu eine Stunde. |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierungsübersicht](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| ------- | ----------- |
| Beta-Quellen wechseln zu GA | Die folgenden Quellen wurden von der Beta-Version zur GA-Version beworben: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| API-Unterstützung für die Erfassung von komprimierten Dateien | Sie können jetzt komprimierte JSON- oder durch Trennzeichen getrennte Dateien mithilfe von Cloud-Datenspeicherung-Quellen Vorschau und erfassen. Weitere Informationen finden Sie im Lernprogramm zum Erfassen von Cloud-Datenspeicherung-Daten mit APIs](../../sources/tutorials/api/collect/cloud-storage.md).[ |
| Unterstützung für rekursives Hochladen von Dateien in der Benutzeroberfläche | Bei Verwendung einer Cloud-Datenspeicherung können Sie jetzt ganze Ordner rekursiv erfassen. Beim Einfügen eines ganzen Ordners müssen Sie sicherstellen, dass sein Inhalt dasselbe Schema verwendet. Weitere Informationen finden Sie im Tutorial zu [Konfigurieren eines Datenflusses für Cloud-Datenspeicherung-Connectors in der Benutzeroberfläche](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
