---
keywords: facebook extensions;facebook extension;facebook destinations;facebook
title: Facebook-Ziel
seo-title: Facebook-Ziel
description: Aktivieren Sie Profile für Ihre Facebook-Kampagnen zur Zielgruppenbestimmung, Personalisierung und Unterdrückung anhand von Hash-E-Mails.
seo-description: Aktivieren Sie Profile für Ihre Facebook-Kampagnen zur Zielgruppenbestimmung, Personalisierung und Unterdrückung anhand von Hash-E-Mails.
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 19%

---


# [!DNL Facebook] Ziel

## Übersicht {#overview}

Activate profiles for your [!DNL Facebook] campaigns for audience targeting, personalization and suppression based on hashed emails.

![Facebook-Ziel in der CDP-Benutzeroberfläche in Echtzeit](/help/rtcdp/destinations/assets/facebook-destination.png)

## Nutzungsszenarien

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Facebook] Ziel verwenden sollten, gibt es zwei Beispielverwendungsfälle, die Kunden der Adobe Echtzeit-Kundendatenplattform mit dieser Funktion lösen können.


### Verwendungsfall Nr. 1


Ein Online-Händler möchte bestehende Kunden über soziale Plattformen erreichen und ihnen personalisierte Angebot auf Basis ihrer bisherigen Bestellungen zeigen. Der Online-Händler kann E-Mail-Adressen von seinem eigenen CRM zur Adobe von Echtzeit-CDP erfassen, Segmente aus eigenen Offlinedaten erstellen und diese Segmente an die [!DNL Facebook] Social-Plattform senden, um ihre Werbeausgaben zu optimieren.


### Verwendungsfall Nr. 2


Eine Fluggesellschaft hat verschiedene Kundenstufen (Bronze, Silver und Gold) und möchte jede dieser Stufen mit personalisierten Angeboten über soziale Plattformen versorgen. Nicht alle Kunden verwenden jedoch die mobile App der Fluggesellschaft, und einige von ihnen haben sich noch nicht bei der Website der Firma angemeldet. Die einzigen IDs, die die Firma zu diesen Kunden hat, sind Mitgliedschafts-IDs und E-Mail-Adressen.

Um sie über soziale Netzwerke hinweg Zielgruppe, können sie die Kundendaten aus ihrem CRM-System in Adobe Echtzeit-CDP einbinden und dabei die E-Mail-Adressen als ID verwenden.

Als Nächstes können sie ihre Offline-Daten einschließlich der zugehörigen Mitgliedschafts-IDs und Kundenebenen verwenden, um neue Audiencen zu erstellen, die sie über das [!DNL Facebook] Ziel Zielgruppe haben können.

## Zielspezifikationen {#destination-specs}

### Datenverwaltung für [!DNL Facebook] Ziele {#data-governance}

>[!IMPORTANT]
>
>Daten, die an gesendet werden, [!DNL Facebook] sollten keine gehefteten Identitäten enthalten. Sie sind für die Erfüllung dieser Verpflichtung verantwortlich und können dies tun, indem Sie sicherstellen, dass Segmente, die für die Aktivierung ausgewählt wurden, keine Heftoption in ihrer Fusionsrichtlinie verwenden. Weitere Informationen zu [Zusammenführungsrichtlinien](/help/profile/ui/merge-policies.md).

### Aktivierungstyp {#activation-type}

**Segmentexport** : Sie exportieren alle Segmentmitglieder (Audience) mit den Bezeichnern (Name, Telefonnummer usw.) verwendet im Facebook-Ziel.

### Voraussetzungen für Facebook-Konten {#facebook-account-prerequisites}

Bevor Sie Zielgruppensegmente an [!DNL Facebook] senden können, müssen Sie sicherstellen, dass Sie die folgenden Voraussetzungen erfüllen:

