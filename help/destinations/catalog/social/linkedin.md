---
keywords: LinkedIn-Verbindung;LinkedIn-Verbindung;LinkedIn-Ziele;LinkedIn;
title: LinkedIn Matched Audiences-Verbindung
description: Aktivieren Sie Profile für Ihre LinkedIn-Kampagnen zum Zielgruppen-Targeting, zur Personalisierung und zur Unterdrückung auf der Grundlage von gehashten E-Mails.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 6b3b830f822cc02c78d6f593c0a949d3e19ada37
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 31%

---

# [!DNL LinkedIn Matched Audiences]-Verbindung

## Übersicht {#overview}

Aktivieren Sie Profile für Ihre [!DNL LinkedIn] Kampagnen zum Zielgruppen-Targeting, zur Personalisierung und zur Unterdrückung, basierend auf gehashten E-Mails und mobilen IDs.

![LinkedIn-Ziel in der Adobe Experience Platform-Benutzeroberfläche](../../assets/catalog/social/linkedin/catalog.png)

## Anwendungsfälle

Damit Sie besser verstehen können, wie und wann Sie das [!DNL LinkedIn Matched Audiences]-Ziel verwenden, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit dieser Funktion geeignet ist.

Ein Software-Unternehmen organisiert eine Konferenz und möchte mit den Teilnehmern in Kontakt bleiben und ihnen personalisierte Angebote auf der Grundlage ihres Konferenzteilnahmestatus anzeigen. Das Unternehmen kann E-Mail-Adressen oder IDs von Mobilgeräten aus seinem eigenen [!DNL CRM] in Adobe Experience Platform aufnehmen. Dann können sie Zielgruppen aus ihren eigenen Offline-Daten aufbauen und diese Zielgruppen an die [!DNL LinkedIn] Social-Media-Plattform senden, wodurch ihre Werbeausgaben optimiert werden.

## Unterstützte Identitäten {#supported-identities}

