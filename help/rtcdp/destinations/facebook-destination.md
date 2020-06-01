---
title: Facebook-Ziel
seo-title: Facebook-Ziel
description: Aktivieren Sie Profil für Ihre Facebook-Kampagnen für Targeting, Personalisierung und Unterdrückung von Audiencen, die auf Hash-E-Mails basieren.
seo-description: Aktivieren Sie Profil für Ihre Facebook-Kampagnen für Targeting, Personalisierung und Unterdrückung von Audiencen, die auf Hash-E-Mails basieren.
translation-type: tm+mt
source-git-commit: 79aecf4955507622ac7879c148cdcd23e893dd65
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---


# Facebook-Ziel

## Übersicht {#overview}

Aktivieren Sie Profil für Ihre Facebook-Kampagnen für Targeting, Personalisierung und Unterdrückung von Audiencen, die auf Hash-E-Mails basieren.

![Facebook-Ziel in der CDP-Benutzeroberfläche in Echtzeit](/help/rtcdp/destinations/assets/facebook-destination.png)

## Nutzungsszenarien

Damit Sie besser verstehen können, wie und wann Sie das Facebook-Ziel verwenden sollten, gibt es zwei Beispielverwendungsfälle, die Kunden der Adobe Echtzeit-Kundendatenplattform mit dieser Funktion lösen können.


### Verwendungsfall Nr. 1


Ein Online-Händler möchte bestehende Kunden über soziale Plattformen erreichen und ihnen personalisierte Angebot auf Basis ihrer bisherigen Bestellungen zeigen. Der Online-Händler kann E-Mail-Adressen aus seinem eigenen CRM an Adobe Echtzeit-CDP erfassen, Segmente aus eigenen Offlinedaten erstellen und diese Segmente an die Facebook-Social-Plattform senden, um ihre Werbeausgaben zu optimieren.


### Verwendungsfall Nr. 2


Eine Fluggesellschaft hat verschiedene Kundenstufen (Bronze, Silver und Gold) und möchte jede dieser Stufen mit personalisierten Angeboten über soziale Plattformen versorgen. Nicht alle Kunden verwenden jedoch die mobile App der Fluggesellschaft, und einige von ihnen haben sich noch nicht bei der Website der Firma angemeldet. Die einzigen IDs, die die Firma zu diesen Kunden hat, sind Mitgliedschafts-IDs und E-Mail-Adressen.

Um sie über soziale Netzwerke hinweg Zielgruppe, können sie die Kundendaten aus ihrem CRM-System in Adobe Echtzeit-CDP einbinden und dabei die E-Mail-Adressen als ID verwenden.

Als Nächstes können sie ihre Offline-Daten einschließlich der zugehörigen Mitgliedschafts-IDs und Kundenebenen verwenden, um neue Audiencen zu erstellen, die sie über das Facebook-Ziel Zielgruppe haben.

## Zielspezifikationen {#destination-specs}

### Datenverwaltung für Facebook-Ziele {#data-governance}

>[!IMPORTANT]
>
>Daten, die an Facebook gesendet werden, sollten keine zugefügten Identitäten enthalten. Sie sind für die Erfüllung dieser Verpflichtung verantwortlich und können dies tun, indem Sie sicherstellen, dass Segmente, die für die Aktivierung ausgewählt wurden, keine Heftoption in ihrer Fusionsrichtlinie verwenden. Weitere Informationen zu [Zusammenführungsrichtlinien](/help/profile/ui/merge-policies.md).

### Aktivierung {#activation-type}

**Segmentexport** : Sie exportieren alle Segmentmitglieder (Audience) mit den Bezeichnern (Name, Telefonnummer usw.) im Facebook-Ziel verwendet.

### Voraussetzungen für Facebook-Konten {#facebook-account-prerequisites}

Bevor Sie Ihre Audiencen an senden können, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen: [!DNL Facebook]

