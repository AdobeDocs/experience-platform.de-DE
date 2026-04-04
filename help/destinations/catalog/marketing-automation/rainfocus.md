---
title: RainFocus-Teilnehmerprofile
description: Erfahren Sie, wie Sie mit dem Ziel-Connector für RainFocus-Teilnehmerprofile Zielgruppenprofile mit dem globalen RainFocus-Teilnehmerprofil synchronisieren können.
last-substantial-update: 2024-12-17T00:00:00Z
exl-id: 27c3848c-411a-4305-a5d5-00b145b95287
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 30%

---

# RainFocus-Teilnehmerprofile {#rainfocus-destination}

## Überblick {#overview}

Verwenden Sie das [!DNL RainFocus Attendee Profiles]-Ziel, um Kundenprofile aus [!DNL Adobe Experience Platform] in die [!DNL RainFocus]-Plattform zu streamen, um Teilnehmerprofile zu erstellen und zu aktualisieren.

>[!IMPORTANT]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom [!DNL RainFocus]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an `clientcare@rainfocus.com` oder besuchen Sie das RainFocus [Hilfezentrum](https://help.rainfocus.com/hc/en-us).

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das RainFocus-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die [!DNL Adobe Experience Platform] Kunden mit diesem Ziel bewältigen können.

### Anwendungsfall #1 {#use-case-1}

Ein großes Unternehmen im Bereich Unternehmenstechnologie wird sich für die bevorstehende globale Expo registrieren lassen und möchte Kundenprofile zur Optimierung des Registrierungsprozesses an [!DNL RainFocus] senden.

### Anwendungsfall #2 {#use-case-2}

Eine Finanzdienstleistungsmarke wird eine Reihe von Roadshows veranstalten, die sich an neue und bestehende Kunden richten. Sie verfügen über eine Reihe von Zielgruppensegmenten mit Zielkunden in [!DNL Adobe Experience Platform]. Mithilfe des [!DNL RainFocus]-Ziel-Connectors können diese Profile einfach zur Aktivierung an [!DNL RainFocus] gesendet werden.

## Voraussetzungen {#prerequisites}

Bevor Sie das [!DNL RainFocus]-Ziel verwenden können, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* Erstellen eines [!DNL RainFocus] API-Profils mit OAuth (global).
   * Der **Attendee Store**-Endpunkt muss aktiviert sein.
   * Es müssen **Client** ID und **Client-**&quot; generiert werden.

Sie müssen außerdem über eine RainFocus-Kennung **Ereigniscode** verfügen, an die Profile gesendet werden sollen.

## Unterstützte Identitäten {#supported-identities}

[!DNL RainFocus] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | [!DNL Adobe Experience Platform] unterstützt sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Apply transformation]** , damit die Daten bei Aktivierung automatisch gehasht [!DNL Experience Platform]. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Art von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
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
| Exporttyp | **[!UICONTROL Profile-based]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigung[. ](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Connect to destination]** aus.

![Geben Sie Authentifizierungsdetails für den RainFocus-Ziel-Connector an](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-authentication.png)

* **[!UICONTROL Client ID]**: Füllen Sie die vom RainFocus-API-Profil bereitgestellten [!DNL Client ID] aus.
* **[!UICONTROL Client secret]**: Füllen Sie die vom RainFocus-API-Profil bereitgestellten [!DNL Client Secret] aus.
* **[!UICONTROL Environment]**: Geben Sie an, mit welcher RainFocus-Umgebung Sie eine Verbindung herstellen möchten, z. B. `dev`, `prod`.
* **[!UICONTROL Org ID]**: Geben Sie die eindeutige `orgid` für Ihre Instanz von RainFocus an.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Angeben von Verbindungsdetails für den RainFocus-Ziel-Connector](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-configure-destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Event ID]**: Ihre [!DNL RainFocus] Ereigniscode-Kennung, an die Profile gesendet werden sollen.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen [ Aktivieren von Zielgruppen für dieses Ziel finden ](/help/destinations/ui/activate-segment-streaming-destinations.md) unter Aktivieren von Zielgruppen für Streaming-Ziele .

### Zuordnen von Attributen und Identitäten {#map}

Die folgenden Ziel-Identity-Namespaces müssen je nach Anwendungsfall zugeordnet werden:

* **E** Mail) muss als Zielfeld mithilfe von zugeordnet werden **Zielfeld > Identity-Namespace auswählen > E-Mail**

![Zuordnen von Profil- und Identitätsfeldern](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-mapping.png)

Es wird empfohlen, zusätzliche Profilfelder zuzuordnen, um sicherzustellen, dass das Teilnehmerprofil in [!DNL RainFocus] vollständig ausgefüllt ist. Die folgenden Zielfelder sind in [!DNL RainFocus] verfügbar:

| Zielfeld | Beschreibung |
|------------|-------------|
| `address1` | Die erste Zeile der Straßenadresse |
| `address2` | Die zweite Zeile der Straßenadresse (falls zutreffend) |
| `city` | Der Stadtname |
| `companyname` | Der Name der Firma |
| `countryid` | Eine ISO 3166-1 Alpha-2-Ländercodekennung für das Land |
| `email` | Die E-Mail-Adresse |
| `firstname` | Der Vorname der Person |
| `lastname` | Der Nachname der Person |
| `jobtitle` | Die Berufsbezeichnung der Person |
| `phone` | Die Telefonnummer |
| `state` | Der FIPS-Alpha-Code des Bundeslandes oder der Provinz |
| `zip` | Die Postleitzahl oder Postleitzahl |

{style="table-layout:auto"}

## Exportierte Daten/Datenexport validieren {#exported-data}

Nachdem ein Profilsatz an [!DNL RainFocus] gesendet wurde, verwenden Sie die API-Profilprotokollierung [!DNL RainFocus] , um zu überprüfen, ob die Profile erfolgreich aufgenommen wurden.

![Anzeigen von Protokollen im API-Profil in RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-profile.png)

![Überprüfen Sie, ob Profile erfolgreich aufgenommen wurden](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-logging.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Weitere Ressourcen {#additional-resources}

* [RainFocus Streaming Source-Connector](https://experienceleague.adobe.com/de/docs/experience-platform/sources/connectors/analytics/rainfocus)
