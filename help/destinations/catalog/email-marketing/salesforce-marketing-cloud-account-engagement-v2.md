---
title: (v2) Salesforce Marketing Cloud-Kundeninteraktion
description: Erfahren Sie, wie Sie mit dem Ziel (V2) Salesforce Marketing Cloud Account Engagement (ehemals Pardot) Ihre Profildaten exportieren und in Salesforce Marketing Cloud Account Engagement mithilfe von Batch-Verarbeitung für Ihre Geschäftsanforderungen aktivieren können.
badge: label="Alpha" type="Informative"
hide: true
hidefromtoc: true
exl-id: cd792eb0-9e90-49e4-8c50-c65126e355c2
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1875'
ht-degree: 17%

---

# [!DNL (V2) Salesforce Marketing Cloud Account Engagement]-Verbindung

Das Ziel [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) (früher als [!DNL Pardot] bezeichnet) exportiert Ihre [!DNL Adobe Experience Platform] Profildaten an die B2B-Marketing-Automatisierungsplattform von Salesforce.

Diese Integration ermöglicht eine nahtlose Datensynchronisation zwischen Ihren Kundenprofilen in [!DNL Adobe Experience Platform] und Ihren Marketing-Kampagnen in [!DNL Salesforce Marketing Cloud Account Engagement].

Dieses Ziel verwendet die -[[!DNL Salesforce Import API v5]](https://developer.salesforce.com/docs/marketing/pardot/guide/import-v5.html), um Batch-Datenexporte effizient zu verarbeiten.


>[!IMPORTANT]
>
> Dies ist die V2-Version des Ziels [Salesforce Marketing Cloud Account Engagement](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md). Diese Version ersetzt das vorherige Ziel und befindet sich derzeit in der Alpha-Version.
> <br>
> Wenn Sie derzeit die vorherige Version des Ziels [Salesforce Marketing Cloud Account Engagement](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) verwenden, müssen Sie vor dem **. Januar 2026 zu dieser Version 2**. Nach Januar 2026 wird Adobe die Vorgängerversion einstellen und nicht mehr verfügbar sein.


## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL (V2) Marketing Cloud Account Engagement]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die [!DNL Adobe Experience Platform] Kunden mit diesem Ziel bewältigen können.

### B2B-Lead-Management {#use-case-lead-management}

Synchronisieren Sie Lead-Daten von [!DNL Adobe Experience Platform] zu [!DNL Salesforce Marketing Cloud Account Engagement], um eine umfassende Lead-Pflege und -Bewertung zu ermöglichen. Ihr Marketing-Team kann in Experience Platform umfangreiche Zielgruppenprofile erstellen und für automatisierte B2B-Marketing-Kampagnen in [!DNL Salesforce Marketing Cloud Account Engagement] exportieren.

### Automatisierung von Campaign {#use-case-campaign-automation}

Sie können Trigger-Marketing-Kampagnen in [!DNL Salesforce Marketing Cloud Account Engagement] durchführen, indem Sie Zielgruppen verwenden, die Sie in [!DNL Adobe Experience Platform] definieren. Nachdem Sie Ihre Audiences in [!DNL Salesforce] exportiert haben, können Sie sie für E-Mail-Kampagnen und die Verwaltung Ihrer Leads durch Pflege, Bewertung und Kampagnensegmentierung verwenden.

### Profilanreicherung {#use-case-profile-enrichment}

Erweitern Sie Ihre [!DNL Salesforce Marketing Cloud Account Engagement] Interessentenprofile mit umfangreichen Kundendaten aus [!DNL Adobe Experience Platform]. Exportieren Sie umfassende Profilattribute, um detailliertere Interessentendatensätze in zu erstellen, [!DNL Salesforce Marketing Cloud Account Engagement] Targeting und Personalisierung zu verbessern.

## Voraussetzungen {#prerequisites}

In den folgenden Abschnitten finden Sie alle Voraussetzungen, die Sie in Experience Platform und [!DNL Salesforce] einrichten müssen, sowie Informationen, die Sie vor der Arbeit mit dem [!DNL (V2) Marketing Cloud Account Engagement]-Ziel sammeln müssen.

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Bevor Sie Daten für das [!DNL (V2) Marketing Cloud Account Engagement]-Ziel aktivieren, müssen Sie ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](../../../catalog/datasets/overview.md) und [Audiences](../../../segmentation/types/overview.md) in [!DNL Experience Platform] erstellt haben.