1. Für Ihr [!DNL Facebook] Benutzerkonto muss die **[!DNL Manage campaigns]** Berechtigung für das Anzeigenkonto aktiviert sein, das Sie verwenden möchten.
2. Hinzufügen Sie das **Adobe Experience Cloud** -Geschäftskonto als Werbepartner in Ihrem [!DNL Facebook Ad Account]. Verwenden Sie `business ID=206617933627973`. Weitere Informationen finden Sie unter [Hinzufügen Partner zu Ihrem Business Manager](https://www.facebook.com/business/help/1717412048538897) in der Facebook-Dokumentation.
   >[!IMPORTANT]
   > Beim Konfigurieren der Berechtigungen für Adobe Experience Cloud müssen Sie die Berechtigung &quot;Kampagnen **verwalten** &quot;aktivieren. Dies ist für die [!DNL Adobe Real-time CDP] Integration erforderlich.
3. Lesen und unterzeichnen Sie die [!DNL Facebook Custom Audiences] Nutzungsbedingungen. Um das zu tun, gehen Sie zu `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, wo `accountID` ist Ihr [!DNL Facebook Ad Account ID].

### Anforderungen für das E-Mail-Hashing {#email-hashing-requirements}

Facebook verlangt, dass keine personenbezogenen Daten (PII) klar gesendet werden. Daher müssen die für Facebook aktivierten Audiencen von *Hash* -E-Mail-Adressen abgekoppelt werden. Sie können festlegen, dass E-Mail-Adressen Hash-Adressen verwendet werden, bevor Sie sie in Adobe Experience Platform übernehmen, oder Sie können festlegen, dass E-Mail-Adressen in Experience Platform eindeutig verwendet werden und dass unser Algorithmus sie bei der Aktivierung hash.

Weitere Informationen zum Eingeben von E-Mail-Adressen in Experience Platform finden Sie in der Übersicht über die [Stapelverarbeitung](/help/ingestion/batch-ingestion/overview.md) und in der Übersicht über die [Erfassung](/help/ingestion/streaming-ingestion/overview.md)von Streaming-Adressen.

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hash, stellen Sie sicher, dass folgende Anforderungen erfüllt sind:

* Entfernen Sie alle führenden und nachfolgenden Leerzeichen aus der E-Mail-Zeichenfolge. example: `johndoe@example.com`, nicht `<space>johndoe@example.com<space>`;
* Achten Sie beim Hashing der E-Mail-Zeichenfolgen darauf, die Zeichenfolge in Kleinbuchstaben mit Hash zu versehen.
   * Beispiel: `example@email.com`, nicht `EXAMPLE@EMAIL.COM`;
* Stellen Sie sicher, dass die Hash-Zeichenfolge nur in Kleinbuchstaben angegeben wird
   * Beispiel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, nicht `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Salt die Zeichenfolge nicht.


>[!IMPORTANT]
>
>Wenn Sie sich dafür entscheiden, keine E-Mail-Adressen zu hash, wird dies von Adobe Echtzeit-CDP für Sie ausgeführt, wenn Sie Segmente in Facebook aktivieren. Wählen Sie im Arbeitsablauf für die [Aktivierung](/help/rtcdp/destinations/activate-destinations.md#activate-data) (siehe Schritt 5) die `Email` Option wie unten für *E-Mail-Adressen* und `Email_LC_SHA256` für *Hash-E-Mail-Adressen* gezeigt.


![Hashing bei der Aktivierung](/help/rtcdp/destinations/assets/identity-mapping.png)

## Mit Ziel verbinden {#connect-destination}

Informationen zum Herstellen einer Verbindung mit dem Facebook-Ziel finden Sie unter Authentifizierungsarbeitsablauf für [Social-Netzwerkziele](/help/rtcdp/destinations/social-network-destinations-workflow.md).


## Aktivieren von Segmenten auf Facebook {#activate-segments}

For instructions on how to activate segments to Facebook, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).