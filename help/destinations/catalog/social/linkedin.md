---
keywords: linkedin-Verbindung;LinkedIn-Verbindung;LinkedIn-Ziele;linkedin
title: Verbindung zu LinkedIn-Audiencen
description: Aktivieren Sie Profil für Ihre LinkedIn-Kampagnen für Targeting, Personalisierung und Unterdrückung von Audiencen, basierend auf Hash-E-Mails.
translation-type: tm+mt
source-git-commit: 48cc2017e4a65321fb7ef54ea26aca0a98606516
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 4%

---


# [!DNL LinkedIn Matched Audiences] connection

Aktivieren Sie Profil für Ihre [!DNL LinkedIn]-Kampagnen für Targeting, Personalisierung und Unterdrückung von Audiencen, basierend auf Hash-E-Mails und mobilen IDs.

![LinkedIn-Ziel in der Adobe Experience Platform-Benutzeroberfläche](../../assets/catalog/social/linkedin/catalog.png)

## Nutzungsszenarien

Damit Sie besser verstehen können, wie und wann Sie das [!DNL LinkedIn Matched Audience]-Ziel verwenden sollten, hier ein Anwendungsfall, den Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

Eine Software-Firma organisiert eine Konferenz und möchte mit den Teilnehmern in Kontakt bleiben und ihnen personalisierte Angebote je nach deren Status als Konferenzteilnehmer zeigen. Die Firma kann E-Mail-Adressen oder Mobilgerät-IDs von ihrem eigenen [!DNL CRM] in Adobe Experience Platform erfassen, Segmente aus ihren eigenen Offlinedaten erstellen und diese Segmente an die [!DNL LinkedIn] Social-Plattform senden, um ihre Werbeausgaben zu optimieren.

## Zielspezifikationen {#destination-specs}

[!DNL LinkedIn Matched Audience] unterstützt die Aktivierung der folgenden Identitäten: E-Mails mit Hashing  [!DNL GAID]und  [!DNL IDFA].

### Exporttyp {#export-type}

**Segmentexport** : Sie exportieren alle Segmentmitglieder (Audience) mit den Bezeichnern (Name, Telefonnummer usw.) wird im [!DNL LinkedIn Matched Audience]-Ziel verwendet.

### Voraussetzungen für LinkedIn-Konto {#LinkedIn-account-prerequisites}

Bevor Sie das Ziel [!UICONTROL LinkedIn Matched Audience] verwenden können, stellen Sie sicher, dass Ihr [!DNL LinkedIn Campaign Manager]-Konto die Berechtigungsstufe [!DNL Creative Manager] oder höher aufweist.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager]-Benutzerberechtigungen finden Sie unter [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Werbekonten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.

### Anforderungen für die ID-Übereinstimmung {#id-matching-requirements}

[!DNL LinkedIn Matched Audience] verlangt, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher können die für [!DNL LinkedIn Matched Audience] aktivierten Audiencen anhand von *Hash*-IDs wie E-Mail-Adressen oder Mobilgerät-IDs ausgewertet werden.

Abhängig von der Art der IDs, die Sie in Adobe Experience Platform eingeben, müssen Sie die entsprechenden Anforderungen erfüllen.

#### Anforderungen für das E-Mail-Hashing {#email-hashing-requirements}

Sie können E-Mail-Adressen vor der Einbindung in Adobe Experience Platform als Hash-E-Mail-Adressen festlegen oder Sie können in Experience Platform mit E-Mail-Adressen arbeiten und sie von unserem Algorithmus auf Aktivierung hash lassen.

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

Informationen zum Herstellen einer Verbindung mit dem Ziel [!DNL LinkedIn Matched Audience] finden Sie unter [Authentifizierungsarbeitsablauf für Social-Netzwerkziele](./workflow.md).

## Aktivieren von Segmenten nach [!DNL LinkedIn Matched Audience] {#activate-segments}

Anweisungen zum Aktivieren von Segmenten in [!DNL LinkedIn Matched Audience] finden Sie unter [Daten in Ziele aktivieren](../../ui/activate-destinations.md).

## Exportierte Daten {#exported-data}

Eine erfolgreiche Aktivierung bedeutet, dass eine [!DNL LinkedIn] benutzerdefinierte Audience programmgesteuert in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login) erstellt wird. Segmentmitgliedschaft in der Zielgruppe wird hinzugefügt und entfernt, wenn Anwender für die aktivierten Segmente qualifiziert oder disqualifiziert werden.

>[!TIP]
>
>Die Integration zwischen Adobe Experience Platform und [!DNL LinkedIn Matched Audience] unterstützt Backfills für historische Audiencen. Alle historischen Segmentqualifikationen werden an [!DNL LinkedIn] gesendet, wenn Sie die Segmente an das Ziel aktivieren.