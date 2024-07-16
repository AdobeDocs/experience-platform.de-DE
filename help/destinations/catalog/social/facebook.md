---
keywords: facebook-Verbindung; facebook-Verbindung; facebook-Ziele; facebook; instagram; Messaging; facebook Messaging
title: Facebook-Verbindung
description: Aktivieren Sie Profile für Ihre Facebook-Kampagnen zum Zielgruppen-Targeting, zur Personalisierung und zur Unterdrückung auf der Basis von gehashten E-Mails.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 30%

---

# [!DNL Facebook]-Verbindung

## Übersicht {#overview}

Aktivieren Sie Profile für Ihre [!DNL Facebook]-Kampagnen für Zielgruppen-Targeting, Personalisierung und Unterdrückung basierend auf Hash-E-Mails.

Sie können dieses Ziel für Zielgruppen-Targeting in [!DNL Facebook's]-Apps verwenden, die von [!DNL Custom Audiences] unterstützt werden, einschließlich [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] und [!DNL Messenger]. Die Auswahl der App, für die Sie die Kampagne ausführen möchten, wird auf der Platzierungsebene in [!DNL Facebook Ads Manager] angezeigt.

![Facebook-Ziel in der Adobe Experience Platform-Benutzeroberfläche.](../../assets/catalog/social/facebook/catalog.png)

## Anwendungsfälle

Um Ihnen zu helfen, besser zu verstehen, wie und wann das [!DNL Facebook]-Ziel verwendet werden soll, finden Sie hier zwei Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

### Anwendungsfall 1

Ein Online-Einzelhändler möchte bestehende Kunden über soziale Plattformen erreichen und ihnen personalisierte Angebote basierend auf ihren bisherigen Bestellungen zeigen. Der Online-Einzelhändler kann E-Mail-Adressen aus seinem eigenen CRM-System in Adobe Experience Platform erfassen, Zielgruppen aus eigenen Offline-Daten erstellen und diese Zielgruppen an die [!DNL Facebook]-Social-Plattform senden, wodurch seine Werbeausgaben optimiert werden.

### Anwendungsfall 2

Eine Fluggesellschaft hat verschiedene Kundenstufen (Bronze, Silber und Gold) und möchte über soziale Plattformen für jede dieser Ebenen personalisierte Angebote bereitstellen. Es wird jedoch nicht von allen Kunden die App der Fluglinie verwendet, und einige von ihnen haben sich nicht bei der Website des Unternehmens angemeldet. Die einzigen IDs, die das Unternehmen über diese Kunden hat, sind Mitgliedschafts-IDs und E-Mail-Adressen.

Um sie über soziale Netzwerke hinweg anzusprechen, können sie die Kundendaten aus ihrem CRM-System in Adobe Experience Platform integrieren und dabei die E-Mail-Adressen als Kennungen verwenden.

Anschließend können sie ihre Offline-Daten einschließlich der zugehörigen Mitgliedschafts-IDs und Kundenebenen verwenden, um neue Zielgruppen zu erstellen, die sie über das [!DNL Facebook]-Ziel ansprechen können.

## Unterstützte Identitäten {#supported-identities}

[!DNL Facebook Custom Audiences] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [ID-Abgleich-Anforderungen](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namespaces für Klartext- bzw. Hash-Telefonnummern. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [ID-Übereinstimmungsanforderungen](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| extern_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

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
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder andere), die im Facebook-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen für facebook-Konten {#facebook-account-prerequisites}

Bevor Sie Ihre Zielgruppen an [!DNL Facebook] senden können, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* Ihr [!DNL Facebook] -Benutzerkonto muss vollen Zugriff auf die [!DNL Facebook Business Account] haben, die Inhaber des von Ihnen verwendeten Anzeigenkontos ist.
* Für Ihr [!DNL Facebook] -Benutzerkonto muss die Berechtigung **[!DNL Manage campaigns]** für das Werbekonto aktiviert sein, das Sie verwenden möchten.
* Das Geschäftskonto **Adobe Experience Cloud** muss als Werbepartner in Ihrem [!DNL Facebook Ad Account] hinzugefügt werden. Verwenden Sie `business ID=206617933627973`. Weitere Informationen finden Sie unter [Partner zu Ihrem Business Manager hinzufügen](https://www.facebook.com/business/help/1717412048538897) in der Facebook-Dokumentation.
  >[!IMPORTANT]
  >
  > Beim Konfigurieren der Berechtigungen für Adobe Experience Cloud müssen Sie die Berechtigung **Kampagnen verwalten** aktivieren. Die Berechtigung ist für die [!DNL Adobe Experience Platform] -Integration erforderlich.
* Lesen und unterschreiben Sie die [!DNL Facebook Custom Audiences]-Nutzungsbedingungen. Gehen Sie dazu zu `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, wobei `accountID` Ihre [!DNL Facebook Ad Account ID] ist.
  >[!IMPORTANT]
  >
  >Stellen Sie beim Signieren der [!DNL Facebook Custom Audiences]-Nutzungsbedingungen sicher, dass Sie dasselbe Benutzerkonto verwenden, das Sie für die Authentifizierung in der Facebook-API verwendet haben.

## Anforderungen an die ID-Übereinstimmung {#id-matching-requirements}

[!DNL Facebook] erfordert, dass keine personenbezogenen Daten (PII) klar gesendet werden. Daher können die für [!DNL Facebook] aktivierten Zielgruppen aus *Hash*-Identifikatoren wie E-Mail-Adressen oder Telefonnummern abgeleitet werden.

Abhängig vom Typ der IDs, die Sie in Adobe Experience Platform erfassen, müssen Sie die entsprechenden Anforderungen erfüllen.

## Hash-Anforderungen für Telefonnummern {#phone-number-hashing-requirements}

Es gibt zwei Methoden zum Aktivieren von Telefonnummern in [!DNL Facebook]:

* **Aufnahme von rohen Telefonnummern**: Sie können rohe Telefonnummern im Format [!DNL E.164] in [!DNL Platform] aufnehmen. Sie sind bei Aktivierung automatisch gehasht. Wenn Sie diese Option wählen, achten Sie darauf, Ihre rohen Telefonnummern immer in den Namespace `Phone_E.164` aufzunehmen.
* **Hash-Telefonnummern erfassen**: Sie können Ihre Telefonnummern vorab hash, bevor Sie sie in [!DNL Platform] aufnehmen. Wenn Sie diese Option wählen, achten Sie darauf, Ihre Hash-Telefonnummern immer in den Namespace `Phone_SHA256` aufzunehmen.

>[!NOTE]
>
>Telefonnummern, die in den Namespace `Phone` aufgenommen werden, können in [!DNL Facebook] nicht aktiviert werden.

## Anforderungen an das E-Mail-Hashing {#email-hashing-requirements}

Sie können E-Mail-Adressen vor der Aufnahme in Adobe Experience Platform hash-Adressen oder eindeutige E-Mail-Adressen in Experience Platform verwenden und diese bei der Aktivierung mit [!DNL Platform] hash lassen.

Weiterführende Informationen zur Aufnahme von E-Mail-Adressen in Experience Platform finden Sie in der [Batch-Erfassungsübersicht](/help/ingestion/batch-ingestion/overview.md) und der [Streaming-Erfassungsübersicht](/help/ingestion/streaming-ingestion/overview.md).

Wenn Sie die E-Mail-Adressen selbst hash möchten, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

* Entfernen Sie alle Leerzeichen am Anfang und am Ende der E-Mail-Zeichenfolge. Beispiel: `johndoe@example.com`, nicht `<space>johndoe@example.com<space>`;
* Achten Sie beim Hashing der E-Mail-Zeichenfolgen darauf, die Zeichenfolge in Kleinbuchstaben zu hash;
   * Beispiel: `example@email.com`, nicht `EXAMPLE@EMAIL.COM`;
* Stellen Sie sicher, dass der Hash-String nur in Kleinbuchstaben geschrieben wird.
   * Beispiel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, nicht `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Salz die Zeichenfolge nicht.

>[!NOTE]
>
>Daten aus nicht gehashten Namespaces werden bei Aktivierung automatisch von [!DNL Platform] gehasht.
> Attributquellendaten werden nicht automatisch gehasht. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht.
> Die Option **[!UICONTROL Transformation anwenden]** wird nur angezeigt, wenn Sie Attribute als Quellfelder auswählen. Es wird nicht angezeigt, wenn Sie Namespaces auswählen.

![Wenden Sie die im Zuordnungsschritt hervorgehobene Transformationssteuerung an.](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Verwenden benutzerdefinierter Namespaces {#custom-namespaces}

Bevor Sie den Namespace `Extern_ID` zum Senden von Daten an [!DNL Facebook] verwenden können, müssen Sie Ihre eigenen Kennungen mit [!DNL Facebook Pixel] synchronisieren. Detaillierte Informationen finden Sie in der [offiziellen Facebook-Dokumentation](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) .

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Das folgende Video zeigt auch die Schritte zum Konfigurieren eines [!DNL Facebook] -Ziels und zum Aktivieren von Zielgruppen.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Die Benutzeroberfläche von Experience Platform wird häufig aktualisiert und kann sich seit der Aufzeichnung dieses Videos geändert haben. Die aktuellsten Informationen finden Sie im Tutorial zur Zielkonfiguration [.](../../ui/connect-destination.md)

### Beim Ziel authentifizieren {#authenticate}

1. Suchen Sie das Facebook-Ziel im Zielkatalog und wählen Sie **[!UICONTROL Einrichten]** aus.
2. Wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.
   ![Authentifizieren Sie sich bei Facebook , der im Aktivierungs-Workflow angezeigt wird.](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. Geben Sie Ihre Facebook-Anmeldedaten ein und wählen Sie **Anmelden** aus.

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="Konto-ID"
>abstract="Ihre Facebook-Werbekonto-ID. Diese ID finden Sie im Facebook-Werbeanzeigenmanager-Konto. Stellen Sie bei der Eingabe dieser ID immer das Präfix `act_` voran."

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre [!DNL Facebook Ad Account ID]. Sie finden diese ID in Ihrem [!DNL Facebook Ads Manager] -Konto. Stellen Sie bei der Eingabe dieser ID immer das Präfix `act_` voran.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="Ursprung der Zielgruppe"
>abstract="Wählen Sie aus, wie die Kundendaten in der Zielgruppe ursprünglich erfasst wurden. Die Daten werden in Facebook angezeigt, wenn eine Person zur Zielgruppe des Segments gehört"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="Ursprung der Zielgruppe"
>abstract="Werbetreibende erfassten Daten direkt bei ihren Kundinnen und Kunden."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="Ursprung der Zielgruppe"
>abstract="Werbetreibende erfassten Daten direkt bei ihren Partnerinnen und Partnern."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="Ursprung der Zielgruppe"
>abstract="Werbetreibende erfassten Daten direkt bei ihren Kundinnen, Kunden, Partnerinnen und Partnern."

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

Im Schritt **[!UICONTROL Segmentplan]** müssen Sie beim Senden von Zielgruppen an [!DNL Facebook Custom Audiences] den [!UICONTROL Ursprung der Zielgruppe] angeben.

![Herkunft der Audience-Dropdown-Liste, die im Facebook-Aktivierungsschritt angezeigt wird.](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Zuordnungsbeispiel: Aktivieren von Zielgruppendaten in [!DNL Facebook Custom Audience] {#example-facebook}

Nachstehend finden Sie ein Beispiel für die korrekte Identitätszuordnung bei der Aktivierung von Zielgruppendaten in [!DNL Facebook Custom Audience].

Quellfelder auswählen:

* Wählen Sie den Namespace `Email` als Quellidentität aus, wenn die von Ihnen verwendeten E-Mail-Adressen nicht gehasht werden.
* Wählen Sie den Namespace `Email_LC_SHA256` als Quellidentität aus, wenn Sie Kunden-E-Mail-Adressen bei der Datenerfassung gemäß den Anforderungen für den E-Mail-Hashing [!DNL Facebook] [E-Mail-Hashing](#email-hashing-requirements) in [!DNL Platform] gehasht haben.
* Wählen Sie den Namespace `PHONE_E.164` als Quellkennung aus, wenn Ihre Daten aus nicht gehashten Telefonnummern bestehen. [!DNL Platform] hasst die Telefonnummern, um die [!DNL Facebook]-Anforderungen zu erfüllen.
* Wählen Sie den Namespace `Phone_SHA256` als Quellidentität aus, wenn Sie bei der Datenerfassung Telefonnummern gemäß den Anforderungen für das Hashing der Telefonnummer [!DNL Facebook] [4 bei der Erfassung der Daten in [!DNL Platform] gehasht haben.](#phone-number-hashing-requirements)
* Wählen Sie den Namespace `IDFA` als Quellidentität aus, wenn Ihre Daten aus [!DNL Apple] Geräte-IDs bestehen.
* Wählen Sie den Namespace `GAID` als Quellidentität aus, wenn Ihre Daten aus [!DNL Android] Geräte-IDs bestehen.
* Wählen Sie den Namespace `Custom` als Quellidentität aus, wenn Ihre Daten aus anderen Kennungen bestehen.

Zielgruppenfelder auswählen:

* Wählen Sie den Namespace `Email_LC_SHA256` als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `Email` oder `Email_LC_SHA256` sind.
* Wählen Sie den Namespace `Phone_SHA256` als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `PHONE_E.164` oder `Phone_SHA256` sind.
* Wählen Sie die Namespaces `IDFA` oder `GAID` als Zielidentität aus, wenn Ihre Quell-Namespaces `IDFA` oder `GAID` sind.
* Wählen Sie den Namespace `Extern_ID` als Zielidentität aus, wenn Ihr Quellnamespace ein benutzerdefinierter Namespace ist.

>[!IMPORTANT]
>
>Daten aus nicht gehashten Namespaces werden bei Aktivierung automatisch von [!DNL Platform] gehasht.
> 
>Attributquellendaten werden nicht automatisch gehasht. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht.

![Wenden Sie die im Zuordnungsschritt hervorgehobene Transformationssteuerung an.](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Exportierte Daten {#exported-data}

Für [!DNL Facebook] bedeutet eine erfolgreiche Aktivierung, dass eine benutzerdefinierte [!DNL Facebook] Zielgruppe programmgesteuert in [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/) erstellt wird. Die Zielgruppenmitgliedschaft wird hinzugefügt und entfernt, da Benutzer für die aktivierten Zielgruppen qualifiziert oder disqualifiziert sind.

>[!TIP]
>
>Die Integration zwischen Adobe Experience Platform und [!DNL Facebook] unterstützt historische Zielgruppen-Backups. Alle historischen Zielgruppenqualifikationen werden an [!DNL Facebook] gesendet, wenn Sie die Zielgruppen für das Ziel aktivieren.

## Fehlerbehebung {#troubleshooting}

### Fehlermeldung „400 Fehlerhafte Anfrage“ {#bad-request}

Beim Konfigurieren dieses Ziels wird möglicherweise der folgende Fehler angezeigt:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Dieser Fehler tritt auf, wenn Kunden neu erstellte Konten verwenden und die [!DNL Facebook] -Berechtigungen noch nicht aktiv sind.

Wenn Sie die Fehlermeldung `400 Bad Request` erhalten, nachdem Sie die Schritte unter [Voraussetzungen für Facebook-Konten](#facebook-account-prerequisites) ausgeführt haben, lassen Sie einige Tage zu, bis die [!DNL Facebook] -Berechtigungen in Kraft treten.
