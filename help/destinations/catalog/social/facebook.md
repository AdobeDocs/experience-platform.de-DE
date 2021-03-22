---
keywords: Facebook-Verbindung;Facebook-Verbindung;Facebook-Ziele;Facebook;Instagram;Messaging;Facebook-Botenenger
title: Facebook-Verbindung
description: Aktivieren Sie Profil für Ihre Facebook-Kampagnen für Targeting, Personalisierung und Unterdrückung von Audiencen, die auf Hash-E-Mails basieren.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 8%

---


# [!DNL Facebook] connection

## Übersicht {#overview}

Aktivieren Sie Profil für Ihre [!DNL Facebook]-Kampagnen für Targeting, Personalisierung und Unterdrückung von Audiencen, die auf Hash-E-Mails basieren.

Sie können dieses Ziel für das Targeting von Audiencen in [!DNL Facebook’s]-Apps verwenden, die von [!DNL Custom Audiences] unterstützt werden, einschließlich [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] und [!DNL Messenger]. Die Auswahl der App, für die Sie die Kampagne ausführen möchten, wird auf der Platzierungsebene in [!DNL Facebook Ads Manager] angezeigt.

![Facebook-Ziel in der Adobe Experience Platform-Benutzeroberfläche](../../assets/catalog/social/facebook/catalog.png)

## Nutzungsszenarien

Damit Sie besser verstehen können, wie und wann das [!DNL Facebook]-Ziel verwendet werden soll, gibt es zwei Beispielverwendungsfälle, die Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

### Verwendungsfall Nr. 1

Ein Online-Händler möchte bestehende Kunden über soziale Plattformen erreichen und ihnen personalisierte Angebot auf Basis ihrer bisherigen Bestellungen zeigen. Der Online-Händler kann E-Mail-Adressen aus seinem eigenen CRM-System nach Adobe Experience Platform erfassen, Segmente aus eigenen Offlinedaten erstellen und diese Segmente an die [!DNL Facebook]-Social-Plattform senden, um ihre Werbeausgaben zu optimieren.

### Verwendungsfall Nr. 2

Eine Fluggesellschaft hat verschiedene Kundenstufen (Bronze, Silver und Gold) und möchte jede dieser Stufen mit personalisierten Angeboten über soziale Plattformen versorgen. Nicht alle Kunden verwenden jedoch die mobile App der Fluggesellschaft, und einige von ihnen haben sich noch nicht bei der Website der Firma angemeldet. Die einzigen IDs, die die Firma zu diesen Kunden hat, sind Mitgliedschafts-IDs und E-Mail-Adressen.

Um sie über soziale Netzwerke hinweg Zielgruppe, können sie die Kundendaten aus ihrem CRM-System in Adobe Experience Platform einbinden und dabei die E-Mail-Adressen als Bezeichner verwenden.

Als Nächstes können sie ihre Offline-Daten einschließlich der zugehörigen Mitgliedschafts-IDs und Kundenebenen verwenden, um neue Audiencen zu erstellen, die sie über das [!DNL Facebook]-Ziel Zielgruppe werden können.

## Datenverwaltung für [!DNL Facebook]-Ziele {#data-governance}

>[!IMPORTANT]
>
>Daten, die an [!DNL Facebook] gesendet werden, dürfen keine gehefteten Identitäten enthalten. Sie sind für die Erfüllung dieser Verpflichtung verantwortlich und können dies tun, indem Sie sicherstellen, dass Segmente, die für die Aktivierung ausgewählt wurden, keine Heftoption in ihrer Fusionsrichtlinie verwenden. Erfahren Sie mehr über [Mergepolicies](/help/profile/ui/merge-policies.md).

## Unterstützte Identitäten {#supported-identities}

[!DNL Facebook Custom Audiences] unterstützt die Aktivierung der Identitäten, die in der folgenden Tabelle beschrieben sind. Erfahren Sie mehr über [identities](/help/identity-service/namespaces.md).