### Voraussetzungen für [!DNL Salesforce Marketing Cloud Account Engagement] {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen für den Export von Daten aus Experience Platform in Ihr [!DNL Marketing Cloud Account Engagement]:

#### Sie benötigen ein [!DNL Marketing Cloud Account Engagement]-Konto {#prerequisites-account}

Ein [!DNL Marketing Cloud Account Engagement] Konto mit einem Abonnement für das Produkt [Marketing Cloud Account Engagement](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) ist erforderlich, um fortzufahren.

#### Sammeln von [!DNL Marketing Cloud Account Engagement]-Anmeldedaten {#gather-credentials}

Schreiben Sie die folgenden Elemente auf, bevor Sie sich beim [!DNL (V2) Marketing Cloud Account Engagement]-Ziel authentifizieren.

| Anmeldedaten | Beschreibung |
| --- | --- |
| **[!UICONTROL Account Engagement Business Unit ID]** | Ihre Geschäftseinheits-ID für die [!DNL Salesforce]-Kontointeraktion. Weitere Informationen zum Ermitteln der ID finden [ in ](https://help.salesforce.com/s/articleView?id=000381973&type=1) Salesforce-Dokumentation . |

{style="table-layout:auto"}

## Unterstützte Identitäten {#supported-identities}

[!DNL (V2) Marketing Cloud Account Engagement] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

Wenn mithilfe einer dieser Kennungen eine Übereinstimmung gefunden wird, wird der vorhandene Datensatz für Interessenten für Kontointeraktionen mit den Daten aus [!DNL Adobe Experience Platform] aktualisiert. Wenn keine Übereinstimmung gefunden wird, wird in Account Engagement ein neuer Interessenten-Datensatz erstellt.

| Zielidentität | Beschreibung | Zu beachten |
|---|---|---|
| `matchId` | Interessenten-ID in Account-Interaktion | Mindestens eine dieser drei Identitäten ist erforderlich |
| `matchSalesforceId` | Salesforce Lead/Kontakt-ID des potenziellen Kunden | Mindestens eine dieser drei Identitäten ist erforderlich |
| `matchEmail` | E-Mail-Adresse des potenziellen Kunden | Mindestens eine dieser drei Identitäten ist erforderlich |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | Ja | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li> benutzerdefinierte Upload-Zielgruppen [importiert](../../../segmentation/ui/audience-portal.md#import-audience) aus CSV-Dateien in Experience Platform,</li><li> Lookalike-Zielgruppen, </li><li> Federated Audiences, </li><li> Zielgruppen, die in anderen Experience Platform-Apps generiert werden, z. B. [!DNL Adobe Journey Optimizer], </li><li> und mehr. </li></ul> |

{style="table-layout:auto"}



Unterstützte Zielgruppen nach Zielgruppen-Datentyp:

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
|--------------------|-----------|-------------|-----------|
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Ja | Basierend auf Kundenprofilen können Sie bestimmte Personengruppen für Marketing-Kampagnen ansprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Sammlungen strukturierter Daten, die im Data Lake von [!DNL Adobe Experience Platform] gespeichert sind. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}


## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Sie exportieren alle Mitglieder einer Zielgruppe zusammen mit den gewünschten Schemafeldern *z. B. E-Mail-Adresse, Telefonnummer, Nachname)* entsprechend Ihrer Feldzuordnung.</li><li>Dieses Ziel unterstützt den Batch-Export von Profildaten mithilfe der Salesforce Import-API v5.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Batch]** | <ul><li>**Anfänglicher Export**: Vollständiger Export unmittelbar nach der Zuordnung</li><li>**Nachfolgende Exporte**: Inkrementelle Exporte alle 3 Stunden</li><li>Dieser Zeitplan ist fest und kann in Alpha nicht angepasst werden</li></ul> |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Connect to destination]** aus.

![Zielverbindungs-Workflow für Salesforce Marketing Cloud Account Engagement V2](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/connect-to-destination.png "Zielverbindungs-Workflow für Salesforce Marketing Cloud Account Engagement V2")

Sie werden zur Anmeldeseite von [!DNL Salesforce] weitergeleitet. Geben Sie Ihre [!DNL Marketing Cloud Account Engagement] Kontoanmeldeinformationen ein und wählen Sie **[!UICONTROL Log In]** aus.

![Salesforce-Anmeldeseite](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/salesforce-auth.png "Salesforce-Anmeldeseite.")

Wählen Sie als Nächstes **[!UICONTROL Allow]** aus, um der **[!DNL Adobe Experience Platform]** App Berechtigungen für den Zugriff auf Ihr [!DNL Salesforce Marketing Cloud Account Engagement]-Konto zu erteilen. *Sie müssen dies nur einmal tun*.

![Bestätigungs-Popup für den Screenshot der Salesforce-App, um der Experience Platform-App Berechtigungen für den Zugriff auf die Marketing Cloud-Kontointeraktion zu erteilen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/allow-app.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche eine Meldung an: *Sie haben erfolgreich eine Verbindung mit dem (V2) Salesforce Marketing Cloud Account Engagement Account* hergestellt und einen **[!UICONTROL Connected]** mit einem grünen Häkchen.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Account Engagement Business Unit ID]**: Ihr [!DNL Salesforce] `Account Engagement Business Unit ID`.
* **[!UICONTROL Account Engagement API]**: Wählen Sie aus, ob Sie die Produktions- (`https://pi.pardot.com`) oder Demo- (`https://pi.demo.pardot.com`) Endpunkte der Account Engagement API verwenden möchten.
* **[!UICONTROL Account Engagement Campaign ID]**: Jeder [!DNL Account Engagement] Interessent muss mit einer Kampagne verknüpft sein. Wenn Sie keine Kampagnen-ID festlegen, versucht Account Engagement automatisch, eine ID zuzuweisen, wenn in Ihrem Salesforce-Konto eine Standardeinstellung vorhanden ist.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md).

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Zielgruppendaten von [!DNL Adobe Experience Platform] an das [!DNL (V2) Marketing Cloud Account Engagement] Ziel zu senden, müssen Sie Ihre Schemafelder des Experience-Datenmodells (XDM) den entsprechenden Feldern im Ziel zuordnen.

