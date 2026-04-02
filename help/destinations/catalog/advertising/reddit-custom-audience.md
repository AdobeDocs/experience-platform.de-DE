---
title: Benutzerdefinierte Zielgruppe bearbeiten
description: Reddit Ads verbindet Marken mit Menschen, die ihre Leidenschaften und Probleme aktiv in Echtzeit erkunden. Reddit Ads verbindet zielstrebige, von der Community angeregte Gespräche mit flexiblen Anzeigenformaten und einem robusten Targeting, um Werbetreibenden dabei zu helfen, engagierte Zielgruppen zu erreichen, Leistungsergebnisse zu erzielen und direkt von den Communities zu lernen, die die Kultur online prägen. Dieses Handbuch richtet sich an Werbetreibende und Medien-Teams, die Adobe Experience Platform verwenden, um Zielgruppen an Reddit Ads zu senden. Es behandelt, was Sie benötigen, um Ihre Konten zu verbinden, Identitäten zuzuordnen und Zielgruppen zu aktivieren.
last-substantial-update: 2026-03-31T00:00:00Z
source-git-commit: c7c74ba9b5c6a66f92dc6a5403d4f2c5614c0049
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 27%

---


# [!DNL Reddit Custom Audience]-Verbindung {#reddit-custom-audience-connection}

## Überblick {#overview}

[!DNL Reddit Ads] verbinden Marken mit Menschen, die ihre Leidenschaften und Probleme aktiv in Echtzeit erkunden. Durch die Kombination von zielgerichteten, von der Community angeregten Konversationen mit flexiblen Anzeigenformaten und robustem Targeting helfen [!DNL Reddit Ads] Werbetreibenden, engagierte Zielgruppen zu erreichen, Leistungsergebnisse zu erzielen und direkt von den Communities zu lernen, die die Kultur online gestalten.

Dieses Handbuch richtet sich an Werbetreibende und Medien-Teams, die [!DNL Adobe Experience Platform] verwenden, um Zielgruppen an [!DNL Reddit Ads] zu senden. Es behandelt, was Sie benötigen, um Ihre Konten zu verbinden, Identitäten zuzuordnen und Zielgruppen zu aktivieren.

>[!IMPORTANT]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden vom [!DNL Reddit]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an <adsapi-partner-support@reddit.com>.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Reddit Custom Audience]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die [!DNL Adobe Experience Platform] Kunden mit diesem Ziel bewältigen können.

### Retargeting bestehender Kunden mit personalisierten Angeboten {#use-case-1}

Ein Online-retailer möchte bestehende Kunden über soziale Plattformen erreichen und ihnen personalisierte Angebote auf der Grundlage ihrer vorherigen Bestellungen zeigen. Der Online-retailer kann E-Mail-Adressen und Geräte-IDs (IDFA und GAID) aus dem eigenen CRM in die [!DNL Adobe Experience Platform] aufnehmen, Zielgruppen aus eigenen Offline-Daten erstellen und diese Zielgruppen an [!DNL Reddit Ads] senden, wodurch die Werbeausgaben optimiert werden.

## Voraussetzungen {#prerequisites}

Bevor Sie dieses Ziel konfigurieren, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* Ein [!DNL Reddit Ads] Konto, das benutzerdefinierte Zielgruppen und Kundenlisten verwenden darf.
* Berechtigung zum Autorisieren der Verbindung. Dies muss ein Benutzer sein, der sich bei [!DNL Reddit] anmelden und den Zugriff für [!DNL Experience Platform] zur Verwaltung von Zielgruppen im Namen des Werbekontos genehmigen kann.
* Ihre [!DNL Reddit]-ID des Werbekontos: Die Kennung für das Werbekonto, in dem Zielgruppen erstellt werden. Ihre Werbekonto-ID finden Sie unter [Konten](https://ads.reddit.com/accounts). Beispiel: `a2_1b2c34d`.

## Unterstützte Identitäten {#supported-identities}

[!DNL Reddit Custom Audience] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
| --- | --- | --- |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | [!DNL Adobe Experience Platform] unterstützt sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Apply transformation]** , sodass [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| Dienstmädchen | Google Advertising ID oder Apple ID für Advertiser, beide mit dem SHA256-Algorithmus gehasht | Ordnen Sie entweder GAID oder IDFA **Dienstmädchen** zu. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Apply transformation]** , sodass [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
| --- | --- | --- |
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den [!DNL Experience Platform]Segmentierungs[Service) generiert ](../../../segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | Ja | Diese Kategorie enthält alle Zielgruppenursprünge außerhalb von Zielgruppen, die durch den Segmentierungs-Service generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). |

{style="table-layout:auto"}

