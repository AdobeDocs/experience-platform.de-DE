---
keywords: LinkedIn-Verbindung; LinkedIn-Verbindung; LinkedIn-Ziele; LinkedIn;
title: Verbindung von LinkedIn mit übereinstimmenden Zielgruppen
description: Aktivieren Sie Profile für Ihre LinkedIn-Kampagnen für Zielgruppen-Targeting, Personalisierung und Unterdrückung basierend auf Hash-E-Mails.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 74d7c48042b0d2b938705b588c185f3c3f96f1cd
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 37%

---

# [!DNL LinkedIn Matched Audiences]-Verbindung

## Übersicht {#overview}

Aktivieren Sie Profile für Ihre [!DNL LinkedIn]-Kampagnen für Zielgruppen-Targeting, Personalisierung und Unterdrückung basierend auf Hash-E-Mails und mobilen IDs.

![LinkedIn-Ziel in der Adobe Experience Platform-Benutzeroberfläche](../../assets/catalog/social/linkedin/catalog.png)

## Anwendungsfälle

Um Ihnen zu helfen, besser zu verstehen, wie und wann das [!DNL LinkedIn Matched Audiences]-Ziel verwendet werden soll, finden Sie hier einen Anwendungsfall, den Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

Ein Softwareunternehmen organisiert eine Konferenz und möchte mit den Teilnehmern in Kontakt bleiben und ihnen personalisierte Angebote basierend auf ihrem Konferenzstatus zeigen. Das Unternehmen kann E-Mail-Adressen oder Mobilgeräte-IDs von seinem eigenen [!DNL CRM] in Adobe Experience Platform erfassen. Anschließend können sie aus ihren eigenen Offline-Daten Zielgruppen erstellen und diese Zielgruppen an die soziale Plattform [!DNL LinkedIn] senden, wodurch ihre Werbeausgaben optimiert werden.

## Unterstützte Identitäten {#supported-identities}

[!DNL LinkedIn Matched Audiences] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [ID-Abgleichanforderungen](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mails. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die durch den Experience Platform [Segmentierungsdienst](../../../segmentation/home.md) generiert wurden. |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer und andere), die im [!DNL LinkedIn Matched Audiences]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen für linkedIn-Konten {#LinkedIn-account-prerequisites}

Bevor Sie das Ziel [!UICONTROL LinkedIn Matched Audience] verwenden können, stellen Sie sicher, dass Ihr [!DNL LinkedIn Campaign Manager]-Konto über die Berechtigungsebene [!DNL Creative Manager] oder höher verfügt.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager] -Benutzerberechtigungen finden Sie unter [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Advertising-Konten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.

## Anforderungen an die ID-Übereinstimmung {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] erfordert, dass keine personenbezogenen Daten (PII) klar gesendet werden. Daher können die für [!DNL LinkedIn Matched Audiences] aktivierten Zielgruppen aus *Hash*-Identifikatoren wie E-Mail-Adressen oder Mobilgeräte-IDs abgeleitet werden.

Abhängig vom Typ der IDs, die Sie in Adobe Experience Platform erfassen, müssen Sie die entsprechenden Anforderungen erfüllen.

## Anforderungen an das E-Mail-Hashing {#email-hashing-requirements}

Sie können E-Mail-Adressen vor der Aufnahme in Adobe Experience Platform hash-Adressen oder eindeutige E-Mail-Adressen in Experience Platform verwenden und diese bei der Aktivierung mit [!DNL Platform] hash lassen.

Weiterführende Informationen zur Aufnahme von E-Mail-Adressen in Experience Platform finden Sie in der [Batch-Erfassungsübersicht](/help/ingestion/batch-ingestion/overview.md) und der [Streaming-Erfassungsübersicht](/help/ingestion/streaming-ingestion/overview.md).

Wenn Sie die E-Mail-Adressen selbst hash möchten, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

* Schneiden Sie alle führenden und nachfolgenden Leerzeichen aus der E-Mail-Zeichenfolge. Beispiel: `johndoe@example.com`, nicht `<space>johndoe@example.com<space>`;
* Achten Sie beim Hashing der E-Mail-Zeichenfolgen darauf, die Zeichenfolge in Kleinbuchstaben zu hash;
   * Beispiel: `example@email.com`, nicht `EXAMPLE@EMAIL.COM`;
* Stellen Sie sicher, dass der Hash-String nur in Kleinbuchstaben geschrieben wird.
   * Beispiel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, nicht `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Salz die Zeichenfolge nicht.

>[!NOTE]
>
>Daten aus nicht gehashten Namespaces werden bei Aktivierung automatisch von [!DNL Platform] gehasht.
> Attributquellendaten werden nicht automatisch gehasht.
> 
> Wenn Ihr Quellfeld ungehashte Attribute enthält, aktivieren Sie während des Schritts [Identitätszuordnung](../../ui/activate-segment-streaming-destinations.md#mapping) die Option **[!UICONTROL Transformation anwenden]** , damit [!DNL Platform] die Daten bei Aktivierung automatisch hasst.
> 
> Die Option **[!UICONTROL Transformation anwenden]** wird nur angezeigt, wenn Sie Attribute als Quellfelder auswählen. Es wird nicht angezeigt, wenn Sie Namespaces auswählen.

![Transformation der Identitätszuordnung](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Das folgende Video zeigt auch die Schritte zum Konfigurieren eines [!DNL LinkedIn Matched Audiences] -Ziels und zum Aktivieren von Zielgruppen.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Die Benutzeroberfläche von Experience Platform wird häufig aktualisiert und kann sich seit der Aufzeichnung dieses Videos geändert haben. Die aktuellsten Informationen finden Sie im Tutorial zur Zielkonfiguration [.](../../ui/connect-destination.md)

### Beim Ziel authentifizieren {#authenticate}

1. Suchen Sie das Ziel &quot;[!DNL LinkedIn Matched Audiences]&quot;im Zielkatalog und wählen Sie &quot;**[!UICONTROL Einrichten]**&quot;.
2. Wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.
   ![Bei LinkedIn authentifizieren](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Geben Sie Ihre LinkedIn-Anmeldedaten ein und wählen Sie **Anmelden** aus.

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="Konto-ID"
>abstract="Ihre LinkedIn-Kampagnenmanager-Konto-ID. Diese ID finden Sie in Ihrem LinkedIn-Kampagnenmanager-Konto."

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre [!DNL LinkedIn Campaign Manager Account ID]. Sie finden diese ID in Ihrem [!DNL LinkedIn Campaign Manager] -Konto.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Exportierte Daten {#exported-data}

Eine erfolgreiche Aktivierung bedeutet, dass eine benutzerdefinierte Zielgruppe vom Typ [!DNL LinkedIn] programmgesteuert in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login) erstellt wird. Die Zielgruppenmitgliedschaft wird angepasst, wenn Benutzer für die aktivierten Zielgruppen qualifiziert oder disqualifiziert sind.

>[!TIP]
>
>Die Integration zwischen Adobe Experience Platform und [!DNL LinkedIn Matched Audiences] unterstützt historische Zielgruppen-Backups. Alle historischen Zielgruppenqualifikationen werden an [!DNL LinkedIn] gesendet, wenn Sie die Zielgruppen für das Ziel aktivieren.