| Zielgruppe | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google Advertising ID | Wählen Sie die GAID-Zielgruppe-ID aus, wenn Ihre Quellidentität ein GAID-Namensraum ist. |
| IDFA | Apple-ID für Werbetreibende | Wählen Sie die IDFA-Zielgruppen-ID aus, wenn Ihre Quellidentität ein IDFA-Namensraum ist. |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht werden | Sowohl Normaltext- als auch SHA256-Hash-Telefonnummern werden von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [Anforderungen für die ID-Zuordnung](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namensraum für einfache und hash-Telefonnummern. Wenn Ihr Quellfeld ungehackte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Transformation]** anwenden, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash. |
| email_lc_sha256 | Mit dem SHA256-Algorithmus verfasste E-Mail-Adressen | Sowohl einfache als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [Anforderungen für die ID-Zuordnung](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namensraum für E-Mail-Adressen mit Standardtext bzw. Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehackte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Transformation]** anwenden, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash. |
| extern_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielgruppen-ID aus, wenn Ihre Quellidentität ein benutzerdefinierter Namensraum ist. |

## Exporttyp {#export-type}

**Segmentexport** : Sie exportieren alle Segmentmitglieder (Audiencen) mit den IDs (Name, Telefonnummer oder andere), die im Facebook-Ziel verwendet werden.

## Voraussetzungen für Facebook-Konten {#facebook-account-prerequisites}

Bevor Sie Zielgruppensegmente an [!DNL Facebook] senden können, müssen Sie sicherstellen, dass Sie die folgenden Voraussetzungen erfüllen:

- Für Ihr [!DNL Facebook]-Benutzerkonto muss die **[!DNL Manage campaigns]**-Berechtigung für das Anzeigenkonto aktiviert sein, das Sie verwenden möchten.
- Das Geschäftskonto **Adobe Experience Cloud** muss als Werbepartner in Ihrem [!DNL Facebook Ad Account] hinzugefügt werden. Verwenden Sie `business ID=206617933627973`. Weitere Informationen finden Sie unter [Hinzufügen Partner in Ihrem Business Manager](https://www.facebook.com/business/help/1717412048538897) in der Facebook-Dokumentation.
   >[!IMPORTANT]
   >
   > Beim Konfigurieren der Berechtigungen für Adobe Experience Cloud müssen Sie die Berechtigung **Kampagnen verwalten** aktivieren. Die Berechtigung ist für die [!DNL Adobe Experience Platform]-Integration erforderlich.
- Lesen und unterschreiben Sie die [!DNL Facebook Custom Audiences]-Nutzungsbedingungen. Gehen Sie dazu zu `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, wobei `accountID` Ihr [!DNL Facebook Ad Account ID] ist.

## Anforderungen für die ID-Übereinstimmung {#id-matching-requirements}

[!DNL Facebook] verlangt, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher können die für [!DNL Facebook] aktivierten Audiencen anhand von *Hash*-IDs wie E-Mail-Adressen oder Telefonnummern ausgewertet werden.

Abhängig von der Art der IDs, die Sie in Adobe Experience Platform eingeben, müssen Sie die entsprechenden Anforderungen erfüllen.

## Hashanforderungen für Telefonnummern {#phone-number-hashing-requirements}

Es gibt zwei Methoden zum Aktivieren von Telefonnummern in [!DNL Facebook]:

- **Rohe Telefonnummern** eingehen: Sie können rohe Telefonnummern im  [!DNL E.164] Format in  [!DNL Platform]. Sie sind automatisch auf die Aktivierung gestoßen. Wenn Sie diese Option wählen, achten Sie darauf, Ihre rohen Telefonnummern immer in den `Phone_E.164`-Namensraum einzugeben.
- **Hash-Telefonnummern** eingehen: Sie können Ihre Telefonnummern vorab hash, bevor Sie  [!DNL Platform]einsteigen. Wenn Sie diese Option wählen, vergewissern Sie sich, dass Sie stets Ihre Hash-Telefonnummern in den `Phone_SHA256`-Namensraum eingeben.

>[!NOTE]
>
>Telefonnummern, die in den `Phone`-Namensraum aufgenommen werden, können in [!DNL Facebook] nicht aktiviert werden.


## Anforderungen für das E-Mail-Hashing {#email-hashing-requirements}

Sie können E-Mail-Adressen vor dem Eingeben in Adobe Experience Platform hash oder in der Experience Platform eindeutige E-Mail-Adressen verwenden und sie bei der Aktivierung mit [!DNL Platform] Hash versehen.

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

## Verwenden benutzerdefinierter Namensraum {#custom-namespaces}

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