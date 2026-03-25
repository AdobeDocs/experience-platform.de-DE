---
title: Audience Analysis-Ziel
description: Zeigen Sie Zielgruppen an, für die sich Kundinnen und Kunden in Customer Journey Analytics qualifizieren.
badgeLimitedAvailability: label="Eingeschränkte Verfügbarkeit" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
hide: true
hidefromtoc: true
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 23%

---

# Audience Analysis-Ziel

Mit dem [!UICONTROL Audience Analysis] Ziel können Sie [!DNL Adobe Experience Platform] Zielgruppendaten in [Customer Journey Analytics &#x200B;](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=de). Sie können auswählen, welche Zielgruppen in die resultierenden angereicherten Daten aufgenommen werden sollen. Zielgruppenqualifikationen sind dann als Dimensionen in [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html)-Berichten verfügbar.

>[!AVAILABILITY]
>
>Dieses Ziel befindet sich in einer eingeschränkten Testphase. Wenn Sie an der Verwendung dieses Ziels interessiert sind, wenden Sie sich an Ihr Adobe Account Team.

## Voraussetzungen {#prerequisites}

Vor der Verwendung dieses Ziels ist Folgendes erforderlich:

* Sie müssen für die Verwendung des Zielgruppenanalyseziels bereitgestellt werden. Wenn Sie noch nicht für die Verwendung dieses Ziels bereitgestellt wurden, wenden Sie sich an Ihr Adobe-Accountteam.
* Sie müssen für die Verwendung von Customer Journey Analytics bereitgestellt werden.
* Mindestens eine Zielgruppe muss in [!DNL Adobe Experience Platform] erstellt worden sein.

## Unterstützte Identitäten {#supported-identities}

Die Zielgruppenanalyse unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md). Normalerweise wird eine Experience Cloud ID (ECID) verwendet.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple-ID für Werbetreibende | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: &quot;Adobe Marketing Cloud ID“, &quot;[!DNL Adobe Experience Cloud] ID“, &quot;[!DNL Adobe Experience Platform] ID“. Weitere Informationen finden Sie im folgenden Dokument [ECID](/help/identity-service/features/ecid.md) . |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | [!DNL Adobe Experience Platform] unterstützt sowohl einfache als auch SHA256-Hash-Telefonnummern. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Apply transformation]** , damit die Daten bei Aktivierung automatisch gehasht [!DNL Experience Platform]. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | [!DNL Adobe Experience Platform] unterstützt sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Apply transformation]** , damit die Daten bei Aktivierung automatisch gehasht [!DNL Experience Platform]. |
| extern_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

Bei der Verwendung dieses Ziels werden die folgenden Typen von Zielgruppen unterstützt:

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | Nein | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li> benutzerdefinierte Upload-Zielgruppen [importiert](../../../segmentation/ui/audience-portal.md#import-audience) aus CSV-Dateien in Experience Platform,</li><li> Lookalike-Zielgruppen, </li><li> Federated Audiences, </li><li> Zielgruppen, die in anderen Experience Platform-Apps generiert werden, z. B. [!DNL Adobe Journey Optimizer], </li><li> und mehr. </li></ul> |

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
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im Ziel der Zielgruppenanalyse verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil in Experience Platform auf der Grundlage einer Zielgruppenbewertung aktualisiert wird, sendet der Connector die Aktualisierung nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Neues Ziel konfigurieren {#configure-destination}

>[!IMPORTANT]
>
>Um ein Ziel zu erstellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigung[. &#x200B;](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Um dieses Ziel zu erstellen, führen Sie die Schritte aus, die im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Der Zielname.
* **[!UICONTROL Description]**: Die Zielbeschreibung.
* **[!UICONTROL Datastream ID]**: Die Datenstrom-ID, die Sie mit qualifizierten Zielgruppen anreichern möchten. Sie können diese ID im [Datenströme-Manager](/help/datastreams/overview.md) abrufen.
* **[!UICONTROL Integration alias]**: Der Integrationsalias.

### Warnhinweise {#alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

* **[!UICONTROL Activation Skipped Rate Exceed]**: Benachrichtigung erfolgt, wenn die Aktivierungsübersprungrate einen Schwellenwert überschreitet.

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

### Governance-Richtlinie und Durchsetzungsmaßnahmen {#governance-policy}

In diesem optionalen Abschnitt können Sie Ihre Data-Governance-Richtlinien definieren und sicherstellen, dass die verwendeten Daten konform sind, wenn Zielgruppen gesendet und aktiv sind.

Wenn Sie die gewünschten Marketing-Aktionen für das Ziel ausgewählt haben, klicken Sie auf **[!UICONTROL Create]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Nachdem das Ziel erstellt wurde, können Sie die gewünschten Zielgruppen für das Ziel aktivieren.

1. Wenn Sie sich noch nicht im erstellten Ziel befinden, können Sie es erneut finden, indem Sie zu **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** navigieren.
1. Wählen Sie **[!UICONTROL Activate audiences]** aus.
1. Wählen Sie die gewünschten Zielgruppen aus, für die Sie Qualifikationen analysieren möchten. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Next]** aus.
1. Überprüfen Sie die Zielkonfiguration und die Zielgruppeneinstellungen und wählen Sie dann **[!UICONTROL Finish]** aus.

Sie können weitere Zielgruppen hinzufügen, die Sie in Zukunft analysieren möchten, indem Sie zurück zur **[!UICONTROL Activate audiences]** navigieren. Zielgruppen können nach ihrer Aktivierung nicht entfernt werden.
