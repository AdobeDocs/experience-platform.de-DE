---
title: Marketo Engage-Verbindung
description: Marketo Engage ist die einzige End-to-End-Lösung für Customer Experience Management (CXM) für Marketing, Werbung, Analysen und Commerce. Damit können Sie Aktivitäten automatisieren und verwalten, von der CRM-Lead-Verwaltung und Kundeninteraktion bis hin zu Account-basiertem Marketing und Umsatzzuordnung.
exl-id: e02b6c65-b59e-41ff-8d33-f8fecfd87773
source-git-commit: 1a87ad8259803886b9a1c60f1cdc50942ba49173
workflow-type: tm+mt
source-wordcount: '1999'
ht-degree: 17%

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

Sie können die Zielgruppen für Marketo Engage aktivieren und den Synchronisierungstyp **[!UICONTROL Nur Zielgruppe]** verwenden.

### Anwendungsfälle für die Zielgruppen- und Profilsynchronisierung {#audience-profile-sync-use-cases}

**Erneuter Kontakt mit bekannten Leads aufnehmen und Leads aktualisieren**

Das Marketing-Team möchte eine Rückgewinnungskampagne für bestehende Marketo-Kontakte starten, die sich aufgrund von Website-Besuchen interessiert haben. Sie möchten auch die Lead-Informationen (z. B. Voreinstellungen, demografische Informationen) aktualisieren, jedoch keine neuen Personen in Marketo erstellen.

Sie können die Zielgruppen für Marketo Engage aktivieren und den Synchronisierungstyp **[!UICONTROL Zielgruppe und Profil]** in Kombination mit der Aktion **[!UICONTROL Nur vorhandene Personen aktualisieren]** verwenden, um sicherzustellen, dass sie nur die Zielgruppen ansprechen, die bereits in Marketo vorhanden sind.

**Erneuter Kontakt und erweiterte Reichweite mit vollständiger Profilsynchronisierung**

Das Marketing-Team möchte eine Zielgruppe für Produktinteressen für eine neue Kampagne aktivieren. Viele der Profile existieren bereits in Marketo, andere sind neu und nur in Real-Time CDP vorhanden. Für die bestehenden Personen möchten sie sicherstellen, dass sie diese Personen in Marketo aktualisieren, aber auch neue Profile erstellen.

Sie können ihre Zielgruppen in Marketo Engage aktivieren und den Synchronisierungstyp **[!UICONTROL Zielgruppe und Profil]** in Kombination mit der Aktion **[!UICONTROL Vorhandene aktualisieren und neue Personen erstellen]** verwenden, um sicherzustellen, dass sie bestehende Leads aus Marketo ansprechen und neue für die neuen Zielgruppen erstellen, die aus Real-Time CDP exportiert wurden.

## Voraussetzungen {#prerequisites}