1. Your [!DNL Facebook] user account must have the **[!DNL Manage campaigns]** permission enabled for the Ad account that you plan to use.
2. Fügen Sie das **Adobe Experience Cloud**-Geschäftskonto als Werbepartner in Ihrem [!DNL Facebook Ad Account] hinzu. Verwenden Sie `business ID=206617933627973`. Weitere Informationen finden Sie unter [Hinzufügen Partner zu Ihrem Business Manager](https://www.facebook.com/business/help/1717412048538897) in der Facebook-Dokumentation.
   >[!IMPORTANT]
   >
   > Beim Konfigurieren der Berechtigungen für Adobe Experience Cloud müssen Sie die Berechtigung **Kampagnen verwalten** aktivieren. Dies ist für die [!DNL Adobe Real-time CDP]-Integration erforderlich.
3. Lesen und unterschreiben Sie die [!DNL Facebook Custom Audiences]-Nutzungsbedingungen. Rufen Sie dazu `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]` auf, wobei `accountID` Ihre [!DNL Facebook Ad Account ID] ist.

### Anforderungen für das E-Mail-Hashing {#email-hashing-requirements}

[!DNL Facebook] verlangt, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher [!DNL Facebook] müssen die aktivierten Audiencen von *Hash* -E-Mail-Adressen abgekoppelt werden. Sie können E-Mail-Adressen vor der Einbindung in Adobe Experience Platform als Hash-E-Mail-Adressen festlegen oder Sie können in Experience Platform mit E-Mail-Adressen arbeiten und sie von unserem Algorithmus auf Aktivierung hash lassen.

Weitere Informationen zum Eingeben von E-Mail-Adressen in der Experience Platform finden Sie in der Übersicht über die [Stapelverarbeitung](/help/ingestion/batch-ingestion/overview.md) und in der Übersicht über die [Erfassung](/help/ingestion/streaming-ingestion/overview.md)des Streamings.

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hash, stellen Sie sicher, dass folgende Anforderungen erfüllt sind:

* Entfernen Sie alle führenden und nachfolgenden Leerzeichen aus der E-Mail-Zeichenfolge. example: `johndoe@example.com`, nicht `<space>johndoe@example.com<space>`;
* Achten Sie beim Hashing der E-Mail-Zeichenfolgen darauf, die Zeichenfolge in Kleinbuchstaben mit Hash zu versehen.
   * Beispiel: `example@email.com`, nicht `EXAMPLE@EMAIL.COM`;
* Stellen Sie sicher, dass die Hash-Zeichenfolge nur in Kleinbuchstaben angegeben wird
   * Beispiel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, nicht `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Salt die Zeichenfolge nicht.


>[!IMPORTANT]
>
>Wenn Sie sich dafür entscheiden, keine E-Mail-Adressen zu hash, wird dies von Adobe Echtzeit-CDP für Sie ausgeführt, wenn Sie Segmente aktivieren für [!DNL Facebook]. Wählen Sie im Arbeitsablauf für die [Aktivierung](/help/rtcdp/destinations/activate-destinations.md#activate-data) (siehe Schritt 5) die `Email` Option wie unten für *E-Mail-Adressen* und `Email_LC_SHA256` für *Hash-E-Mail-Adressen* gezeigt.


![Hashing bei der Aktivierung](/help/rtcdp/destinations/assets/identity-mapping.png)

## Mit Ziel verbinden {#connect-destination}

To connect to the [!DNL Facebook] destination, see [Social network destinations authentication workflow](/help/rtcdp/destinations/social-network-destinations-workflow.md).


## Activate segments to [!DNL Facebook] {#activate-segments}

For instructions on how to activate segments to [!DNL Facebook], see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).

## Exportierte Daten {#exported-data}

For [!DNL Facebook], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segmentmitgliedschaft in der Zielgruppe wird hinzugefügt und entfernt, wenn Anwender für die aktivierten Segmente qualifiziert oder disqualifiziert werden.

>[!TIP]
>
>Die Integration zwischen Adobe Real-Time CDP und [!DNL Facebook] unterstützt historische Audiencen-Backfills. Alle historischen Segmentqualifikationen werden an gesendet, [!DNL Facebook] wenn Sie die Segmente an das Ziel aktivieren.