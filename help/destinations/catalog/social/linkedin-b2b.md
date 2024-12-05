---
title: (Firmen) LinkedIn-Verbindung
description: Verwenden Sie dieses Ziel, um Ihre Zielgruppen für Account-Based Marketing (ABM) zu aktivieren. Aktivieren Sie Profile für Ihre LinkedIn-Kampagnen für Zielgruppen-Targeting, Personalisierung und Unterdrückung basierend auf Hash-E-Mails.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
source-git-commit: e45c50a6447be4a60145eea6956d30d51166e675
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 25%

---

# (Firmen) Verbindung von LinkedIn Match Audiences {#companies-linkedin}

>[!AVAILABILITY]
>
>Die Funktion zum Aktivieren von Kontozielgruppen für das LinkedIn-Ziel (Unternehmen) ist für Unternehmen verfügbar, die die Editionen [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) und [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) von Real-time Customer Data Platform erwerben.

Verwenden Sie dieses Ziel, um Ihre [Konto-Zielgruppen](/help/segmentation/ui/account-audiences.md) für Account-Based Marketing (ABM) zu aktivieren. Werben Sie über das Ziel &quot;**[!UICONTROL (Unternehmen) LinkedIn]**&quot;für relevante Rollen und Rollen in Ihren Zielkonten. Weitere Informationen zum Konto-Targeting](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting) finden Sie in der LinkedIn-Dokumentation auf der LinkedIn-Plattform.[

>[!TIP]
>
>Für Anwendungsfälle auf individueller Ebene (oder zwischen Unternehmen und Verbrauchern) empfiehlt Adobe, das Ziel [LinkedIn Matched Audience](/help/destinations/catalog/social/linkedin.md) zu verwenden.

![LinkedIn-Konto-Ziel in der Experience Platform-Benutzeroberfläche angezeigt.](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die durch den Experience Platform [Segmentierungsdienst](../../../segmentation/home.md) generiert wurden. |
| Benutzerdefinierte Uploads | X | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-and-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|--------------|-----------|---------------------------|
| Exporttyp | Zielgruppenexport | Alle Zielgruppenmitglieder werden mit Schlüsselkennungen wie Name, Telefonnummer und mehr exportiert. |
| Häufigkeit | Streaming | &quot;Always-on&quot;-API-basierte Verbindungen. Aktualisierungen werden unmittelbar nach Profiländerungen nachgelagert gesendet. |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

Stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen, um Kontozielgruppen nach LinkedIn zu exportieren:

### Voraussetzungen für linkedIn-Konten {#LinkedIn-account-prerequisites}

Bevor Sie das Ziel &quot;[!UICONTROL (Unternehmen) LinkedIn Matched Audience]&quot;verwenden können, stellen Sie sicher, dass Ihr [!DNL LinkedIn Campaign Manager]-Konto über die Berechtigungsebene [!DNL Creative Manager] oder höher verfügt.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager] -Benutzerberechtigungen finden Sie unter [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Advertising-Konten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

1. Suchen Sie das Ziel &quot;[!DNL (Companies) LinkedIn Matched Audiences]&quot;im Zielkatalog und wählen Sie &quot;**[!UICONTROL Einrichten]**&quot;.
2. Wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.
   ![Bei LinkedIn authentifizieren](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. Geben Sie Ihre LinkedIn-Anmeldedaten ein und wählen Sie **Anmelden** aus.

Nach Abschluss des Anmeldeprozesses mit LinkedIn können Sie mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre [!DNL LinkedIn Campaign Manager Account ID]. Sie finden diese ID in Ihrem [!DNL LinkedIn Campaign Manager] -Konto.

Sie können jetzt Kontozielgruppen für LinkedIn aktivieren.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Kontozielgruppen für Ziele zu aktivieren.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Kontozielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Kontozielgruppen für dieses Ziel finden Sie unter [Aktivieren von Kontozielgruppen](/help/destinations/ui/activate-account-audiences.md) .

## Erforderliche Zuordnungspaare im Zuordnungsschritt bei der Aktivierung von Kontozielgruppen für das Ziel **[!UICONTROL (Unternehmen) LinkedIn Matched Audiences]** {#required-mappings}

Beachten Sie beim Aktivieren von Kontozielgruppen für das Ziel &quot;**[!UICONTROL (Unternehmen) LinkedIn Matched Audiences]**&quot;, dass die folgenden beiden Zuordnungspaare für den erfolgreichen Export von Daten obligatorisch sind:

![Erforderliche Felder für die LinkedIn-Zuordnung.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Quellfeld | Zielfeld |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (Wählen Sie dieses Feld in der Ansicht **[!UICONTROL Identitäts-Namespace auswählen]** aus, wenn Sie das **[!UICONTROL Zielfeld]** auswählen). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Kontozielgruppen für Ziele zu aktivieren.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Kontozielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

## Exportierte Daten {#exported-data}

Eine erfolgreiche Aktivierung bedeutet, dass eine benutzerdefinierte Zielgruppe vom Typ [!DNL LinkedIn] programmgesteuert in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login) erstellt wird. Die Zielgruppenmitgliedschaft wird angepasst, wenn Benutzer für die aktivierten Zielgruppen qualifiziert oder disqualifiziert sind.