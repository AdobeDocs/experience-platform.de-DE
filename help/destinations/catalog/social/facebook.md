---
keywords: Facebook-Verbindung;Facebook-Verbindung;Facebook-Ziele;Facebook;Instagram;Messaging;Facebook-Botenenger
title: Facebook-Verbindung
description: Aktivieren Sie Profile für Ihre Facebook-Kampagnen zur Zielgruppenbestimmung, Personalisierung und Unterdrückung anhand von Hash-E-Mails.
translation-type: tm+mt
source-git-commit: bec44832a235dd3f9e2ee0f3ffc77854ee5784d7
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 13%

---


# [!DNL Facebook] connection

Aktivieren Sie Profil für Ihre [!DNL Facebook]-Kampagnen für Targeting, Personalisierung und Unterdrückung von Audiencen, die auf Hash-E-Mails basieren.

Sie können dieses Ziel für das Targeting von Audiencen in [!DNL Facebook’s]-Apps verwenden, die von [!DNL Custom Audiences] unterstützt werden, einschließlich [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] und [!DNL Messenger]. Die Auswahl der App, für die Sie die Kampagne ausführen möchten, wird auf der Platzierungsebene in [!DNL Facebook Ads Manager] angezeigt.

![Facebook-Ziel in der Adobe Experience Platform-Benutzeroberfläche](../../assets/catalog/social/facebook/catalog.png)

## Nutzungsszenarien

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Facebook]-Ziel verwenden sollten, gibt es zwei Beispielverwendungsfälle, die Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

### Verwendungsfall Nr. 1

Ein Online-Händler möchte bestehende Kunden über soziale Plattformen erreichen und ihnen personalisierte Angebot auf Basis ihrer bisherigen Bestellungen zeigen. Der Online-Händler kann E-Mail-Adressen aus seinem eigenen CRM-System nach Adobe Experience Platform erfassen, Segmente aus eigenen Offlinedaten erstellen und diese Segmente an die [!DNL Facebook]-Social-Plattform senden, um ihre Werbeausgaben zu optimieren.

### Verwendungsfall Nr. 2

Eine Fluggesellschaft hat verschiedene Kundenstufen (Bronze, Silver und Gold) und möchte jede dieser Stufen mit personalisierten Angeboten über soziale Plattformen versorgen. Nicht alle Kunden verwenden jedoch die mobile App der Fluggesellschaft, und einige von ihnen haben sich noch nicht bei der Website der Firma angemeldet. Die einzigen IDs, die die Firma zu diesen Kunden hat, sind Mitgliedschafts-IDs und E-Mail-Adressen.

Um sie über soziale Netzwerke hinweg Zielgruppe, können sie die Kundendaten aus ihrem CRM-System in Adobe Experience Platform einbinden und dabei die E-Mail-Adressen als Bezeichner verwenden.

Als Nächstes können sie ihre Offline-Daten einschließlich der zugehörigen Mitgliedschafts-IDs und Kundenebenen verwenden, um neue Audiencen zu erstellen, die sie über das [!DNL Facebook]-Ziel Zielgruppe werden können.

## Zielspezifikationen {#destination-specs}

### Datenverwaltung für [!DNL Facebook]-Ziele {#data-governance}

>[!IMPORTANT]
>
>Daten, die an [!DNL Facebook] gesendet werden, sollten keine gehefteten Identitäten enthalten. Sie sind für die Erfüllung dieser Verpflichtung verantwortlich und können dies tun, indem Sie sicherstellen, dass Segmente, die für die Aktivierung ausgewählt wurden, keine Heftoption in ihrer Fusionsrichtlinie verwenden. Erfahren Sie mehr über [Mergepolicies](/help/profile/ui/merge-policies.md).

### Exporttyp {#export-type}

**Segmentexport** : Sie exportieren alle Segmentmitglieder (Audience) mit den Bezeichnern (Name, Telefonnummer usw.) verwendet im Facebook-Ziel.

### Voraussetzungen für Facebook-Konten {#facebook-account-prerequisites}

Bevor Sie Zielgruppensegmente an [!DNL Facebook] senden können, müssen Sie sicherstellen, dass Sie die folgenden Voraussetzungen erfüllen:

