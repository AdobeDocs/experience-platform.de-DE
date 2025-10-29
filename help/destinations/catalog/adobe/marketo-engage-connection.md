---
title: Marketo Engage-Verbindung
description: Marketo Engage ist die einzige End-to-End-Lösung für Customer Experience Management (CXM) für Marketing, Werbung, Analysen und Commerce. Damit können Sie Aktivitäten automatisieren und verwalten, von der CRM-Lead-Verwaltung und Kundeninteraktion bis hin zu Account-basiertem Marketing und Umsatzzuordnung.
exl-id: e02b6c65-b59e-41ff-8d33-f8fecfd87773
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1873'
ht-degree: 16%

---

# Marketo Engage-Verbindung

## Überblick {#overview}

[!DNL Marketo Engage] ist die einzige End-to-End-Lösung für Customer Experience Management (CXM) für Marketing, Werbung, Analysen und Commerce. Damit können Sie Aktivitäten automatisieren und verwalten, von der CRM-Lead-Verwaltung und Kundeninteraktion bis hin zu Account-basiertem Marketing und Umsatzzuordnung.

Verwenden Sie dieses Ziel für die Echtzeit-Synchronisierung von Zielgruppendaten und Profilattributen zwischen Adobe Experience Platform und Marketo Engage.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Marketo Engage]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel bewältigen können.

### Anwendungsfälle für die Zielgruppensynchronisierung {#audience-sync-use-cases}

**Nur bekannte Leads erneut kontaktieren**

Das Marketing-Team möchte eine Win-Back-Kampagne durchführen, die auf Leads abzielt, die sich nicht innerhalb von 90 oder mehr Tagen betätigt haben, aber bereits in Marketo existieren.

Sie können die Zielgruppen für Marketo Engage aktivieren und den **[!UICONTROL Audience Only]** Synchronisierungstyp verwenden.

### Anwendungsfälle für die Zielgruppen- und Profilsynchronisierung {#audience-profile-sync-use-cases}

**Erneuter Kontakt mit bekannten Leads aufnehmen und Leads aktualisieren**

Das Marketing-Team möchte eine Rückgewinnungskampagne für bestehende Marketo-Kontakte starten, die sich aufgrund von Website-Besuchen interessiert haben. Sie möchten auch die Lead-Informationen (z. B. Voreinstellungen, demografische Informationen) aktualisieren, jedoch keine neuen Personen in Marketo erstellen.

Sie können die Zielgruppen für Marketo Engage aktivieren und den **[!UICONTROL Audience and Profile]** Synchronisierungstyp in Kombination mit der **[!UICONTROL Update existing persons only]** verwenden, um sicherzustellen, dass sie nur die Zielgruppen ansprechen, die bereits in Marketo vorhanden sind.

**Erneuter Kontakt und erweiterte Reichweite mit vollständiger Profilsynchronisierung**

Das Marketing-Team möchte eine Zielgruppe für Produktinteressen für eine neue Kampagne aktivieren. Viele der Profile existieren bereits in Marketo, andere sind neu und nur in Real-Time CDP vorhanden. Für die bestehenden Personen möchten sie sicherstellen, dass sie diese Personen in Marketo aktualisieren, aber auch neue Profile erstellen.

Sie können ihre Zielgruppen in Marketo Engage aktivieren und den **[!UICONTROL Audience and Profile]** Synchronisierungstyp in Kombination mit der **[!UICONTROL Update existing and create new persons]** verwenden, um sicherzustellen, dass sie bestehende Leads aus Marketo ansprechen und neue für die neuen Zielgruppen erstellen, die aus Real-Time CDP exportiert wurden.

## Voraussetzungen {#prerequisites}