* Die Person, die das Ziel einrichtet, muss über die Berechtigung [Person bearbeiten](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions#access-database) in ihrer Marketo-Instanz und -Partition verfügen.
* Beim Einrichten dieses Ziels sind nur Marketo Engage-Instanzen in derselben Adobe Real-Time CDP-Organisation verfügbar.
* Nur Marketo Engage-Instanzen, deren Benutzer in der Adobe Admin Console verwaltet werden, können dieses Ziel verwenden.

## Unterstützte Identitäten {#supported-identities}

[!DNL Marketo Engage] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| `DedupeField` | Das Feld, das zum Identifizieren und Abgleichen bestehender Leads in Marketo verwendet wird. | Ordnen Sie [ Schritt ](#mapping)Zuordnung“ jedes Quellfeld (z. B. `Email` oder andere benutzerdefinierte Kennungen) zu, das Sie als Deduplizierungsfeld für diese Zielidentität verwenden möchten. Um die besten Ergebnisse zu erzielen, wählen Sie ein Feld aus, das in allen Ihren Kundenprofilen konsistent verfügbar und eindeutig ist. `ECID` wird als Deduplizierungsfeld nicht unterstützt. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können. Die beiden folgenden Tabellen geben an, welche Zielgruppen dieser Connector unterstützt, _Zielgruppenherkunft_ und _Profiltypen in der Zielgruppe enthalten_:

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
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
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (E-Mail, ECID), die im [!DNL Marketo Engage]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Lead-Zuordnungsverhalten {#lead-matching}

Wenn Sie verstehen, wie die Marketo-Lead-Zuordnung funktioniert, können Sie die richtige Konfiguration für Ihren Anwendungsfall auswählen. Das passende Verhalten hängt von den ausgewählten Einstellungen **[!UICONTROL Synchronisierungstyp]** und **[!UICONTROL Personenaktion]** ab.

Marketo verwendet das Feld **[!UICONTROL Marketo-Deduplizierung]** Sie wählen aus, um Experience Platform-Profile bestehenden Marketo-Leads zuzuordnen. Der Matching-Prozess durchsucht alle Partitionen in Ihrer Marketo-Instanz, um vorhandene Leads zu finden. Anhand der folgenden Tabelle können Sie sehen, wie Leads in Ihrer Marketo-Instanz je nach ausgewählter Konfiguration erstellt und aktualisiert werden.

| Synchronisierungstyp | Aktion der Person | Übereinstimmungsverhalten |
|-----------|---------------|-------------------|
| **[!UICONTROL Nur Profil]** | **[!UICONTROL Vorhandene aktualisieren und neue Personen erstellen]** | <ul><li>Aktualisiert vorhandene Leads mit neuen Profildaten</li><li>Erstellt neue Leads in der ausgewählten Partition für nicht übereinstimmende Profile</li></ul> |
| **[!UICONTROL Nur Profil]** | **[!UICONTROL Nur vorhandene Personen aktualisieren]** | <ul><li>Aktualisiert vorhandene Leads mit neuen Profildaten</li><li>Keine neuen Leads für nicht übereinstimmende Profile erstellt</li></ul> |
| **[!UICONTROL Nur Zielgruppe]** | k. A. | <ul><li>Fügt vorhandene Leads zu Zielgruppenlisten hinzu</li><li>Keine neuen Leads für nicht übereinstimmende Profile erstellt</li></ul> |
| **[!UICONTROL Zielgruppe und Profil]** | **[!UICONTROL Vorhandene aktualisieren und neue Personen erstellen]** | <ul><li>Aktualisiert vorhandene Leads mit neuen Profildaten</li><li>Fügt vorhandene Leads zu Zielgruppenlisten hinzu</li><li>Erstellt neue Leads in der ausgewählten Partition für nicht übereinstimmende Profile</li><li>Fügt neue Leads zu Zielgruppenlisten hinzu</li></ul> |
| **[!UICONTROL Zielgruppe und Profil]** | **[!UICONTROL Nur vorhandene Personen aktualisieren]** | <ul><li>Aktualisiert vorhandene Leads mit neuen Profildaten</li><li>Fügt vorhandene Leads zu Zielgruppenlisten hinzu</li><li>Keine neuen Leads für nicht übereinstimmende Profile erstellt</li></ul> |

{style="table-layout:auto"}

### Wichtige Überlegungen

* **Auswahl des Deduplizierungsfelds**: Wählen Sie ein Feld aus, das in Ihren Kundenprofilen konsistent verfügbar und eindeutig ist (z. B.: E-Mail-Adresse, Kunden-ID).
* **Partitionsverarbeitung**: Beim Erstellen neuer Leads werden diese in der ausgewählten Partition platziert (oder **[!UICONTROL Standard]**-Partition, wenn keine Partition ausgewählt wurde)
* **Umgang mit Duplikaten**: Wenn mehrere Marketo-Leads demselben Profil entsprechen, wird nur der zuletzt aktualisierte Lead aktualisiert
* **Partitionsübergreifender Abgleich**: Das System sucht in allen Partitionen nach vorhandenen Leads, unabhängig davon, welche Partition Sie für neue Leads ausgewählt haben

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>* Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
>
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Screenshot, der zeigt, wie eine Authentifizierung beim Ziel erfolgt](../../assets/catalog/adobe/marketo-engage-connection/connect-destination.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Beispiel-Screenshot, der zeigt, wie Details für Ihr Ziel ausgefüllt werden](../../assets/catalog/adobe/marketo-engage-connection/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Munchkin ID]**: Wählen Sie die [!DNL Marketo Munchkin ID] aus, die Sie für dieses Ziel verwenden möchten.
* **[!UICONTROL Workspace-ID]**: Wählen Sie Ihre Marketo Workspace-ID aus.
* **[!UICONTROL Synchronisierungstyp]**: Wählen Sie den Synchronisierungstyp aus, den Sie für dieses Ziel verwenden möchten:
   * **[!UICONTROL Zielgruppe und Profil]**: Wählen Sie diese Option, wenn Sie sowohl Zielgruppenmitglieder zu Marketo-Listen hinzufügen als auch deren Profilinformationen auf dem neuesten Stand halten möchten.
   * **[!UICONTROL Nur Profil]**: Wählen Sie diese Option aus, wenn Sie möchten, dass Marketo-Lead-Profile stets mit den neuesten Informationen aus Experience Platform aktualisiert werden.
   * **[!UICONTROL Nur Zielgruppe]**: Wählen Sie diese Option aus, wenn Sie Zielgruppenmitglieder zu Marketo-Listen hinzufügen möchten, ohne ihre Profilinformationen zu aktualisieren.
* **[!UICONTROL Partition]**: *Die Partitionsauswahl ist nur verfügbar, wenn Sie **[!UICONTROL Nur Profil]**oder **[!UICONTROL Audience und Profil]**Synchronisierungstypen* auswählen. Wählen Sie eine Marketo-Partitions-ID aus, die mit Ihrem ausgewählten Arbeitsbereich verknüpft ist. Auf diese Weise können Sie angeben, welche Lead-Partition in Marketo die exportierten Daten erhält. Wenn Sie keine bestimmte Partition auswählen, werden Ihre Daten an die **[!UICONTROL Standard]**-Partition in Marketo gesendet.
* **[!UICONTROL Marketo-Deduplizierungsfeld]**: Wählen Sie das Marketo-Deduplizierungsfeld aus, das Sie beim Aktualisieren vorhandener Marketo-Leads verwenden möchten. Dieser Selektor zeigt die Felder an, die Sie in Marketo als Deduplizierungsfelder markiert haben. Wenn ein bestimmtes Feld aus Marketo als Deduplizierungsfeld angezeigt werden soll, müssen Sie das Feld in Marketo als [ durchsuchbares ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/lead-database) markieren.

  >[!NOTE]
  >
  >Marketo `Lead ID` und Experience Cloud IDs (`ECID`) werden für die Deduplizierung nicht unterstützt.

* **[!UICONTROL Personenaktion]**: Wählen Sie die Marketo-Aktion aus, die Sie beim Exportieren von Daten ausführen möchten.
   * **[!UICONTROL Vorhandene Personen aktualisieren und neue Personen erstellen]**: Wählen Sie diese Option, um bestehende Marketo-Leads zu aktualisieren und neue Leads für Zielgruppenmitglieder zu erstellen, die sich noch nicht in Marketo befinden. Neue Leads werden in der ausgewählten Partition erstellt. Wenn Sie keine Partition ausgewählt haben, werden neue Leads in der Partition **[!UICONTROL Standard]** erstellt.
   * **[!UICONTROL Nur bestehende Personen aktualisieren]**: Wählen Sie diese Option, wenn Sie nur bestehende Marketo-Leads aktualisieren möchten, ohne neue zu erstellen. Wenn mehrere Leads demselben Profil entsprechen, wird nur der zuletzt aktualisierte Marketo-Lead mit Ihren Experience Platform-Daten aktualisiert.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Zielen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

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
