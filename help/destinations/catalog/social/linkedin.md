---
keywords: LinkedIn-Verbindung; LinkedIn-Verbindung; LinkedIn-Ziele; LinkedIn;
title: Verbindung von LinkedIn mit übereinstimmenden Zielgruppen
description: Aktivieren Sie Profile für Ihre LinkedIn-Kampagnen für Zielgruppen-Targeting, Personalisierung und Unterdrückung basierend auf Hash-E-Mails.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 10%

---

# [!DNL LinkedIn Matched Audiences]-Verbindung

## Übersicht {#overview}

Profile für Ihre [!DNL LinkedIn] Kampagnen für Zielgruppen-Targeting, Personalisierung und Unterdrückung basierend auf Hash-E-Mails und mobilen IDs.

![linkedIn-Ziel in der Adobe Experience Platform-Benutzeroberfläche](../../assets/catalog/social/linkedin/catalog.png)

## Anwendungsfälle

So können Sie besser verstehen, wie und wann die Variable [!DNL LinkedIn Matched Audiences] Ziel, hier ein Anwendungsfall, den Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

Ein Softwareunternehmen organisiert eine Konferenz und möchte mit den Teilnehmern in Kontakt bleiben und ihnen personalisierte Angebote basierend auf ihrem Konferenzstatus zeigen. Das Unternehmen kann E-Mail-Adressen oder Mobilgeräte-IDs von eigenen erfassen [!DNL CRM] nach Adobe Experience Platform. Anschließend können sie Segmente aus ihren eigenen Offline-Daten erstellen und diese Segmente an die [!DNL LinkedIn] Social-Plattform zur Optimierung ihrer Werbeausgaben.

## Unterstützte Identitäten {#supported-identities}

[!DNL LinkedIn Matched Audiences] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Weitere Informationen [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google Advertising ID | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [Anforderungen an die ID-Übereinstimmung](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mails. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, um [!DNL Platform] die Daten bei Aktivierung automatisch hash. |

{style=&quot;table-layout:auto&quot;}

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer und andere), die im [!DNL LinkedIn Matched Audiences] Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Voraussetzungen für linkedIn-Konten {#LinkedIn-account-prerequisites}

Bevor Sie die [!UICONTROL linkedIn Match Audience] Ziel, stellen Sie sicher, dass Ihre [!DNL LinkedIn Campaign Manager] -Konto hat [!DNL Creative Manager] Berechtigungsebene oder höher.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager] Benutzerberechtigungen, siehe [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Werbekonten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.

## Anforderungen an die ID-Übereinstimmung {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] erfordert, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher werden die Zielgruppen für [!DNL LinkedIn Matched Audiences] kann deaktiviert werden *Hash* Kennungen, wie E-Mail-Adressen oder Mobilgeräte-IDs.

Abhängig vom Typ der IDs, die Sie in Adobe Experience Platform erfassen, müssen Sie die entsprechenden Anforderungen erfüllen.

## Anforderungen an das E-Mail-Hashing {#email-hashing-requirements}

Sie können E-Mail-Adressen hash, bevor Sie sie in Adobe Experience Platform aufnehmen, oder eindeutige E-Mail-Adressen in Experience Platform verwenden und [!DNL Platform] Hash sie bei Aktivierung.

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

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

Das folgende Video zeigt auch die Schritte zum Konfigurieren eines [!DNL LinkedIn Matched Audiences] Zielgruppen und Aktivieren von Segmenten.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Die Benutzeroberfläche von Experience Platform wird häufig aktualisiert und kann sich seit der Aufzeichnung dieses Videos geändert haben. Die aktuellsten Informationen finden Sie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: einen Namen, mit dem Sie dieses Ziel in Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre [!DNL LinkedIn Campaign Manager Account ID]. Diese ID finden Sie in Ihrer [!DNL LinkedIn Campaign Manager] -Konto.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Exportierte Daten {#exported-data}

Eine erfolgreiche Aktivierung bedeutet, dass eine [!DNL LinkedIn] eine benutzerdefinierte Zielgruppe wird programmgesteuert in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). Segmentmitgliedschaft in der Zielgruppe wird hinzugefügt und entfernt, wenn Anwender für die aktivierten Segmente qualifiziert oder disqualifiziert werden.

>[!TIP]
>
>Die Integration zwischen Adobe Experience Platform und [!DNL LinkedIn Matched Audiences] unterstützt historische Zielgruppen-Backups. Alle historischen Segmentqualifikationen werden an gesendet. [!DNL LinkedIn] wenn Sie die Segmente für das Ziel aktivieren.
