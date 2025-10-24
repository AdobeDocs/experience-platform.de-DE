---
title: Snowflake Batch-Verbindung
description: Erstellen Sie eine Live-Snowflake-Datenfreigabe, um tägliche Zielgruppenaktualisierungen direkt als freigegebene Tabellen in Ihrem Konto zu erhalten.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 6959ccd0-ba30-4750-a7de-d0a709292ef7
source-git-commit: 59df2c6a0fb5d9dbdd10b52d82fb6b94f5083c3a
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 18%

---

# Snowflake Batch-Verbindung {#snowflake-destination}

>[!AVAILABILITY]
>
>Dieser Ziel-Connector ist nur eingeschränkt verfügbar und nur für Real-Time CDP Ultimate-Kunden verfügbar, die in der [VA7-Region bereitgestellt &#x200B;](/help/landing/multi-cloud.md#azure-regions).

## Überblick {#overview}

Verwenden Sie dieses Ziel, um Zielgruppendaten an dynamische Tabellen in Ihrem Snowflake-Konto zu senden. Dynamische Tabellen ermöglichen den Zugriff auf Ihre Daten, ohne dass physische Datenkopien erforderlich sind.

In den folgenden Abschnitten erfahren Sie, wie das Snowflake-Ziel funktioniert und wie Daten zwischen Adobe und Snowflake übertragen werden.

### Funktionsweise der Datenfreigabe in Snowflake {#data-sharing}

Dieses Ziel verwendet eine [!DNL Snowflake] Datenfreigabe, d. h. es werden keine Daten physisch exportiert oder an Ihre eigene Snowflake-Instanz übertragen. Stattdessen gewährt Ihnen Adobe schreibgeschützten Zugriff auf eine Live-Tabelle, die in der Snowflake-Umgebung von Adobe gehostet wird. Sie können diese freigegebene Tabelle direkt aus Ihrem Snowflake-Konto abfragen, aber Sie sind nicht der Eigentümer der Tabelle und können sie nicht über die angegebene Aufbewahrungsfrist hinaus ändern oder beibehalten. Adobe verwaltet den Lebenszyklus und die Struktur der freigegebenen Tabelle vollständig.

Wenn Sie zum ersten Mal einen Datenfluss von Adobe zu Ihrem Snowflake-Konto eingerichtet haben, werden Sie aufgefordert, den privaten Eintrag von Adobe zu akzeptieren.

![Screenshot mit dem Bildschirm für die Annahme der privaten Snowflake-Auflistung](../../assets/catalog/cloud-storage/snowflake-batch/snowflake-accept-listing.png)

### Datenaufbewahrung und Time-to-Live (TTL) {#ttl}

Alle über diese Integration freigegebenen Daten haben eine feste Time-to-Live (TTL) von sieben Tagen. Sieben Tage nach dem letzten Export läuft die dynamische Tabelle automatisch ab und wird unzugänglich, unabhängig davon, ob der Datenfluss noch aktiv ist. Wenn Sie die Daten länger als sieben Tage aufbewahren müssen, müssen Sie den Inhalt in eine Tabelle kopieren, deren Eigentümer Sie in Ihrer eigenen Snowflake-Instanz sind, bevor die TTL abläuft.

>[!IMPORTANT]
>
>Durch das Löschen eines Datenflusses in Experience Platform verschwindet die dynamische Tabelle aus Ihrem Snowflake-Konto.

### Verhalten bei der Zielgruppenaktualisierung {#audience-update-behavior}

Wenn Ihre Zielgruppe im [Batch-Modus](../../../segmentation/methods/batch-segmentation.md) ausgewertet wird, werden die Daten in der freigegebenen Tabelle alle 24 Stunden aktualisiert. Das bedeutet, dass es zwischen den Änderungen der Zielgruppenzugehörigkeit und dem Zeitpunkt, zu dem diese Änderungen in der freigegebenen Tabelle angezeigt werden, zu einer Verzögerung von bis zu 24 Stunden kommen kann.

### Batch-Datenfreigabelogik {#batch-data-sharing}

Wenn ein Datenfluss zum ersten Mal für eine Zielgruppe ausgeführt wird, wird eine Aufstockung durchgeführt und alle derzeit qualifizierten Profile werden freigegeben. Nach dieser ersten Aufstockung stellt das Ziel regelmäßig Momentaufnahmen der vollständigen Zielgruppenzugehörigkeit bereit. Jeder Schnappschuss ersetzt die vorherigen Daten in der freigegebenen Tabelle, sodass immer die neueste vollständige Ansicht der Zielgruppe ohne historische Daten angezeigt wird.

## Streaming vs. Batch-Datenfreigabe {#batch-vs-streaming}

Experience Platform bietet zwei Typen von Snowflake-Zielen: [Snowflake-Streaming](snowflake.md) und [Snowflake-Batch](snowflake-batch.md).

Zwar ermöglichen Ihnen beide Ziele den kopiefreien Zugriff auf Ihre Daten in Snowflake, doch es gibt auch einige empfohlene Best Practices in Bezug auf Anwendungsfälle für jeden Connector.

Die nachstehende Tabelle hilft Ihnen bei der Entscheidung über den zu verwendenden Connector, indem sie die Szenarien skizziert, in denen jede Methode der Datenfreigabe am besten geeignet ist.

|  | Wählen Sie [Snowflake Batch](snowflake-batch.md) wenn Sie benötigen | Wählen Sie [Snowflake-Streaming](snowflake.md), wenn Sie Folgendes benötigen |
|--------|-------------------|----------------------|
| **Aktualisierungshäufigkeit** | Periodische Momentaufnahmen | Kontinuierliche Aktualisierungen in Echtzeit |
| **Datendarstellung** | Vollständiger Zielgruppen-Snapshot, der frühere Daten ersetzt | Inkrementelle Aktualisierungen basierend auf Profiländerungen |
| **Anwendungsfall - Fokus** | Analytische/ML-Workloads, bei denen die Latenz nicht kritisch ist | Sofortige Aktionsszenarien, die Echtzeit-Updates erfordern |
| **Daten-Management** | Immer den neuesten vollständigen Schnappschuss anzeigen | Inkrementelle Aktualisierungen basierend auf Änderungen der Zielgruppenzugehörigkeit |
| **Beispielszenarien** | Geschäftsberichte, Datenanalyse, ML-Modell-Training | Unterdrückung von Marketing-Kampagnen, Echtzeit-Personalisierung |

Weitere Informationen zum Freigeben von Streaming-Daten finden Sie in der Dokumentation zu [Snowflake Streaming](snowflake.md)Verbindungen.

## Anwendungsfälle {#use-cases}

Die Freigabe von Batch-Daten ist ideal für Szenarien, in denen Sie eine vollständige Momentaufnahme Ihrer Zielgruppe benötigen und keine Echtzeit-Aktualisierungen erforderlich sind, z. B.:

* **Analytische Workloads**: Bei der Durchführung von Datenanalysen, Reporting oder Business Intelligence-Aufgaben, die eine vollständige Ansicht der Zielgruppenzugehörigkeit erfordern
* **Workflows für maschinelles Lernen**: Zum Trainieren von ML-Modellen oder zum Ausführen prädiktiver Analysen, die von vollständigen Zielgruppen-Momentaufnahmen profitieren
* **Data Warehousing**: Wenn Sie eine aktuelle Kopie von Zielgruppendaten in Ihrer eigenen Snowflake-Instanz pflegen müssen
* **Periodisches Reporting**: Für regelmäßige Geschäftsberichte, bei denen Sie den neuesten Zielgruppenstatus ohne Verlaufsverfolgung benötigen
* **ETL-Prozesse**: Wenn Sie Zielgruppendaten in Batches umwandeln oder verarbeiten müssen

Die Freigabe von Batch-Daten vereinfacht das Daten-Management durch Bereitstellung vollständiger Momentaufnahmen, sodass inkrementelle Aktualisierungen oder Zusammenführungsänderungen nicht mehr manuell verwaltet werden müssen.

## Voraussetzungen {#prerequisites}

Bevor Sie Ihre Snowflake-Verbindung konfigurieren, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* Sie haben Zugriff auf ein [!DNL Snowflake].
* Ihr Snowflake-Konto hat private Listeneinträge abonniert. Sie oder eine andere Person in Ihrem Unternehmen, die über Administratorrechte für das Konto auf Snowflake verfügt, können dies konfigurieren.

Weitere Informationen zu den [[!DNL Snowflake]  Berechtigungen finden &#x200B;](https://docs.snowflake.com/en/collaboration/consumer-listings-access#access-a-private-listing) in der Dokumentation .

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können. Die beiden folgenden Tabellen geben an, welche Zielgruppen dieser Connector unterstützt, _Zielgruppenherkunft_ und _Profiltypen in der Zielgruppe enthalten_:

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | ✓ | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li> benutzerdefinierte Upload-Zielgruppen [importiert](../../../segmentation/ui/audience-portal.md#import-audience) aus CSV-Dateien in Experience Platform,</li><li> Lookalike-Zielgruppen, </li><li> Federated Audiences, </li><li> Zielgruppen, die in anderen Experience Platform-Apps wie Adobe Journey Optimizer generiert wurden, </li><li> und mehr. </li></ul> |

{style="table-layout:auto"}

Unterstützte Zielgruppen nach Zielgruppen-Datentyp:

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
|--------------------|-----------|-------------|-----------|
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | ✓ | Basierend auf Kundenprofilen können Sie bestimmte Personengruppen für Marketing-Kampagnen ansprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Im Data Lake von Adobe Experience Platform gespeicherte Sammlungen strukturierter Daten. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im [!DNL Snowflake]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Dieses Ziel bietet regelmäßige Momentaufnahmen der vollständigen Zielgruppenzugehörigkeit durch die Datenfreigabe von Snowflake. Jeder Schnappschuss ersetzt die vorherigen Daten, sodass Sie immer die neueste vollständige Ansicht Ihrer Audience haben. |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. &#x200B;](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Connect to destination]** aus und geben Sie einen Kontonamen und optional eine Kontobeschreibung an.

![Beispiel-Screenshot, der zeigt, wie eine Authentifizierung beim Ziel erfolgt](../../assets/catalog/cloud-storage/snowflake-batch/authenticate-destination.png)

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_snowflake_batch_accountID"
>title="Geben Sie Ihre Snowflake-Konto-ID ein"
>abstract="Wenn Ihr Konto mit einer Organisation verknüpft ist, verwenden Sie dieses Format: `OrganizationName.AccountName`<br><br>. Wenn Ihr Konto nicht mit einer Organisation verknüpft ist, verwenden Sie dieses Format:`AccountName`."

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Beispiel-Screenshot, der zeigt, wie Details für Ihr Ziel ausgefüllt werden](../../assets/catalog/cloud-storage/snowflake-batch/configure-destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Snowflake Account ID]**: Ihre Snowflake-Konto-ID. Verwenden Sie das folgende Konto-ID-Format, je nachdem, ob Ihr Konto mit einer Organisation verknüpft ist:
   * Wenn Ihr Konto mit einer Organisation verknüpft ist: `OrganizationName.AccountName`.
   * Wenn Ihr Konto nicht mit einer Organisation verknüpft ist: `AccountName`.
* **[!UICONTROL Account acknowledgment]**: Schalten Sie die Snowflake-Konto-ID-Bestätigung um, um zu bestätigen, dass Ihre Konto-ID korrekt ist und zu Ihnen gehört.

>[!IMPORTANT]
>
> Sonderzeichen, die im Zielnamen und im Namen der Experience Platform-Sandbox verwendet werden, werden in Snowflake automatisch in Unterstriche (`_`) konvertiert. Um Verwirrung zu vermeiden, verwenden Sie keine Sonderzeichen in Ihrem Ziel und Sandbox-Namen.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Zielen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md).

### Attribute zuordnen {#map}

Sie können Identitäten und Profilattribute an dieses Ziel exportieren.

![Bild der Experience Platform-Benutzeroberfläche mit dem Zuordnungsbildschirm für das Snowflake-Ziel.](../../assets/catalog/cloud-storage/snowflake-batch/mapping.png)

Sie können das [Steuerelement für berechnete Felder](../../ui/data-transformations-calculated-fields.md) verwenden, um Arrays zu exportieren und Vorgänge für sie auszuführen.

Die Zielattribute werden in Snowflake automatisch mit dem Attributnamen erstellt, den Sie im Feld **[!UICONTROL Attribute name]** angeben.

## Exportierte Daten/Datenexport validieren {#exported-data}

Die Daten werden über eine dynamische Tabelle in Ihrem Snowflake-Konto bereitgestellt. Überprüfen Sie Ihr Snowflake-Konto, um sicherzustellen, dass die Daten korrekt exportiert wurden.

### Datenstruktur {#data-structure}

Die dynamische Tabelle enthält die folgenden Spalten:

* **TS**: Eine Zeitstempelspalte, die angibt, wann jede Zeile zuletzt aktualisiert wurde
* **Zuordnungsattribute**: Jedes Zuordnungsattribut, das Sie während des Aktivierungs-Workflows auswählen, wird in Snowflake als Spaltenüberschrift dargestellt
* **Zielgruppenzugehörigkeit**: Die Zugehörigkeit zu einer dem Datenfluss zugeordneten Zielgruppe wird über einen `active` Eintrag in der entsprechenden Zelle angezeigt

![Screenshot der Snowflake-Benutzeroberfläche mit dynamischen Tabellendaten](../../assets/catalog/cloud-storage/snowflake-batch/data-validation.png)

## Bekannte Einschränkungen {#known-limitations}

### Standardmäßige Einschränkung für Zusammenführungsrichtlinien {#default-merge-policy-restriction}

Derzeit können nur Zielgruppen exportiert werden, die der standardmäßigen Zusammenführungsrichtlinie zugeordnet sind.

### Regionale Verfügbarkeit {#regional-availability}

Das [!DNL Snowflake] Batch-Ziel ist derzeit nur für Real-Time CDP-Kundinnen und -Kunden verfügbar, die in der Experience Platform VA7-Region bereitgestellt sind.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
