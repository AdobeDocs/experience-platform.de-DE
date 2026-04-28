---
title: Wurzel
description: Erfahren Sie, wie Sie Adobe Experience Platform-Zielgruppen mit Root verbinden, um die Kampagnenleistung durch intelligentere Zielgruppenbestimmung, Unterdrückung und Personalisierung zu verbessern.
source-git-commit: a281a7c961b8576105913feb7a7f8258c975e875
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 25%

---


# [!DNL Rokt]-Verbindung {#rokt-destination}

## Überblick {#overview}

[[!DNL Rokt]](https://www.rokt.com) nutzt den Wert von eCommerce mithilfe von KI-gestützter Echtzeit-Entscheidungsfindung, um jeden ™ relevanter zu machen. Es bietet personalisierte Erlebnisse und verbindet Werbetreibende mit Kunden mit hohen Absichten. Verbinden Sie [!DNL Adobe Experience Platform] Zielgruppen, um die Kampagnenleistung durch intelligentere Zielgruppenbestimmung, Unterdrückung und Personalisierung zu [!DNL Rokt]. Erreichen Sie die richtigen Kunden zur richtigen Zeit und reduzieren Sie gleichzeitig verschwendete Ausgaben.

>[!IMPORTANT]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom [!DNL Rokt]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte an Ihren [!DNL Rokt] Account Manager oder kontaktieren Sie uns unter `support@rokt.com`.

## Anwendungsfälle {#use-cases}

Die folgenden Anwendungsfälle zeigen, wie [!DNL Experience Platform] Kunden das [!DNL Rokt]-Ziel verwenden können.

### Anwendungsfall #1: Retargeting {#use-case-1}

Erneutes Ansprechen von Kunden mit hohen Absichten, die Ihre Site oder Ihr Programm besucht, aber nicht konvertiert haben. Erstellen Sie eine Zielgruppe in [!DNL Experience Platform], einschließlich Benutzender, die bestimmte Produktkategorien durchsucht oder einen Checkout-Fluss abgebrochen haben. Pushen Sie diese Zielgruppe dann zu [!DNL Rokt], um personalisierte Angebote am Point of Purchase auf Partner-Sites bereitzustellen. [!DNL Rokt] erfolgt innerhalb des Transaktionszeitpunkts, unmittelbar nachdem ein Kunde einen Kauf an einer anderen Stelle abgeschlossen hat. Retargeting-Zielgruppen werden erreicht, wenn die Kaufabsicht ihren Höhepunkt erreicht. Dies führt zu höheren Konversionsraten als das herkömmliche Display-Retargeting.

### Anwendungsfall #2: Unterdrückungslisten {#use-case-2}

Vermeiden Sie verschwendete Ausgaben und irrelevante Erlebnisse, indem Sie Zielgruppen unterdrücken, die bestimmte [!DNL Rokt]-Angebote nicht erhalten sollten. Häufige Anwendungsfälle für die Unterdrückung sind der Ausschluss von Konvertern, Mitgliedern des Treueprogramms, die an einer aktiven Promotion teilnehmen, oder Benutzer, die sich gegen das Marketing entschieden haben. Schließen Sie beispielsweise Kunden aus, die in den letzten 30 Tagen gekauft haben. Synchronisieren Sie diese Unterdrückungszielgruppen von [!DNL Experience Platform] zu [!DNL Rokt] in Echtzeit. Dadurch bleiben Kampagnen auf neue oder erneut kontaktierbare Benutzende ausgerichtet. Dies verbessert den ROI und schützt das Kundenerlebnis.

## Voraussetzungen {#prerequisites}

Bevor Sie das [!DNL Rokt]-Ziel in [!DNL Adobe Experience Platform] einrichten, müssen Sie die folgenden Anmeldeinformationen von Ihrem **[!DNL Rokt]Account Manager abrufen**:

* **API-Schlüssel**: Verwenden Sie dies als **[!UICONTROL Username]** beim [Authentifizieren der Zielverbindung](#authenticate).
* **API-Geheimnis**: Verwenden Sie dies als **[!UICONTROL Password]** beim [Authentifizieren der Zielverbindung](#authenticate).

Ihr [!DNL Rokt] Account Manager stellt diese Anmeldeinformationen vor Ihrer Einrichtung auf der [!DNL Rokt]-Plattform bereit. Wenden Sie sich an Ihren Kundenbetreuer, falls Sie diese noch nicht erhalten haben.

## Unterstützte Identitäten {#supported-identities}

[!DNL Rokt] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| email | Nur-Text-E-Mail-Adresse | Empfohlen. Wird für die Profilzuordnung in [!DNL Rokt] verwendet. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, wählen Sie die Option **[!UICONTROL Apply transformation]** aus, damit die Daten bei Aktivierung automatisch gehasht [!DNL Experience Platform]. |
| phone | Nur-Text-Telefonnummer | Wird für die Profilzuordnung in [!DNL Rokt] verwendet. |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, wählen Sie die Option **[!UICONTROL Apply transformation]** aus, damit die Daten bei Aktivierung automatisch gehasht [!DNL Experience Platform]. |
| GAID | Advertising-ID [!DNL Google] | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | [!DNL Apple]-ID für Werbetreibende | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| aepProfileId | [!DNL Adobe Experience Platform] Profilkennung | Ordnet die Profil-ID (`xdm:_id`) als Fallback-Kennung zu. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über die [!DNL Experience Platform]-[[!DNL Segmentation Service]](/help/segmentation/home.md) generiert wurden. |
| Alle anderen Ursprünge der Zielgruppe | Ja | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li> benutzerdefinierte Upload-[ (importiert](/help/segmentation/ui/audience-portal.md#import-audience) in [!DNL Experience Platform] aus CSV-Dateien,</li><li> Lookalike-Zielgruppen, </li><li> Federated Audiences, </li><li> in anderen [!DNL Experience Platform]-Apps generierte Zielgruppen wie [!DNL Adobe Journey Optimizer], </li><li> und mehr. </li></ul> |

{style="table-layout:auto"}

Unterstützte Zielgruppen nach Zielgruppen-Datentyp:

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
|--------------------|-----------|-------------|-----------|
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Ja | Basierend auf Kundenprofilen. Verwenden Sie diese, um bestimmte Personengruppen für Marketing-Kampagnen anzusprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Sammlungen strukturierter Daten, die im Data Lake von [!DNL Adobe Experience Platform] gespeichert sind. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (E-Mail, Telefon, Smartphone-Anzeige oder andere), die im [!DNL Rokt]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in [!DNL Experience Platform] auf der Grundlage einer Zielgruppenbewertung aktualisiert wird, sendet der Connector die Aktualisierung nachgelagert an [!DNL Rokt]. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](/help/destinations/ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Connect to destination]** aus.

* **[!UICONTROL Username]**: Ihr API-Schlüssel, bereitgestellt von Ihrem [!DNL Rokt] Account Manager.
* **[!UICONTROL Password]**: Ihr API-Geheimnis, bereitgestellt von Ihrem [!DNL Rokt] Account Manager.

  ![Der Bildschirm [!DNL Rokt] Zielkonfiguration in [!DNL Experience Platform] mit ausgefüllten Kontodetails, Authentifizierungsfeldern und Zieldetails.](/help/destinations/assets/catalog/advertising/rokt/aep-configure-destination.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können (z. B. &quot;[!DNL Rokt] - Retargeting von Zielgruppen„).
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](/help/destinations/ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Das [!DNL Rokt]-Ziel unterstützt die Zuordnung von Identity-Namespaces von [!DNL Experience Platform] zu [!DNL Rokt] Identitätsfeldern. Sie müssen mindestens eine Identität zuordnen, um eine Zielgruppe erfolgreich aktivieren zu können. Die empfohlenen Zuordnungen sind in der folgenden Tabelle aufgeführt.

| Quellfeld | Zielfeld | Zu beachten |
|---|---|---|
| `IdentityMap: Email` | `Identity: email` | Empfohlen |
| `IdentityMap: Email_LC_SHA256` | `Identity: emailSha256` | Empfohlen |
| `IdentityMap: Phone` | `Identity: phone` | Optional |
| `IdentityMap: Phone_SHA256` | `Identity: phoneSha256` | Optional |
| `IdentityMap: GAID` | `Identity: gaid` | Optional |
| `IdentityMap: IDFA` | `Identity: idfa` | Optional |
| `xdm: _id` | `Identity: aepProfileId` | Optional |

{style="table-layout:auto"}

Im Folgenden finden Sie ein Beispiel für eine vollständige Zuordnung:

![Der Zuordnungsschritt des Zielaktivierungs-Workflows für [!DNL Rokt] in [!DNL Experience Platform], mit konfigurierten Quell- und Ziel-Identitätsfeldern.](/help/destinations/assets/catalog/advertising/rokt/aep-identity-mapping.png)

>[!NOTE]
>
>Es wird dringend mindestens eine E-Mail-basierte Identitätszuordnung (`email` oder `emailSha256`) empfohlen, um die Übereinstimmungsraten in [!DNL Rokt] zu maximieren.

### Konfigurieren des Zielgruppen-Zeitplans {#audience-schedule}

Konfigurieren Sie nach Abschluss des Zuordnungsschritts einen Zielgruppen-Zeitplan für jede ausgewählte Zielgruppe. Geben Sie einen **[!UICONTROL Start date]** für den Beginn der Synchronisierung der Zielgruppe und einen **[!UICONTROL Mapping ID]** (einen Titel, mit dem diese Zielgruppe in [!DNL Rokt] identifiziert wird) an. Sie können den Namen der [!DNL Experience Platform] Zielgruppe oder eine beliebige beschreibende Zeichenfolge verwenden, die Ihnen und Ihrem [!DNL Rokt] Account Manager bei der Identifizierung der Zielgruppe hilft.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Weitere Ressourcen {#additional-resources}

* [[!DNL Rokt] Entwicklerdokumentation](https://docs.rokt.com)
* [Adobe Experience Platform-Ziele - Übersicht](/help/destinations/home.md)
