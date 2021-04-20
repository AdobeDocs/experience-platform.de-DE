---
keywords: linkedin-Verbindung;LinkedIn-Verbindung;LinkedIn-Ziele;linkedin
title: Verbindung zu LinkedIn-Audiencen
description: Aktivieren Sie Profil für Ihre LinkedIn-Kampagnen für Targeting, Personalisierung und Unterdrückung von Audiencen, basierend auf Hash-E-Mails.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
translation-type: tm+mt
source-git-commit: 805cb72e91e6446f74cc3461d39841740eb576c7
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 4%

---

# [!DNL LinkedIn Matched Audiences] connection

## Übersicht {#overview}

Aktivieren Sie Profil für Ihre [!DNL LinkedIn]-Kampagnen für Targeting, Personalisierung und Unterdrückung von Audiencen, basierend auf Hash-E-Mails und mobilen IDs.

![linkedIn-Ziel in der Adobe Experience Platform-Benutzeroberfläche](../../assets/catalog/social/linkedin/catalog.png)

## Anwendungsbeispiele

Damit Sie besser verstehen können, wie und wann das [!DNL LinkedIn Matched Audiences]-Ziel verwendet werden soll, hier ein Anwendungsfall, den Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

Eine Software-Firma organisiert eine Konferenz und möchte mit den Teilnehmern in Kontakt bleiben und ihnen personalisierte Angebote je nach deren Status als Konferenzteilnehmer zeigen. Die Firma kann E-Mail-Adressen oder Mobilgeräte-IDs von ihrem eigenen [!DNL CRM] in Adobe Experience Platform erfassen. Anschließend können sie Segmente aus ihren eigenen Offlinedaten erstellen und diese Segmente an die soziale Plattform [!DNL LinkedIn] senden, um ihre Werbeausgaben zu optimieren.

## Unterstützte Identitäten {#supported-identities}

[!DNL LinkedIn Matched Audiences] unterstützt die Aktivierung der Identitäten, die in der folgenden Tabelle beschrieben sind. Erfahren Sie mehr über [identities](/help/identity-service/namespaces.md).

| Zielgruppe | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google Advertising ID | Wählen Sie diese Zielgruppen-ID aus, wenn Ihre Quellidentität ein GAID-Namensraum ist. |
| IDFA | Apple-ID für Werbetreibende | Wählen Sie diese Zielgruppen-ID aus, wenn Ihre Quellidentität ein IDFA-Namensraum ist. |
| email_lc_sha256 | Mit dem SHA256-Algorithmus verfasste E-Mail-Adressen | Sowohl einfache als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [Anforderungen für die ID-Zuordnung](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namensraum für reine und Hash-E-Mails. Wenn Ihr Quellfeld ungehackte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Transformation]** anwenden, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash. |


## Exporttyp {#export-type}

**Segmentexport** : Sie exportieren alle Segmentmitglieder (Audience) mit den IDs (Name, Telefonnummer usw.), die im  [!DNL LinkedIn Matched Audiences] Ziel verwendet werden.

## Voraussetzungen für linkedIn-Konten {#LinkedIn-account-prerequisites}

Bevor Sie das [!UICONTROL LinkedIn Matched Audience]-Ziel verwenden können, stellen Sie sicher, dass Ihr [!DNL LinkedIn Campaign Manager]-Konto das Berechtigungsniveau [!DNL Creative Manager] oder höher aufweist.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager]-Benutzerberechtigungen finden Sie unter [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Werbekonten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.

## Anforderungen für die ID-Übereinstimmung {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] verlangt, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher können die für [!DNL LinkedIn Matched Audiences] aktivierten Audiencen anhand von *Hash*-IDs wie E-Mail-Adressen oder Mobilgerät-IDs ausgewertet werden.

Abhängig von der Art der IDs, die Sie in Adobe Experience Platform eingeben, müssen Sie die entsprechenden Anforderungen erfüllen.

## Anforderungen für das E-Mail-Hashing {#email-hashing-requirements}

Sie können E-Mail-Adressen vor dem Eingeben in Adobe Experience Platform hash oder in der Experience Platform eindeutige E-Mail-Adressen verwenden und sie bei der Aktivierung mit [!DNL Platform] Hash versehen.

Weitere Informationen zum Eingeben von E-Mail-Adressen in Experience Platformen finden Sie unter [Überblick über die Stapelverarbeitung](/help/ingestion/batch-ingestion/overview.md) und [Übersicht über die Streaming-Erfassung](/help/ingestion/streaming-ingestion/overview.md).

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hash, stellen Sie sicher, dass folgende Anforderungen erfüllt sind:

- Beschneiden Sie alle führenden und nachfolgenden Leerzeichen aus der E-Mail-Zeichenfolge. Beispiel: `johndoe@example.com`, nicht `<space>johndoe@example.com<space>`;
- Achten Sie beim Hashing der E-Mail-Zeichenfolgen darauf, die Zeichenfolge in Kleinbuchstaben mit Hash zu versehen.
   - Beispiel: `example@email.com`, nicht `EXAMPLE@EMAIL.COM`;
- Stellen Sie sicher, dass die Hash-Zeichenfolge nur in Kleinbuchstaben angegeben wird
   - Beispiel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, nicht `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Salt die Zeichenfolge nicht.

>[!NOTE]
>
>Daten von Namensräumen ohne Hash werden bei Aktivierung automatisch durch [!DNL Platform] gehasht.
> Attributquellendaten werden nicht automatisch mit Hashing versehen.
> 
> Aktivieren Sie im Schritt [Identitätszuordnung](../../ui/activate-destinations.md#identity-mapping), wenn Ihr Quellfeld ungehackte Attribute enthält, die Option **[!UICONTROL Transformation]** anwenden, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash.
> 
> Die Option **[!UICONTROL Transformation anwenden]** wird nur angezeigt, wenn Sie Attribute als Quellfelder auswählen. Es wird nicht angezeigt, wenn Sie Namensraum auswählen.

![Identitätszuordnungs-Transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Mit Ziel verbinden {#connect-destination}

Informationen zum Herstellen einer Verbindung mit dem Ziel [!DNL LinkedIn Matched Audiences] finden Sie unter [Arbeitsablauf für die Authentifizierung von Social-Zielen](./workflow.md).

Das folgende Video zeigt auch die Schritte zum Konfigurieren eines [!DNL LinkedIn Matched Audiences]-Ziels und zum Aktivieren von Segmenten.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Aktivieren von Segmenten nach [!DNL LinkedIn Matched Audiences] {#activate-segments}

Anweisungen zum Aktivieren von Segmenten in [!DNL LinkedIn Matched Audiences] finden Sie unter [Daten in Ziele aktivieren](../../ui/activate-destinations.md).

## Exportierte Daten {#exported-data}

Eine erfolgreiche Aktivierung bedeutet, dass eine [!DNL LinkedIn] benutzerdefinierte Audience programmgesteuert in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login) erstellt wird. Segmentmitgliedschaft in der Zielgruppe wird hinzugefügt und entfernt, wenn Anwender für die aktivierten Segmente qualifiziert oder disqualifiziert werden.

>[!TIP]
>
>Die Integration zwischen Adobe Experience Platform und [!DNL LinkedIn Matched Audiences] unterstützt Backfills für historische Audiencen. Alle historischen Segmentqualifikationen werden an [!DNL LinkedIn] gesendet, wenn Sie die Segmente an das Ziel aktivieren.
