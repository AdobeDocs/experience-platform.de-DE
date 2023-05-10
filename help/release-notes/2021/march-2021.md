---
title: Adobe Experience Platform – Versionshinweise März 2021
description: Versionshinweise März 2021 für Adobe Experience Platform.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 100%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 31. März 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

| Funktion | Beschreibung |
| ------- | ----------- |
| `add_to_array`-Funktion | Die Funktion wurde aktualisiert, um Arrays als Parameter zu unterstützen. |
| `to_array`-Funktion | Die Funktion wurde aktualisiert, um Objekte als Parameter zu unterstützen. |

Weitere Informationen finden Sie unter [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## Segmentierungs-Service {#segmentation}

Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und aus Ihren [!DNL Real-Time Customer Profile]-Daten Zielgruppen generieren können. Diese Segmente werden zentral in [!DNL Platform] konfiguriert und gepflegt, sodass sie für jede Adobe-Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| (Beta) Edge-Segmentierung | Bei der Edge-Segmentierung werden Segmente in Echtzeit ausgewertet, was Anwendungsfälle mit Personalisierung auf derselben Seite und der folgenden Seite ermöglicht. Weitere Informationen zur Edge-Segmentierung finden Sie in der [Übersicht über die Segmentierungsbenutzeroberfläche](../../segmentation/ui/overview.md). |
| (Beta) Inkrementelle Segmentierung | Erhöht die Aktualität vorhandener Segmentdefinitionen, die in der Batch-Segmentierung ausgewertet werden, auf bis zu eine Stunde. |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierung – Übersicht](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| ------- | ----------- |
| Wechsel von Betaquellen zu allgemeiner Verfügbarkeit | Die folgenden Quellen wurden von der Betaversion auf allgemeine Verfügbarkeit umgestellt: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| API-Unterstützung für die Erfassung komprimierter Dateien | Sie können komprimierte JSON- oder durch Trennzeichen getrennte Dateien mithilfe von Cloud-Speicherquellen nun in einer Vorschau anzeigen und erfassen. Weitere Informationen finden Sie im Tutorial zum [Erfassen von Cloud-Speicherdaten mithilfe von APIs](../../sources/tutorials/api/collect/cloud-storage.md). |
| UI-Unterstützung für das rekursive Hochladen von Dateien | Sie können bei Verwendung einer Cloud-Speicherquelle jetzt ganze Ordner rekursiv erfassen. Bei der Erfassung eines ganzen Ordners müssen Sie sicherstellen, dass dessen Inhalt dasselbe Schema aufweist. Weitere Informationen finden Sie im Tutorial zum [Konfigurieren eines Datenflusses für Cloud-Speicher-Connectoren in der Benutzeroberfläche](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