Eine vollständige Liste der unterstützten [ finden Sie in der Dokumentation zur ](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html)Salesforce Prospect API v5. Beachten Sie[ dass ](https://developer.salesforce.com/docs/marketing/pardot/guide/custom-field-v5.html)benutzerdefinierte Felder“ in der Alpha-Version nicht unterstützt werden.

#### Unterstützte Attribute {#supported-attributes}

Das Ziel Salesforce Marketing Cloud-Kontointeraktion unterstützt die in der folgenden Tabelle beschriebenen Zielattribute.

| Attribut | Typ | Beschreibung |
|---------|----------|----------|
| `salesforceId` | Zeichenfolge | Die Salesforce-ID des potenziellen Kunden |
| `salesforceOwnerId` | Ganzzahl | Die Salesforce-Benutzer-ID des potenziellen Besitzers |
| `salutation` | Zeichenfolge | Anrede des potenziellen Kunden (z. B. Mr., Ms., Dr.) |
| `score` | Ganzzahl | Punktzahl des potenziellen Kunden bei der Kontointeraktion |
| `source` | Zeichenfolge | Quelle des Interessenten-Datensatzes |
| `state` | Zeichenfolge | Bundesland/Region des potenziellen Kunden |
| `territory` | Zeichenfolge | Das dem Interessenten zugewiesene Gebiet |
| `userId` | Ganzzahl | Die dem Interessenten zugeordnete Benutzer-ID |
| `website` | Zeichenfolge | URL der Website des Interessenten |
| `yearsInBusiness` | Zeichenfolge | Die Anzahl der Jahre, die der potenzielle Kunde bereits im Geschäft ist |
| `zip` | Zeichenfolge | Die Postleitzahl des potenziellen Kunden |

#### Erforderliche Zuordnungen {#required-mappings}

Bevor Sie mit der Zuordnung Ihrer Daten beginnen, überprüfen Sie die erforderlichen Feldzuordnungen unten.

| Zielfeld | Typ | Erforderlich | Verwendungszeitpunkt |
|---|---|---|---|
| `email` | Attribut | Immer erforderlich | Die E-Mail-Adresse des Interessenten. Dies ist die primäre Kennung, um Interessentendatensätze in Account Engagement zu finden und abzugleichen, wenn Sie keine `matchId` oder `matchSalesforceId` haben. <br> **Hinweis:** Bei der Funktion „Mehrere Interessenten mit derselben E-Mail-Adresse zulassen“ von Account Engagement kann die ausschließliche Verwendung von E-Mails zu Unklarheiten führen, wenn mehrere Interessenten mit derselben E-Mail vorhanden sind. Bei der Kontointeraktion wird in der Regel in solchen Fällen standardmäßig der Interessent mit der neuesten Aktivität aktualisiert. |
| `matchId` | Identität | Mindestens eine dieser drei Identitäten ist erforderlich | Eine eindeutige Kennung, die von Account Engagement für jeden einzelnen Interessentendatensatz generiert wird. Verwenden Sie diese Option, wenn Sie bereits über die Account Engagement Prospect ID verfügen und sicherstellen möchten, dass Aktualisierungen auf den richtigen Interessenten angewendet werden, insbesondere wenn mehrere Interessenten dieselbe E-Mail-Adresse teilen. |
| `matchSalesforceId` | Identität | Mindestens eine dieser drei Identitäten ist erforderlich | Die Salesforce-ID eines Leads oder Kontakts in Salesforce. Verwenden Sie diese Option, wenn ein Interessent bereits mit Salesforce synchronisiert wurde, um die Datenkonsistenz zwischen Account-Interaktion und Salesforce zu gewährleisten. |
| `matchEmail` | Identität | Mindestens eine dieser drei Identitäten ist erforderlich | Die E-Mail-Adresse des Interessenten, die für den Abgleich verwendet wird. Verwenden Sie diese ID als alternative Kennung, wenn Sie nicht über die spezifische Account Engagement Prospect ID oder Salesforce ID verfügen. Hinweis: Wenn mehrere Interessenten dieselbe E-Mail-Adresse haben, aktualisiert Account Engagement in der Regel den Interessenten mit der neuesten Aktivität. |

Gehen Sie wie folgt vor, um die richtigen Felder zuzuordnen.

1. Wählen Sie im **[!UICONTROL Mapping]** Schritt **[!UICONTROL Add new mapping]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
1. Wählen Sie im **[!UICONTROL Select source field]** die Kategorie **[!UICONTROL Select attributes]** und dann das XDM-Attribut aus, oder wählen Sie die **[!UICONTROL Select identity namespace]** und dann eine Identität aus.
1. Wählen Sie im **[!UICONTROL Select target field]**-Fenster den **[!UICONTROL Select identity namespace]** und dann eine Identität aus, oder wählen Sie **[!UICONTROL Select custom attributes]** Kategorie aus und geben Sie in der Liste der standardmäßigen Felder für Interessenten für Account-Interaktionen an.

![Zuordnen von XDM-Feldern und Identitäten zu Salesforce Marketing Cloud Account Engagement V2-Feldern](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/mapping.png "Beispiel für die Zuordnung von XDM-Feldern und Identitäten zu Salesforce Marketing Cloud Account Engagement V2-Feldern")

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Navigieren Sie zu einer der ausgewählten Zielgruppen. Wählen Sie die Registerkarte **[!DNL Activation data]** aus. Die Spalte **[!UICONTROL Mapping ID]** zeigt den Namen des benutzerdefinierten Felds an, das innerhalb der [!DNL Marketing Cloud Account Engagement Prospects] generiert wird.
   Beispiel-Screenshot der ![Experience Platform-Benutzeroberfläche mit der Zuordnungs-ID für ein ausgewähltes Segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/selected-segment-mapping-id.png)

1. Rufen Sie die [[!DNL Salesforce]](https://login.salesforce.com/) Website auf. Navigieren Sie dann zur Seite **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** und überprüfen Sie, ob die potenziellen Kunden aus der Audience hinzugefügt/aktualisiert wurden. Alternativ können Sie auch auf [[!DNL Account Engagement]](https://pi.pardot.com/) und die **[!DNL Prospects]** zugreifen.
   ![Screenshot der Salesforce-Benutzeroberfläche mit der Seite „Interessenten“.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/prospects.png)

1. Um zu überprüfen, ob die Interessenten aktualisiert wurden, wählen Sie einen Interessenten aus und überprüfen Sie, ob das benutzerdefinierte Feld des Interessenten mit dem Zielgruppenstatus von Experience Platform aktualisiert wurde.
   ![Screenshot der Salesforce-Benutzeroberfläche mit der ausgewählten Interessentenseite. Das benutzerdefinierte Feld des Interessenten wird mit dem Zielgruppenstatus aktualisiert.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/prospect.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Weitere Ressourcen {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API-Dokumentation](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html)
* [Dokumentation zur Salesforce-Import-API v5](https://developer.salesforce.com/docs/marketing/pardot/guide/import-v5.html)
* [Dokumentation zur Salesforce Prospect API v5](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html)
