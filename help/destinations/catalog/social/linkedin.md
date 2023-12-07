---
keywords: LinkedIn-Verbindung; LinkedIn-Verbindung; LinkedIn-Ziele; LinkedIn;
title: Verbindung von LinkedIn mit übereinstimmenden Zielgruppen
description: Aktivieren Sie Profile für Ihre LinkedIn-Kampagnen für Zielgruppen-Targeting, Personalisierung und Unterdrückung basierend auf Hash-E-Mails.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 40%

---

# [!DNL LinkedIn Matched Audiences]-Verbindung

## Übersicht {#overview}

Profile für Ihre [!DNL LinkedIn] Kampagnen für Zielgruppen-Targeting, Personalisierung und Unterdrückung basierend auf Hash-E-Mails und mobilen IDs.

![LinkedIn-Ziel in der Adobe Experience Platform-Benutzeroberfläche](../../assets/catalog/social/linkedin/catalog.png)

## Anwendungsfälle

So können Sie besser verstehen, wie und wann die Variable [!DNL LinkedIn Matched Audiences] Ziel, hier ein Anwendungsfall, den Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

Ein Softwareunternehmen organisiert eine Konferenz und möchte mit den Teilnehmern in Kontakt bleiben und ihnen personalisierte Angebote basierend auf ihrem Konferenzstatus zeigen. Das Unternehmen kann E-Mail-Adressen oder Mobilgeräte-IDs von eigenen erfassen [!DNL CRM] nach Adobe Experience Platform. Anschließend können sie Zielgruppen aus ihren eigenen Offline-Daten erstellen und diese Zielgruppen an die [!DNL LinkedIn] Social-Plattform zur Optimierung ihrer Werbeausgaben.

## Unterstützte Identitäten {#supported-identities}

[!DNL LinkedIn Matched Audiences] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google Advertising ID | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [Anforderungen an die ID-Übereinstimmung](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mails. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer und andere), die im [!DNL LinkedIn Matched Audiences] Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen für linkedIn-Konten {#LinkedIn-account-prerequisites}

Bevor Sie die [!UICONTROL LinkedIn Match Audience] Ziel, stellen Sie sicher, dass Ihre [!DNL LinkedIn Campaign Manager] -Konto hat die [!DNL Creative Manager] Berechtigungsebene oder höher.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager] Benutzerberechtigungen, siehe [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Werbekonten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.

## Anforderungen an die ID-Übereinstimmung {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] erfordert, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher werden die Zielgruppen für [!DNL LinkedIn Matched Audiences] kann deaktiviert werden *Hash* Kennungen, wie E-Mail-Adressen oder Mobilgeräte-IDs.

Abhängig vom Typ der IDs, die Sie in Adobe Experience Platform erfassen, müssen Sie die entsprechenden Anforderungen erfüllen.

## Anforderungen an das E-Mail-Hashing {#email-hashing-requirements}

Sie können E-Mail-Adressen vor der Aufnahme in Adobe Experience Platform hash-Adressen oder eindeutige E-Mail-Adressen in Experience Platform verwenden und [!DNL Platform] Hash sie bei Aktivierung.

Informationen zur Aufnahme von E-Mail-Adressen in Experience Platform finden Sie in der [Batch-Erfassung - Übersicht](/help/ingestion/batch-ingestion/overview.md) und [Streaming-Erfassung - Übersicht](/help/ingestion/streaming-ingestion/overview.md).

Wenn Sie die E-Mail-Adressen selbst hash möchten, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

* Schneiden Sie alle führenden und nachfolgenden Leerzeichen aus der E-Mail-Zeichenfolge. Beispiel: `johndoe@example.com`, nicht `<space>johndoe@example.com<space>`;
* Achten Sie beim Hashing der E-Mail-Zeichenfolgen darauf, die Zeichenfolge in Kleinbuchstaben zu hash;
   * Beispiel: `example@email.com`, nicht `EXAMPLE@EMAIL.COM`;
* Stellen Sie sicher, dass der Hash-String nur in Kleinbuchstaben geschrieben wird.
   * Beispiel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, nicht `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Salz die Zeichenfolge nicht.

>[!NOTE]
>
>Daten aus nicht gehashten Namespaces werden automatisch von [!DNL Platform] bei Aktivierung.
> Attributquellendaten werden nicht automatisch gehasht.
> 
> Während [Identitätszuordnung](../../ui/activate-segment-streaming-destinations.md#mapping) Schritt: Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, um [!DNL Platform] die Daten bei Aktivierung automatisch hash.
> 
> Die **[!UICONTROL Umwandlung anwenden]** wird nur angezeigt, wenn Sie Attribute als Quellfelder auswählen. Es wird nicht angezeigt, wenn Sie Namespaces auswählen.

![Identity Mapping Transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Das folgende Video zeigt auch die Schritte zum Konfigurieren eines [!DNL LinkedIn Matched Audiences] Zielgruppen bestimmen und aktivieren.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Die Benutzeroberfläche von Experience Platform wird häufig aktualisiert und kann sich seit der Aufzeichnung dieses Videos geändert haben. Die aktuellsten Informationen finden Sie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Beim Ziel authentifizieren {#authenticate}

1. Suchen Sie die [!DNL LinkedIn Matched Audiences] Ziel im Zielkatalog auswählen **[!UICONTROL Einrichten]**.
2. Auswählen **[!UICONTROL Mit Ziel verbinden]**.
   ![Bei LinkedIn authentifizieren](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Geben Sie Ihre LinkedIn-Anmeldedaten ein und wählen Sie **Anmelden**.

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="Konto-ID"
>abstract="Ihre LinkedIn-Kampagnenmanager-Konto-ID. Diese ID finden Sie in Ihrem LinkedIn-Kampagnenmanager-Konto."

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihr [!DNL LinkedIn Campaign Manager Account ID]. Diese ID finden Sie in Ihrer [!DNL LinkedIn Campaign Manager] -Konto.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Exportierte Daten {#exported-data}

Eine erfolgreiche Aktivierung bedeutet, dass eine [!DNL LinkedIn] eine benutzerdefinierte Zielgruppe wird programmgesteuert in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). Die Zielgruppenmitgliedschaft wird hinzugefügt und entfernt, da Benutzer für die aktivierten Zielgruppen qualifiziert oder disqualifiziert sind.

>[!TIP]
>
>Die Integration zwischen Adobe Experience Platform und [!DNL LinkedIn Matched Audiences] unterstützt historische Zielgruppen-Backups. Alle historischen Zielgruppenqualifikationen werden an gesendet. [!DNL LinkedIn] wenn Sie die Zielgruppen für das Ziel aktivieren.
