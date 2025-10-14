---
title: Gainsight PX-Verbindung
description: Verwenden Sie das Gainsight PX-Ziel, um Segmentierungsinformationen an die Gainsight PX-Plattform zu senden.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0ca0d34f-f866-4f59-80f8-60198fbb86be
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 37%

---

# Gainsight PX-Verbindung {#gainsight-px}

## Übersicht {#overview}

[[!DNL Gainsight PX]](https://www.gainsight.com/product-experience/) ist eine Produkterlebnisplattform, mit der Produkt-Teams verstehen können, wie Benutzer ihre Produkte verwenden, Feedback einholen und In-App-Interaktionen erstellen können, z. B. exemplarische Vorgehensweisen zu Produkten, um das Onboarding von Benutzern und die Produktakzeptanz zu fördern.

>[!IMPORTANT]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom *Gainsight PX*-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *`pxsupport@gainsight.com`*.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das *Gainsight PX*-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel bewältigen können.

### Zielgruppenbestimmung von In-App-Interaktionen {#targeting-in-app-engagements}

Ein SaaS-Unternehmen möchte seine Kunden über ein Anwendungshandbuch auf Gainsight PX ansprechen. Eine Zielgruppe, die dieses Engagement erhält, wurde auf Adobe Experience Platform erstellt. Das Gainsight PX-Ziel empfängt die Zielgruppe und stellt sie in der Gainsight PX-Umgebung bereit.

## Voraussetzungen {#prerequisites}

* Wenden Sie sich an das [!DNL Gainsight]-Supportteam und fordern Sie die Aktivierung externer Segmentfunktionen für Ihr Abonnement an.
* Generieren Sie einen OAuth-Geheimniswert für Ihr PX-Abonnement mithilfe der Schaltfläche **[!UICONTROL Neues Geheimnis generieren]** unten auf der Seite [Unternehmensdetails](https://app.aptrinsic.com/settings/subscription)
  ![Bildschirm mit Unternehmensdetails in Gainsight PX mit der Schaltfläche „Neues Geheimnis generieren“](../../assets/catalog/analytics/gainsight-px/generate_oauth_secret.png)

## Unterstützte Identitäten {#supported-identities}

Gainsight PX unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](../../../identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung |
|---|----|
| IdentifyID | Allgemeine Benutzerkennung, die eine Benutzerin oder einen Benutzer in Gainsight PX und Adobe Experience Platform eindeutig identifiziert |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Art von Zielgruppe Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---|---|---|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform ([-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | X | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---|---|---|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im [!DNL Gainsight PX]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil in Experience Platform auf der Grundlage einer Zielgruppenbewertung aktualisiert wird, sendet der Connector die Aktualisierung nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Authentifizierungs-Screenshot](../../assets/catalog/analytics/gainsight-px/auth-screen.png)

* **[!UICONTROL Kennwort]**: Das für die Anmeldung bei [[!DNL Gainsight PX]](https://app.aptrinsic.com) verwendete Kennwort
* **[!UICONTROL Client-ID]**: Die Gainsight PX-Abonnement-ID auf der [Seite „Unternehmensdetails“](https://app.aptrinsic.com/settings/subscription)
* **[!UICONTROL Client-Geheimnis]**: Das OAuth-Geheimnis, das unten auf der Seite &quot;[&quot; &#x200B;](https://app.aptrinsic.com/settings/subscription) der [!DNL Gainsight PX]-Benutzeroberfläche generiert wird.
* **[!UICONTROL Benutzername]**: Die E-Mail, mit der die Anmeldung bei der [[!DNL Gainsight PX]](https://app.aptrinsic.com)-Benutzeroberfläche erfolgt

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Bildschirm mit Zieldetails in der Experience Platform-Benutzeroberfläche, der zeigt, wie die Felder Name und Beschreibung ausgefüllt werden](../../assets/catalog/analytics/gainsight-px/destination_details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Identitäten {#map}

Dieses Ziel unterstützt die Zuordnung von Profilattributen und Identity-Namespaces. Das Zielgruppen-Mapping muss immer der Identity-Namespace **[!UICONTROL IDENTIFY_ID]** sein.

In den folgenden Beispielen erfahren Sie mehr über die Konfiguration der Zuordnung.

#### Profilattribut zuordnen {#map-profile-attribute}

Im folgenden Beispiel ist das Quellfeld ein XDM-Profilattribut, das dem Ziel-Namespace IDENTIFY_ID zugeordnet wird.

![Beispielzuordnungsbildschirm für Identity-Namespaces, der zeigt, wie die Quell- und Zielwerte ausgewählt werden](../../assets/catalog/analytics/gainsight-px/mapping_attribute.png)

#### Zuordnen eines Identity-Namespace {#map-identity-namespace}

Im folgenden Beispiel ist das Quellfeld ein Identity-Namespace (**[!UICONTROL ECID]**), der dem Zielnamespace **[!UICONTROL IDENTIFY_ID]** zugeordnet wird.

![Bildschirm für die Attributbeispielzuordnung , der zeigt, wie die Quell- und Zielwerte ausgewählt werden](../../assets/catalog/analytics/gainsight-px/mapping_identities.png)

## Exportierte Daten/Datenexport validieren {#exported-data}

Segmentierungsdaten werden von der Experience Platform an Gainsight PX gestreamt.

Segmentmetadaten werden im Bildschirm Segmente in der [!DNL Gainsight PX]-Benutzeroberfläche angezeigt.

![Bildschirm „Segmentliste“ in Gainsight PX mit externen Segmenten.](../../assets/catalog/analytics/gainsight-px/segment_metadata.png)

Informationen zur Segmentzugehörigkeit sind auf der Registerkarte Segmente des Bildschirms Audience Explorer der [!DNL Gainsight PX]-Benutzeroberfläche sichtbar.

![Audience Explorer -Bildschirm in Gainsight PX mit zugehörigen Segmenten für einen Benutzer.](../../assets/catalog/analytics/gainsight-px/PX_Segments.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