- Für Ihr [!DNL Facebook]-Benutzerkonto muss die **[!DNL Manage campaigns]**-Berechtigung für das Anzeigenkonto aktiviert sein, das Sie verwenden möchten.
- Das Geschäftskonto **Adobe Experience Cloud** muss als Werbepartner in Ihrem [!DNL Facebook Ad Account] hinzugefügt werden. Verwenden Sie `business ID=206617933627973`. Weitere Informationen finden Sie unter [Hinzufügen Partner in Ihrem Business Manager](https://www.facebook.com/business/help/1717412048538897) in der Facebook-Dokumentation.
   >[!IMPORTANT]
   >
   > Beim Konfigurieren der Berechtigungen für Adobe Experience Cloud müssen Sie die Berechtigung **Kampagnen verwalten** aktivieren. Dies ist für die [!DNL Adobe Experience Platform]-Integration erforderlich.
- Lesen und unterschreiben Sie die [!DNL Facebook Custom Audiences]-Nutzungsbedingungen. Rufen Sie dazu `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]` auf, wobei `accountID` Ihre [!DNL Facebook Ad Account ID] ist.

### Anforderungen für die ID-Übereinstimmung {#id-matching-requirements}

[!DNL Facebook] verlangt, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher können die für [!DNL Facebook] aktivierten Audiencen anhand von *Hash*-IDs wie E-Mail-Adressen oder Telefonnummern ausgewertet werden.

Abhängig von der Art der IDs, die Sie in Adobe Experience Platform eingeben, müssen Sie die entsprechenden Anforderungen erfüllen.

#### Hashanforderungen für Telefonnummern {#phone-number-hashing-requirements}

Es gibt zwei Methoden zum Aktivieren von Telefonnummern in [!DNL Facebook]:

- **Rohe Telefonnummern** eingehen: Sie können rohe Telefonnummern im  [!DNL E.164] Format in  [!DNL Platform]aufnehmen, die bei der Aktivierung automatisch mit Hashing versehen werden. Wenn Sie diese Option wählen, achten Sie darauf, Ihre rohen Telefonnummern immer in den `Phone_E.164`-Namensraum einzugeben.
- **Hash-Telefonnummern** eingehen: Sie können Ihre Telefonnummern vorab hash, bevor Sie  [!DNL Platform]einsteigen. Wenn Sie diese Option wählen, vergewissern Sie sich, dass Sie stets Ihre Hash-Telefonnummern in den `Phone_SHA256`-Namensraum eingeben.

>[!NOTE]
>
>Telefonnummern, die in den `Phone`-Namensraum aufgenommen werden, können in [!DNL Facebook] nicht aktiviert werden.


#### Anforderungen für das E-Mail-Hashing {#email-hashing-requirements}

Sie können E-Mail-Adressen vor der Einbindung in Adobe Experience Platform als Hash-E-Mail-Adressen festlegen oder Sie können in Experience Platform mit E-Mail-Adressen arbeiten und sie von unserem Algorithmus auf Aktivierung hash lassen.

Weitere Informationen zum Eingeben von E-Mail-Adressen in Experience Platformen finden Sie unter [Überblick über die Stapelverarbeitung](/help/ingestion/batch-ingestion/overview.md) und [Übersicht über die Streaming-Erfassung](/help/ingestion/streaming-ingestion/overview.md).

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hash, stellen Sie sicher, dass folgende Anforderungen erfüllt sind:

- Entfernen Sie alle führenden und nachfolgenden Leerzeichen aus der E-Mail-Zeichenfolge. example: `johndoe@example.com`, nicht `<space>johndoe@example.com<space>`;
- Achten Sie beim Hashing der E-Mail-Zeichenfolgen darauf, die Zeichenfolge in Kleinbuchstaben mit Hash zu versehen.
   - Beispiel: `example@email.com`, nicht `EXAMPLE@EMAIL.COM`;
- Stellen Sie sicher, dass die Hash-Zeichenfolge nur in Kleinbuchstaben angegeben wird
   - Beispiel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, nicht `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Salt die Zeichenfolge nicht.

>[!NOTE]
>
>Daten von Namensräumen ohne Hash werden bei Aktivierung automatisch durch [!DNL Platform] gehasht.
> Attributquellendaten werden nicht automatisch mit Hashing versehen. Wenn Ihr Quellfeld ungehackte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Transformation]** anwenden, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash.
> Die Option **[!UICONTROL Transformation anwenden]** wird nur angezeigt, wenn Sie Attribute als Quellfelder auswählen. Es wird nicht angezeigt, wenn Sie Namensraum auswählen.

![Identitätszuordnungs-Transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

#### Verwenden benutzerdefinierter Namensraum {#custom-namespaces}

Bevor Sie den Namensraum `Extern_ID` verwenden können, um Daten an [!DNL Facebook] zu senden, müssen Sie sicherstellen, dass Sie Ihre eigenen IDs mit [!DNL Facebook Pixel] synchronisieren. Ausführliche Informationen finden Sie in der [offiziellen Dokumentation](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers).

## Mit Ziel verbinden {#connect-destination}

Informationen zum Herstellen einer Verbindung mit dem Ziel [!DNL Facebook] finden Sie unter [Authentifizierungsarbeitsablauf für Social-Netzwerkziele](./workflow.md).

## Aktivieren von Segmenten nach [!DNL Facebook] {#activate-segments}

Anweisungen zum Aktivieren von Segmenten in [!DNL Facebook] finden Sie unter [Daten in Ziele aktivieren](../../ui/activate-destinations.md).

Im Schritt **[!UICONTROL Segmentplan]** müssen Sie die [!UICONTROL Herkunft der Audience] angeben, wenn Sie Segmente an [!DNL Facebook Custom Audiences] senden.

![Facebook-Herkunft der Audience](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## Exportierte Daten {#exported-data}

Bei [!DNL Facebook] bedeutet eine erfolgreiche Aktivierung, dass eine [!DNL Facebook] benutzerdefinierte Audience programmgesteuert in [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/) erstellt wird. Segmentmitgliedschaft in der Zielgruppe wird hinzugefügt und entfernt, wenn Anwender für die aktivierten Segmente qualifiziert oder disqualifiziert werden.

>[!TIP]
>
>Die Integration zwischen Adobe Experience Platform und [!DNL Facebook] unterstützt Backfills für historische Audiencen. Alle historischen Segmentqualifikationen werden an [!DNL Facebook] gesendet, wenn Sie die Segmente an das Ziel aktivieren.