Unterstützte Zielgruppen nach Datentyp:

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
| --- | --- | --- | --- |
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Ja | Basierend auf Kundenprofilen können Sie bestimmte Personengruppen für Marketing-Kampagnen ansprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Sammlungen strukturierter Daten, die im Data Lake von [!DNL Adobe Experience Platform] gespeichert sind. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
| --- | --- | --- |
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im [!DNL Reddit Custom Audience]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Connect to destination]** aus.

![Der Bildschirm Benutzerdefinierte Zielgruppenauthentifizierung für Reddit mit den Feldern, die für die Verbindung erforderlich sind.](../../assets/catalog/advertising/redditcustomaudience/configure_new_destination_fields.png)

Sie werden umgeleitet, um sich bei [!DNL Reddit] anzumelden. Wählen Sie nach der Überprüfung der angeforderten Berechtigungen **[!UICONTROL Allow]** aus, damit [!DNL Experience Platform] Zielgruppen erstellen und die Mitgliedschaft im Namen Ihres Werbekontos aktualisieren können.

![Der Bildschirm OAuth-Berechtigung bearbeiten.](../../assets/catalog/advertising/redditcustomaudience/reddit_oauth.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Der Bildschirm Benutzerdefiniertes Zielgruppenziel für Reddit](../../assets/catalog/advertising/redditcustomaudience/reddit_account_details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel erkennen.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Ad Account ID]**: Ihre [!DNL Reddit]-Werbekonto-ID.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Die folgenden Zielidentitäts-Namespaces müssen je nach Anwendungsfall zugeordnet werden:

| Quellfeld | Zielfeld | Anmerkungen |
| --- | --- | --- |
| E-Mail (Nur-Text oder gehasht) | email_lc_sha256 | Ihr Quellfeld kann gehasht oder unhasht sein. [!DNL Reddit] akzeptiert nur Hash-Werte. Aktivieren Sie **[!UICONTROL Apply transformation]**, sodass [!DNL Experience Platform] die E-Mail vor dem Senden hasst. |
| MAID (Nur-Text oder Hash) | Dienstmädchen | Ihr Quellfeld kann gehasht oder unhasht sein. [!DNL Reddit] akzeptiert nur Hash-Werte. Aktivieren Sie **[!UICONTROL Apply transformation]**, sodass [!DNL Experience Platform] den Wert vor dem Senden hasst. |

Sie müssen mindestens eine der Identitäten zuordnen.

![Der Bildschirm für die Identitätszuordnung mit Quell- und Zielfeldern, die für die benutzerdefinierte Reddit-Zielgruppe konfiguriert sind.](../../assets/catalog/advertising/redditcustomaudience/mapping.png)

## Exportierte Daten/Datenexport validieren {#exported-data}

Nach der Aktivierung Ihrer Zielgruppen können Sie sie in Ihrem [!DNL Reddit] Ads Manager-Konto sehen.

Zielgruppen, die neu in [!DNL Reddit] erstellt wurden, befinden sich im Status „Ausstehend“. Sobald Ihr Datenfluss ausgeführt und Profile exportiert wurden, gleicht [!DNL Reddit] die Profile mit [!DNL Reddit] Benutzern ab. Nach der Verarbeitung der Daten ändert sich der Zielgruppenstatus in **[!UICONTROL Valid]**. Die Zielgruppengröße muss mindestens [1.000 Benutzer](https://ads-api.reddit.com/docs/v3/manage-customer-lists) erreichen, um als gültig zu gelten. Zielgruppen, die die erforderliche Größe nicht erreichen, werden als **[!UICONTROL Invalid]** angezeigt.

![Der Reddit Ads Manager, der eine exportierte Zielgruppe und ihren Status anzeigt.](../../assets/catalog/advertising/redditcustomaudience/see_audience_in_reddit.png)

Im Folgenden finden Sie ein Beispiel für die an [!DNL Reddit] gesendete Payload:

```json
{
  "data": {
    "action_type": "ADD",
    "column_order": [
      "EMAIL_SHA256",
      "MAID_SHA256"
    ],
    "user_data": [
      [
        "d7ef2e7b2a3663c25284a3d6d13b1ca727fc8c659474b81afe0cec997a4737d2",
        "510870d7b3e47a28a2b2f3aef27a4c81aab0b2eefda27dea50bc4c991d9e5435"
      ]
    ]
  }
}
```

Weitere Informationen finden [ in der ](https://ads-api.reddit.com/docs/v3/operations/Update%20Custom%20Audience%20Users) zur Reddit-API .

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Weitere Ressourcen {#additional-resources}

Weitere Informationen zur Funktionsweise des Endpunkts für benutzerdefinierte Zielgruppen finden [ in der ](https://ads-api.reddit.com/docs/v3/operations/Update%20Custom%20Audience%20Users) zur Reddit-API .
