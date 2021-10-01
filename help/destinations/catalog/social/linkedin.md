---
keywords: LinkedIn-Verbindung; LinkedIn-Verbindung; LinkedIn-Ziele; LinkedIn;
title: Verbindung von LinkedIn mit übereinstimmenden Zielgruppen
description: Aktivieren Sie Profile für Ihre LinkedIn-Kampagnen für Zielgruppen-Targeting, Personalisierung und Unterdrückung basierend auf Hash-E-Mails.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 3%

---

# [!DNL LinkedIn Matched Audiences] connection

## Übersicht {#overview}

Aktivieren Sie Profile für Ihre [!DNL LinkedIn]-Kampagnen für Zielgruppen-Targeting, Personalisierung und Unterdrückung, basierend auf Hash-E-Mails und mobilen IDs.

![linkedIn-Ziel in der Adobe Experience Platform-Benutzeroberfläche](../../assets/catalog/social/linkedin/catalog.png)

## Anwendungsfälle

Um Ihnen zu helfen, besser zu verstehen, wie und wann das [!DNL LinkedIn Matched Audiences]-Ziel verwendet werden soll, finden Sie hier einen Anwendungsfall, den Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

Ein Softwareunternehmen organisiert eine Konferenz und möchte mit den Teilnehmern in Kontakt bleiben und ihnen personalisierte Angebote basierend auf ihrem Konferenzstatus zeigen. Das Unternehmen kann E-Mail-Adressen oder Mobilgeräte-IDs von seinem eigenen [!DNL CRM] in Adobe Experience Platform erfassen. Anschließend können sie Segmente aus ihren eigenen Offline-Daten erstellen und diese Segmente an die soziale Plattform [!DNL LinkedIn] senden, wodurch ihre Werbeausgaben optimiert werden.

## Unterstützte Identitäten {#supported-identities}

[!DNL LinkedIn Matched Audiences] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Erfahren Sie mehr über [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google Advertising ID | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [Anforderungen an die ID-Zuordnung](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namespaces für Nur-Text- und Hash-E-Mails. Wenn Ihr Quellfeld ungehashte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash. |


## Exporttyp {#export-type}

**Segmentexport** : Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer und andere), die im  [!DNL LinkedIn Matched Audiences] Ziel verwendet werden.

## Voraussetzungen für linkedIn-Konten {#LinkedIn-account-prerequisites}

Bevor Sie das Ziel [!UICONTROL LinkedIn Matched Audience] verwenden können, stellen Sie sicher, dass Ihr [!DNL LinkedIn Campaign Manager]-Konto über die Berechtigungsebene [!DNL Creative Manager] oder höher verfügt.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager]-Benutzerberechtigungen finden Sie unter [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Werbekonten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.

## Anforderungen an die ID-Übereinstimmung {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] erfordert, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher können die für [!DNL LinkedIn Matched Audiences] aktivierten Zielgruppen von *Hash*-Identifikatoren wie E-Mail-Adressen oder Mobilgeräte-IDs abgeleitet werden.

Abhängig vom Typ der IDs, die Sie in Adobe Experience Platform erfassen, müssen Sie die entsprechenden Anforderungen erfüllen.

## Anforderungen an das E-Mail-Hashing {#email-hashing-requirements}

Sie können E-Mail-Adressen vor der Aufnahme in Adobe Experience Platform hash-Adressen oder in der Experience Platform eindeutige E-Mail-Adressen verwenden und [!DNL Platform] bei Aktivierung hash-Adressen einrichten.

Weitere Informationen zur Aufnahme von E-Mail-Adressen in Experience Platform finden Sie unter [Batch-Erfassung - Übersicht](/help/ingestion/batch-ingestion/overview.md) und [Streaming-Erfassung - Übersicht](/help/ingestion/streaming-ingestion/overview.md).

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
> Aktivieren Sie während des Schritts [Identitätszuordnung](../../ui/activate-segment-streaming-destinations.md#mapping) die Option **[!UICONTROL Umwandlung anwenden]**, wenn Ihr Quellfeld ungehashte Attribute enthält, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasst.
> 
> Die Option **[!UICONTROL Umwandlung anwenden]** wird nur angezeigt, wenn Sie Attribute als Quellfelder auswählen. Es wird nicht angezeigt, wenn Sie Namespaces auswählen.

![Identity Mapping Transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

Das folgende Video zeigt auch die Schritte zum Konfigurieren eines [!DNL LinkedIn Matched Audiences]-Ziels und zum Aktivieren von Segmenten.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Die Benutzeroberfläche der Experience Platform wird häufig aktualisiert und kann sich seit der Aufzeichnung dieses Videos geändert haben. Die aktuellsten Informationen finden Sie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: einen Namen, mit dem Sie dieses Ziel in Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihr  [!DNL LinkedIn Campaign Manager Account ID]. Sie finden diese ID in Ihrem [!DNL LinkedIn Campaign Manager] -Konto.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) .

## Exportierte Daten {#exported-data}

Eine erfolgreiche Aktivierung bedeutet, dass eine [!DNL LinkedIn] benutzerdefinierte Zielgruppe programmgesteuert in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login) erstellt wird. Segmentmitgliedschaft in der Zielgruppe wird hinzugefügt und entfernt, wenn Anwender für die aktivierten Segmente qualifiziert oder disqualifiziert werden.

>[!TIP]
>
>Die Integration zwischen Adobe Experience Platform und [!DNL LinkedIn Matched Audiences] unterstützt historische Zielgruppen-Backups. Alle historischen Segmentqualifikationen werden an [!DNL LinkedIn] gesendet, wenn Sie die Segmente für das Ziel aktivieren.
