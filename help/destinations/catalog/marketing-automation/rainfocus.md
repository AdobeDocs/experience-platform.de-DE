---
title: RainFocus-Teilnehmerprofile
description: Erfahren Sie, wie Sie mit dem Ziel-Connector für RainFocus-Teilnehmerprofile Zielgruppenprofile mit dem globalen RainFocus-Teilnehmerprofil synchronisieren können.
last-substantial-update: 2024-12-17T00:00:00Z
exl-id: 27c3848c-411a-4305-a5d5-00b145b95287
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 44%

---

# RainFocus-Teilnehmerprofile {#rainfocus-destination}

## Überblick {#overview}

Verwenden Sie das [!DNL RainFocus Attendee Profiles] Ziel, um Kundenprofile aus Adobe Experience Platform in die [!DNL RainFocus] zu streamen, um Teilnehmerprofile zu erstellen und zu aktualisieren.

>[!IMPORTANT]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom [!DNL RainFocus]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an `clientcare@rainfocus.com` oder besuchen Sie das RainFocus [Hilfezentrum](https://help.rainfocus.com/hc/en-us).

## Anwendungsszenarien {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das RainFocus-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel bewältigen können.

### Anwendungsfall #1 {#use-case-1}

Ein großes Unternehmen im Bereich Unternehmenstechnologie wird sich für die bevorstehende globale Expo registrieren lassen und möchte Kundenprofile an [!DNL RainFocus] senden, um den Registrierungsprozess zu optimieren.

### Anwendungsfall #2 {#use-case-2}

Eine Finanzdienstleistungsmarke wird eine Reihe von Roadshows veranstalten, die sich an neue und bestehende Kunden richten. Sie verfügen über eine Reihe von Zielgruppensegmenten mit Zielkunden in Adobe Experience Platform. Mithilfe des [!DNL RainFocus]-Ziel-Connectors können diese Profile einfach zur Aktivierung an [!DNL RainFocus] gesendet werden.

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
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Experience Platform] die Daten bei Aktivierung automatisch hasht. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Art von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Geben Sie Authentifizierungsdetails für den RainFocus-Ziel-Connector an](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-authentication.png)

* **[!UICONTROL Client-ID]**: Füllen Sie die vom RainFocus-API-Profil bereitgestellten [!DNL Client ID] aus.
* **[!UICONTROL Client-Geheimnis]**: Füllen Sie die vom RainFocus-API-Profil bereitgestellten [!DNL Client Secret] aus.
* **[!UICONTROL Umgebung]**: Geben Sie an, mit welcher RainFocus-Umgebung Sie eine Verbindung herstellen möchten, z. B. `dev`, `prod`.
* **[!UICONTROL Org ID]**: Geben Sie die eindeutige `orgid` für Ihre Instanz von RainFocus an.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Angeben von Verbindungsdetails für den RainFocus-Ziel-Connector](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-configure-destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Ereignis-ID]**: Ihre [!DNL RainFocus] Ereigniscode-Kennung, an die Profile gesendet werden sollen.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffssteuerung – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

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

## Zusätzliche Ressourcen {#additional-resources}

* [RainFocus Streaming Source-Connector](https://experienceleague.adobe.com/de/docs/experience-platform/sources/connectors/analytics/rainfocus)