[!DNL LinkedIn Matched Audiences] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
>
>Ab September 2025 können Sie [!DNL IDFA] nicht mehr als Zielidentität zuordnen, da [!DNL IDFA] vom [!DNL LinkedIn Matched Audiences] Ziel nicht mehr unterstützt wird. Weitere Informationen finden Sie in der [!DNL LinkedIn Matched Audiences] zur [-](https://learn.microsoft.com/en-us/linkedin/marketing/matched-audiences/create-and-manage-segment-users?view=li-lms-2025-07&tabs=http#idtypes) . Diese Änderung ist auf die Anforderungen von LinkedIn zurückzuführen und steht in keinem Zusammenhang mit Ziel-Service-Upgrades von Experience Platform.


| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [ID-](#id-matching-requirements-id-matching-requirements)-Anforderungen“ und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mails. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Experience Platform] die Daten bei Aktivierung automatisch hasht. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer und sonstiges), die im [!DNL LinkedIn Matched Audiences]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen für LinkedIn-Konto {#LinkedIn-account-prerequisites}

Bevor Sie das Ziel [!UICONTROL LinkedIn Matched Audience] verwenden können, stellen Sie sicher, dass Ihr [!DNL LinkedIn Campaign Manager]-Konto über die [!DNL Creative Manager] Berechtigungsstufe oder höher verfügt.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager]-Benutzerberechtigungen finden Sie unter [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Advertising-Konten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.

## Anforderungen für den ID-Abgleich {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] erfordert, dass keine personenbezogenen Daten (PII) in klarer Form gesendet werden. Daher können die für [!DNL LinkedIn Matched Audiences] aktivierten Zielgruppen als Hash-*(*) verschlüsselt werden, z. B. E-Mail-Adressen oder IDs von Mobilgeräten.

Je nach Typ der IDs, die Sie in Adobe Experience Platform aufnehmen, müssen Sie die entsprechenden Anforderungen erfüllen.

## Hash-Anforderungen für E-Mails {#email-hashing-requirements}

Sie können E-Mail-Adressen hashen, bevor Sie sie in Adobe Experience Platform aufnehmen, oder E-Mail-Adressen in Clear in Experience Platform verwenden und bei der Aktivierung hashen [!DNL Experience Platform].

Weitere Informationen zum Aufnehmen von E-Mail-Adressen in Experience Platform finden Sie unter [Übersicht über die Batch](/help/ingestion/batch-ingestion/overview.md)Aufnahme und [Streaming-Aufnahme - Übersicht](/help/ingestion/streaming-ingestion/overview.md).

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hashen, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

* Entfernt alle führenden und nachfolgenden Leerzeichen aus der E-Mail-Zeichenfolge. Beispiel: `johndoe@example.com`, nicht `<space>johndoe@example.com<space>`;
* Achten Sie beim Hashing der E-Mail-Zeichenfolgen darauf, die Zeichenfolge in Kleinbuchstaben zu hashen.
   * Beispiel: `example@email.com`, nicht `EXAMPLE@EMAIL.COM`;
* Stellen Sie sicher, dass die Hash-Zeichenfolge vollständig in Kleinbuchstaben geschrieben ist
   * Beispiel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, nicht `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Die Schnur nicht salzen.

>[!NOTE]
>
>Daten aus nicht gehashten Namespaces werden von [!DNL Experience Platform] bei der Aktivierung automatisch gehasht.
>&#x200B;> Attributquelldaten werden nicht automatisch gehasht.
> 
> Wenn Ihr [ ungehashte Attribute enthält, aktivieren Sie im Schritt „Identitätszuordnung](../../ui/activate-segment-streaming-destinations.md#mapping) die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Experience Platform] die Daten bei Aktivierung automatisch hasht.
> 
> Die Option **[!UICONTROL Umwandlung anwenden]** wird nur angezeigt, wenn Sie Attribute als Quellfelder auswählen. Er wird bei der Auswahl von Namespaces nicht angezeigt.

![Umwandlung der Identitätszuordnung](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Das folgende Video zeigt auch die Schritte zum Konfigurieren eines [!DNL LinkedIn Matched Audiences] Ziels und zum Aktivieren von Zielgruppen.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Die Benutzeroberfläche von Experience Platform wird häufig aktualisiert und kann sich seit der Aufzeichnung dieses Videos geändert haben. Die neuesten Informationen finden Sie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Beim Ziel authentifizieren {#authenticate}

1. Suchen Sie das [!DNL LinkedIn Matched Audiences] im Zielkatalog und wählen Sie **[!UICONTROL Einrichten]**.
2. Wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.
   ![Authentifizierung bei LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Geben Sie Ihre LinkedIn-Anmeldedaten ein und wählen Sie **Anmelden** aus.

### Authentifizierungsdaten aktualisieren {#refresh-authentication-credentials}

LinkedIn-Token laufen alle 60 Tage ab. Sie können das Ablaufdatum Ihres Tokens über die Spalte **[!UICONTROL Account-Ablaufdatum]** entweder auf den Registerkarten **[[!UICONTROL Konten]](../../ui/destinations-workspace.md#accounts)** oder **[[!UICONTROL Durchsuchen]](../../ui/destinations-workspace.md#browse)** überwachen.

Sobald das Token abgelaufen ist, funktionieren Datenexporte an das Ziel nicht mehr. Um dies zu verhindern, authentifizieren Sie sich erneut, indem Sie die folgenden Schritte ausführen:

1. Navigieren Sie **[!UICONTROL Ziele]** > **[!UICONTROL Konten]**
2. (Optional) Verwenden Sie die verfügbaren Filter auf der Seite, um nur LinkedIn-Konten anzuzeigen.
   ![Filtern, um nur LinkedIn-Konten anzuzeigen](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-filters.png)
3. Wählen Sie das Konto aus, das Sie aktualisieren möchten, klicken Sie auf das Auslassungszeichen und wählen Sie **[!UICONTROL Details bearbeiten]**.
   ![Wählen Sie das Steuerelement „Details bearbeiten“](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-edit-details.png)
4. Wählen Sie im modalen Fenster die Option **[!UICONTROL OAuth erneut verbinden]** und authentifizieren Sie sich erneut mit Ihren LinkedIn-Anmeldeinformationen.
   ![Modales Fenster mit Option „OAuth erneut verbinden“](/help/destinations/assets/catalog/social/linkedin/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>Ihre Authentifizierungsdaten werden aktualisiert und ihre Gültigkeitsdauer wird auf 60 Tage zurückgesetzt.

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="Konto-ID"
>abstract="Ihre LinkedIn-Kampagnenmanager-Konto-ID. Diese ID finden Sie in Ihrem LinkedIn-Kampagnenmanager-Konto."

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre [!DNL LinkedIn Campaign Manager Account ID]. Diese ID finden Sie in Ihrem [!DNL LinkedIn Campaign Manager].

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Exportierte Daten {#exported-data}

Eine erfolgreiche Aktivierung bedeutet, dass eine [!DNL LinkedIn] benutzerdefinierte Zielgruppe programmgesteuert in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login) erstellt wird. Die Zielgruppenzugehörigkeit wird angepasst, da Benutzende für die aktivierten Zielgruppen qualifiziert oder disqualifiziert werden.

>[!TIP]
>
>Die Integration zwischen Adobe Experience Platform und [!DNL LinkedIn Matched Audiences] unterstützt Aufstockungen historischer Zielgruppen. Alle historischen Zielgruppenqualifikationen werden an [!DNL LinkedIn] gesendet, wenn Sie die Zielgruppen für das Ziel aktivieren.