* Die Person, die das Ziel einrichtet, muss über die Berechtigung [Person bearbeiten](https://experienceleague.adobe.com/de/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions#access-database) in ihrer Marketo-Instanz und -Partition verfügen.
* Beim Einrichten dieses Ziels sind nur Marketo Engage-Instanzen in derselben Adobe Real-Time CDP-Organisation verfügbar.
* Nur Marketo Engage-Instanzen, deren Benutzer in der Adobe Admin Console verwaltet werden, können dieses Ziel verwenden.

## Unterstützte Identitäten {#supported-identities}

[!DNL Marketo Engage] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| `DedupeField` | Das Feld, das zum Identifizieren und Abgleichen bestehender Leads in Marketo verwendet wird. | Ordnen Sie [&#x200B; Schritt &#x200B;](#mapping)Zuordnung“ jedes Quellfeld (z. B. `Email` oder andere benutzerdefinierte Kennungen) zu, das Sie als Deduplizierungsfeld für diese Zielidentität verwenden möchten. Um die besten Ergebnisse zu erzielen, wählen Sie ein Feld aus, das in allen Ihren Kundenprofilen konsistent verfügbar und eindeutig ist. `ECID` wird als Deduplizierungsfeld nicht unterstützt. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können. Die beiden folgenden Tabellen geben an, welche Zielgruppen dieser Connector unterstützt, _Zielgruppenherkunft_ und _Profiltypen in der Zielgruppe enthalten_:

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | ✓ | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li> benutzerdefinierte Upload-Zielgruppen [importiert](../../../segmentation/ui/audience-portal.md#import-audience) aus CSV-Dateien in Experience Platform,</li><li> Lookalike-Zielgruppen, </li><li> Federated Audiences, </li><li> Zielgruppen, die in anderen Experience Platform-Apps wie Adobe Journey Optimizer generiert wurden, </li><li> und mehr. </li></ul> <br> |

{style="table-layout:auto"}

Unterstützte Zielgruppen nach Zielgruppen-Datentyp:

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
|--------------------|-----------|-------------|-----------|
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Ja | Basierend auf Kundenprofilen können Sie bestimmte Personengruppen für Marketing-Kampagnen ansprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Im Data Lake von Adobe Experience Platform gespeicherte Sammlungen strukturierter Daten. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (E-Mail, ECID), die im [!DNL Marketo Engage]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Lead-Zuordnungsverhalten {#lead-matching}

Wenn Sie verstehen, wie die Marketo-Lead-Zuordnung funktioniert, können Sie die richtige Konfiguration für Ihren Anwendungsfall auswählen. Das passende Verhalten hängt von den ausgewählten **[!UICONTROL Sync Type]**- und **[!UICONTROL Person Action]** ab.

Marketo verwendet die von Ihnen ausgewählten **[!UICONTROL Marketo deduplication field]**, um Experience Platform-Profile bestehenden Marketo-Leads zuzuordnen. Der Matching-Prozess durchsucht alle Partitionen in Ihrer Marketo-Instanz, um vorhandene Leads zu finden. Anhand der folgenden Tabelle können Sie sehen, wie Leads in Ihrer Marketo-Instanz je nach ausgewählter Konfiguration erstellt und aktualisiert werden.

| Synchronisierungstyp | Aktion der Person | Übereinstimmungsverhalten |
|-----------|---------------|-------------------|
| **[!UICONTROL Profile only]** | **[!UICONTROL Update existing and create new persons]** | <ul><li>Aktualisiert vorhandene Leads mit neuen Profildaten</li><li>Erstellt neue Leads in der ausgewählten Partition für nicht übereinstimmende Profile</li></ul> |
| **[!UICONTROL Profile only]** | **[!UICONTROL Update existing persons only]** | <ul><li>Aktualisiert vorhandene Leads mit neuen Profildaten</li><li>Keine neuen Leads für nicht übereinstimmende Profile erstellt</li></ul> |
| **[!UICONTROL Audience only]** | k. A. | <ul><li>Fügt vorhandene Leads zu Zielgruppenlisten hinzu</li><li>Keine neuen Leads für nicht übereinstimmende Profile erstellt</li></ul> |
| **[!UICONTROL Audience and profile]** | **[!UICONTROL Update existing and create new persons]** | <ul><li>Aktualisiert vorhandene Leads mit neuen Profildaten</li><li>Fügt vorhandene Leads zu Zielgruppenlisten hinzu</li><li>Erstellt neue Leads in der ausgewählten Partition für nicht übereinstimmende Profile</li><li>Fügt neue Leads zu Zielgruppenlisten hinzu</li></ul> |
| **[!UICONTROL Audience and profile]** | **[!UICONTROL Update existing persons only]** | <ul><li>Aktualisiert vorhandene Leads mit neuen Profildaten</li><li>Fügt vorhandene Leads zu Zielgruppenlisten hinzu</li><li>Keine neuen Leads für nicht übereinstimmende Profile erstellt</li></ul> |

{style="table-layout:auto"}

### Wichtige Überlegungen

* **Auswahl des Deduplizierungsfelds**: Wählen Sie ein Feld aus, das in Ihren Kundenprofilen konsistent verfügbar und eindeutig ist (z. B.: E-Mail-Adresse, Kunden-ID).
* **Partitionsverarbeitung**: Beim Erstellen neuer Leads werden diese in der ausgewählten Partition platziert (oder **[!UICONTROL Default]** Partition, wenn keine Partition ausgewählt wurde)
* **Umgang mit Duplikaten**: Wenn mehrere Marketo-Leads demselben Profil entsprechen, wird nur der zuletzt aktualisierte Lead aktualisiert
* **Partitionsübergreifender Abgleich**: Das System sucht in allen Partitionen nach vorhandenen Leads, unabhängig davon, welche Partition Sie für neue Leads ausgewählt haben

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>* Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. &#x200B;](/help/access-control/home.md#permissions)
>
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Connect to destination]** aus.

![Screenshot, der zeigt, wie eine Authentifizierung beim Ziel erfolgt](../../assets/catalog/adobe/marketo-engage-connection/connect-destination.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Beispiel-Screenshot, der zeigt, wie Details für Ihr Ziel ausgefüllt werden](../../assets/catalog/adobe/marketo-engage-connection/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Munchkin ID]**: Wählen Sie die [!DNL Marketo Munchkin ID] aus, die Sie für dieses Ziel verwenden möchten.
* **[!UICONTROL Workspace ID]**: Wählen Sie Ihre Marketo Workspace-ID aus.
* **[!UICONTROL Sync type]**: Wählen Sie den Synchronisierungstyp aus, den Sie für dieses Ziel verwenden möchten:
   * **[!UICONTROL Audience and profile]**: Wählen Sie diese Option aus, wenn Sie sowohl Zielgruppenmitglieder zu Marketo-Listen hinzufügen als auch deren Profilinformationen auf dem neuesten Stand halten möchten.
   * **[!UICONTROL Profile only]**: Wählen Sie diese Option aus, um Marketo-Lead-Profile mit den neuesten Informationen aus Experience Platform auf dem neuesten Stand zu halten.
   * **[!UICONTROL Audience only]**: Wählen Sie diese Option aus, wenn Sie Zielgruppenmitglieder zu Marketo-Listen hinzufügen möchten, ohne ihre Profilinformationen zu aktualisieren.
* **[!UICONTROL Partition]**: *Die Partitionsauswahl ist nur bei der Auswahl von **[!UICONTROL Profile only]**&#x200B;oder **[!UICONTROL Audience and profile]**&#x200B;Synchronisierungstypen verfügbar*. Wählen Sie eine Marketo-Partitions-ID aus, die mit Ihrem ausgewählten Arbeitsbereich verknüpft ist. Auf diese Weise können Sie angeben, welche Lead-Partition in Marketo die exportierten Daten erhält. Wenn Sie keine bestimmte Partition auswählen, werden Ihre Daten an die **[!UICONTROL Default]** Partition in Marketo gesendet.
* **[!UICONTROL Marketo deduplication field]**: Wählen Sie das Marketo-Deduplizierungsfeld aus, das Sie beim Aktualisieren vorhandener Marketo-Leads verwenden möchten. Dieser Selektor zeigt die Felder an, die Sie in Marketo als Deduplizierungsfelder markiert haben. Wenn ein bestimmtes Feld aus Marketo als Deduplizierungsfeld angezeigt werden soll, müssen Sie das Feld in Marketo als [&#x200B; durchsuchbares &#x200B;](https://experienceleague.adobe.com/de/docs/marketo-developer/marketo/rest/lead-database/lead-database) markieren.

  >[!NOTE]
  >
  >Marketo `Lead ID` und Experience Cloud IDs (`ECID`) werden für die Deduplizierung nicht unterstützt.

* **[!UICONTROL Person Action]**: Wählen Sie die Marketo-Aktion aus, die Sie beim Exportieren von Daten ausführen möchten.
   * **[!UICONTROL Update existing and create new persons]**: Wählen Sie diese Option, um bestehende Marketo-Leads zu aktualisieren und neue Leads für Zielgruppenmitglieder zu erstellen, die sich noch nicht in Marketo befinden. Neue Leads werden in der ausgewählten Partition erstellt. Wenn Sie keine Partition ausgewählt haben, werden neue Leads in der **[!UICONTROL Default]** erstellt.
   * **[!UICONTROL Update existing persons only]**: Wählen Sie diese Option aus, wenn Sie nur bestehende Marketo-Leads aktualisieren möchten, ohne neue zu erstellen. Wenn mehrere Leads demselben Profil entsprechen, wird nur der zuletzt aktualisierte Marketo-Lead mit Ihren Experience Platform-Daten aktualisiert.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Zielen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Erforderliche Zuordnungen {#required-mappings}

Ordnen Sie während des Zuordnungsschritts jedes Quellfeld (z. B. `email` oder andere benutzerdefinierte Kennungen), das Sie als Deduplizierungsfeld verwenden möchten, der `DedupeField` Zielidentität zu. Um die besten Ergebnisse zu erzielen, wählen Sie ein Feld aus, das in allen Ihren Kundenprofilen konsistent verfügbar und eindeutig ist.

Damit Marketo Leads erfolgreich erstellen kann, müssen Sie auch die folgenden erforderlichen Zielattribute zuordnen:

* `firstName`: Der Vorname des Leads
* `lastName`: Der Nachname des Leads
* `email`: Die E-Mail-Adresse des Leads

Wenn Sie `email` als Deduplizierungsfeld verwenden, müssen Sie auch die Attribute `firstName` und `lastName` zuordnen, wie in der Abbildung unten dargestellt.

![Screenshot der erforderlichen Zuordnung bei Verwendung von E-Mail als Deduplizierungsfeld](../../assets/catalog/adobe/marketo-engage-connection/required-mapping-email-dedupe.png)

Wenn Sie ein anderes Deduplizierungsfeld verwenden, müssen Sie alle drei erforderlichen Attribute (`firstName`, `lastName`, `email`) wie in der Abbildung unten dargestellt manuell zuordnen.

![Screenshot, der die erforderliche Zuordnung zeigt, wenn keine E-Mail als Deduplizierungsfeld verwendet wird](../../assets/catalog/adobe/marketo-engage-connection/required-mapping-email.png)

## Exportierte Daten/Datenexport validieren {#exported-data}

Nachdem Sie Zielgruppen in Marketo Engage exportiert haben, sollten Sie sich bei Ihrem Marketo-Konto anmelden, um zu überprüfen, ob die Zielgruppen erwartungsgemäß aktiviert wurden. Überprüfen Sie die relevanten Lead-Partitionen und Arbeitsbereiche in Marketo, um sicherzustellen, dass die Zielgruppendaten korrekt angezeigt werden und dass die beabsichtigten Aktionen (z. B. Aktualisieren oder Erstellen von Personen) ausgeführt wurden.

Wenn die erwarteten Daten nicht angezeigt werden, überprüfen Sie Ihre Zuordnungs- und Exporteinstellungen in Adobe Experience Platform und versuchen Sie den Export erneut.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
