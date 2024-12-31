---
title: (Firmen) LinkedIn-Verbindung
description: Verwenden Sie dieses Ziel, um Ihre Konto-Zielgruppen für Account-Based Marketing-Anwendungsfälle (ABM) zu aktivieren. Aktivieren Sie Profile für Ihre LinkedIn-Kampagnen zum Zielgruppen-Targeting, zur Personalisierung und zur Unterdrückung, basierend auf gehashten E-Mails.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P-Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: 68d2cca3-952b-49d0-8ea2-e776a233b752
source-git-commit: e1a81f9f81a6499683055a280a935684ab4463eb
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 25%

---

# (Firmen) LinkedIn Match Audiences-Verbindung {#companies-linkedin}

>[!AVAILABILITY]
>
>Die Funktion zum Aktivieren von Account-Zielgruppen für das LinkedIn-Ziel (Unternehmen) ist für Unternehmen verfügbar, die die [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b)- und [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p)-Editionen von Real-time Customer Data Platform erwerben.

Verwenden Sie dieses Ziel, um Ihre [Account-Zielgruppen](/help/segmentation/ui/account-audiences.md) für Account-Based Marketing (ABM)-Anwendungsfälle zu aktivieren. Werben Sie über das **[!UICONTROL (Companies) LinkedIn]** Business-to-Business-Ziel für relevante Personas und Rollen in Ihren Zielkonten. Besuchen Sie die LinkedIn-Dokumentation[ um mehr über Account-](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting) auf der LinkedIn-Plattform zu erfahren.

>[!TIP]
>
>Für Anwendungsfälle auf individueller Ebene (oder zwischen Unternehmen und Privatkunden) empfiehlt Adobe die Verwendung des Ziels [Zielgruppe mit LinkedIn-Abgleich](/help/destinations/catalog/social/linkedin.md).

![Ziel des LinkedIn-Kontos wird auf der Experience Platform-Benutzeroberfläche angezeigt.](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Art von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform ([-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | X | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-and-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|--------------|-----------|---------------------------|
| Exporttyp | Zielgruppenexport | Alle Mitglieder der Zielgruppe werden mit Schlüsselkennungen wie Name, Telefonnummer und mehr exportiert. |
| Häufigkeit | Streaming | „Always-on“-API-basierte Verbindungen. Aktualisierungen werden nachgelagert sofort nach Profiländerungen gesendet. |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

Stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen, um Konto-Zielgruppen in LinkedIn zu exportieren:

### Voraussetzungen für das linkedIn-Konto {#LinkedIn-account-prerequisites}

Bevor Sie das Ziel [!UICONTROL (Unternehmen) LinkedIn Matched Audience] verwenden können, stellen Sie sicher, dass Ihr [!DNL LinkedIn Campaign Manager]-Konto über die [!DNL Creative Manager] Berechtigungsstufe oder höher verfügt.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager]-Benutzerberechtigungen finden Sie unter [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Advertising-Konten](https://www.linkedin.com/help/lms/answer/5753) in der Dokumentation zu LinkedIn.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

1. Suchen Sie das [!DNL (Companies) LinkedIn Matched Audiences] im Zielkatalog und wählen Sie **[!UICONTROL Einrichten]**.
2. Wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.
   ![Authentifizierung bei LinkedIn](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. Geben Sie Ihre LinkedIn-Anmeldeinformationen ein und wählen Sie **Anmelden** aus.

Nach Abschluss des Anmeldevorgangs mit LinkedIn können Sie mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre [!DNL LinkedIn Campaign Manager Account ID]. Diese ID finden Sie in Ihrem [!DNL LinkedIn Campaign Manager].

Sie können jetzt Account-Zielgruppen für LinkedIn aktivieren.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Konto-Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Konto-Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [ Aktivieren von Konto-Zielgruppen für ](/help/destinations/ui/activate-account-audiences.md) Ziel finden Sie unter „Aktivieren von Konto-Zielgruppen“.

## Erforderliche Zuordnungspaare im Zuordnungsschritt beim Aktivieren von Konto-Zielgruppen für das Ziel **[!UICONTROL Abgestimmte Zielgruppen von LinkedIn (Unternehmen]** {#required-mappings}

Beachten Sie beim Aktivieren von Konto-Zielgruppen für das Ziel &quot;**[!UICONTROL (Unternehmen) LinkedIn Matched Audiences]**, dass die folgenden beiden Zuordnungspaare obligatorisch sind, um Daten erfolgreich zu exportieren:

![Erforderliche Felder für die LinkedIn-Zuordnung.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Quellfeld | Zielfeld |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (wählen Sie dieses Feld in der Ansicht **[!UICONTROL Identity-Namespace auswählen]** bei Auswahl **[!UICONTROL Zielfeld]** aus). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Konto-Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Konto-Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

## Exportierte Daten {#exported-data}

Eine erfolgreiche Aktivierung bedeutet, dass eine [!DNL LinkedIn] benutzerdefinierte Zielgruppe programmgesteuert in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login) erstellt wird. Die Zielgruppenzugehörigkeit wird angepasst, da Benutzende für die aktivierten Zielgruppen qualifiziert oder disqualifiziert werden.
