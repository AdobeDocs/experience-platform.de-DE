---
title: The Trade Desk - CRM-Verbindung
description: Profile für Ihr Trade Desk-Konto aktivieren, um Zielgruppen-Targeting und -Unterdrückung auf der Grundlage von CRM-Daten durchzuführen.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 47d4078acc73736546d4cbb2d17b49bf8945743a
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 8%

---

# Die [!DNL Trade Desk] - CRM-Verbindung

>[!IMPORTANT]
>
>Es gibt zwei The Trade Desk - CRM-Ziele im [Zielkatalog](/help/destinations/catalog/overview.md).
>
>* Wenn Sie Daten in der EU beziehen, verwenden Sie das **[!DNL The Trade Desk - CRM (EU)]**.
>* Wenn Sie Daten in der APAC- oder NAMER-Region beziehen, verwenden Sie das **[!DNL The Trade Desk - CRM (NAMER & APAC)]** .
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden vom *[!DNL Trade Desk]*-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte an Ihren [!DNL Trade Desk].

## Übersicht {#overview}

Erfahren Sie, wie Sie Profile in Ihrem [!DNL Trade Desk]-Konto aktivieren können, um Zielgruppen-Targeting und -Unterdrückung auf der Grundlage von CRM-Daten durchzuführen.

Dieser Connector sendet Daten zur Aktivierung von Erstanbieter-Daten an [!DNL The Trade Desk]. [!DNL The Trade Desk] speichern Sie Ihre rohen (ungehashten) E-Mails und Telefonnummern.

>[!TIP]
>
>Verwenden Sie [!DNL The Trade Desk - CRM] Ziel, um CRM-Daten (z. B. E-Mails und Telefonnummern) und andere First-Party-Datenkennungen wie Cookies und Geräte-IDs zu senden. Sie können weiterhin das [Trade Desk-Ziel](/help/destinations/catalog/advertising/tradedesk.md) im Experience Platform-Katalog für Cookies und Geräte-ID-Zuordnungen verwenden.

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
>Bevor Sie Zielgruppen für das Trade Desk aktivieren können, müssen Sie sich an Ihren [!DNL Trade Desk] Account Manager wenden, um die Funktion zu aktivieren. Wenn Sie E-Mails, Telefonnummern und UID2/EUID senden, müssen Sie den unterzeichneten UID2/EUID-Vertrag mit [!DNL The Trade Desk] teilen.

## Anforderungen für den ID-Abgleich {#id-matching-requirements}

Je nach Typ der IDs, die Sie in Adobe Experience Platform aufnehmen, müssen Sie die entsprechenden Anforderungen erfüllen. Weitere Informationen finden Sie [ „Übersicht ](/help/identity-service/features/namespaces.md) Identitäts-Namespaces“.

## Unterstützte Identitäten {#supported-identities}

[!DNL The Trade Desk] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

Adobe Experience Platform unterstützt sowohl ungehashte als auch gehashte E-Mail-Adressen und Telefonnummern. Befolgen Sie die Anweisungen im Abschnitt Anforderungen an den ID-Abgleich und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mail-Adressen.

| Ziel-Identität | Beschreibung |
|---|---|
| E-Mail | E-Mail-Adressen (Klartext) |
| Email_LC_SHA256 | E-Mail-Adressen müssen mit SHA256 in Kleinbuchstaben gehasht werden. Sie können diese Einstellung später nicht mehr ändern. |
| Telefon (E.164) | Telefonnummern, die im E.164-Format normalisiert werden müssen. Das Format E.164 enthält ein Pluszeichen (+), eine internationale Landesvorwahl, eine Ortsvorwahl und eine Telefonnummer. Beispiel: (+)(Länder-Code)(Ortsvorwahl)(Telefonnummer). Diese Kennung ist nicht verfügbar für „The Trade Desk - First-Party Data“ (EU). |
| Phone (SHA256_E.164) | Telefonnummern, die bereits auf das E.164-Format normalisiert und dann mit SHA-256 gehasht wurden, mit dem resultierenden Hash-Base64-kodiert. Diese Kennung ist nicht verfügbar für „The Trade Desk - First-Party Data“ (EU). |
| TDID | Cookie-ID im Trade Desk |
| GAID | GOOGLE ADVERTISING ID |
| IDFA | Apple-ID für Werbetreibende |
| UID2 | Der unformatierte UID2-Wert |
| UID2Token | Das verschlüsselte UID2-Token, auch als Werbe-Token bezeichnet. |
| EUID | Der rohe ID-Wert der Europäischen Union |
| EUIDToken | Das verschlüsselte EUID-Token, auch als Werbe-Token bezeichnet. |
| RampID | Die RampID mit 49 oder 70 Zeichen (früher IdentityLink oder IDL genannt). Dies muss eine RampID von LiveRamp sein, die speziell für The Trade Desk zugeordnet ist. |
| netID | Die netID des Benutzers als eine mit Base64 verschlüsselte Zeichenfolge mit 70 Zeichen. Diese ID wird nur in Europa unterstützt. |
| FirstID | Die First-ID des Benutzers, ein Erstanbieter-Cookie, das normalerweise von Herausgebern in Frankreich gesetzt wird. Diese ID wird nur in Europa unterstützt. |

{style="table-layout:auto"}

## Hash-Anforderungen für E-Mails {#email-hashing}

Sie können E-Mail-Adressen hashen, bevor Sie sie in Adobe Experience Platform aufnehmen, oder rohe E-Mail-Adressen verwenden.

Weitere Informationen zum Aufnehmen von E-Mail-Adressen in Experience Platform finden Sie unter [Übersicht über die Batch-Aufnahme](/help/ingestion/batch-ingestion/overview.md).

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hashen, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

* Leerzeichen am Anfang und Ende entfernen.
* Wandeln Sie alle ASCII-Zeichen in Kleinbuchstaben um.
* Entfernen Sie in `gmail.com` E-Mail-Adressen die folgenden Zeichen aus dem Teil Benutzername der E-Mail-Adresse:

      * Der Zeitraum (“.„) Zeichen (ASCII-Code 46). Normalisieren Sie beispielsweise &quot;jane.doe@gmail.com&quot; auf &quot;janedoe@gmail.com&quot;.
     * Das Pluszeichen (`+`) (ASCII-Code 43) und alle nachfolgenden Zeichen. Normalisieren Sie beispielsweise &quot;janedoe+home@gmail.com&quot; auf &quot;janedoe@gmail.com&quot;.
  
## Normalisierungs- und Hash-Anforderungen für Telefonnummern {#phone-hashing}

Hier finden Sie, was Sie über das Hochladen von Telefonnummern wissen müssen:

* Sie müssen Telefonnummern normalisieren, bevor Sie sie in einer Anfrage senden, unabhängig davon, ob Sie sie in einer Anfrage gehasht oder unhasht senden.
* Um normalisierte, Hash- und kodierte Daten hochzuladen, müssen Sie Telefonnummern als Base64-kodierte SHA-256-Hashes der normalisierten Telefonnummern senden.

Unabhängig davon, ob Sie rohe oder Hash-Telefonnummern hochladen möchten, müssen Sie sie normalisieren.

>[!IMPORTANT]
>
>Die Normalisierung vor dem Hashing stellt sicher, dass der generierte ID-Wert immer gleich ist und die Daten genau abgeglichen werden können.

Im Folgenden finden Sie Informationen zu den Normalisierungsanforderungen für Telefonnummern:

* Der UID2-Operator akzeptiert Telefonnummern im E.164-Format, dem internationalen Telefonnummernformat, das die weltweite Eindeutigkeit sicherstellt.
* E.164-Telefonnummern können maximal 15 Stellen haben.
* Normalisierte E.164-Telefonnummern verwenden die folgende Syntax: `[+][country code][subscriber number including area code]` ohne Leerzeichen, Bindestriche, Klammern oder andere Sonderzeichen. Im Folgenden finden Sie einige Beispiele:

      * US: 1 (234) 567-8901 wird auf +12345678901 normalisiert.
     * Singapur: 65 1243 5678 wird auf +6512345678 normalisiert.
     * Australien: Handy-Nummer 0491 570 006 ist normalisiert, um den Länder-Code hinzuzufügen und die führende Null: +61491570006.
     * GB: Mobiltelefonnummer 07812 345678 wird normalisiert, um den Ländercode hinzuzufügen und die führende Null zu löschen: +447812345678.
  
Stellen Sie sicher, dass die normalisierte Telefonnummer UTF-8 lautet, nicht ein anderes Kodierungssystem wie UTF-16.

Ein Telefonnummern-Hash ist ein Base64-kodierter SHA-256-Hash einer normalisierten Telefonnummer. Die Telefonnummer wird zunächst normalisiert, dann mit dem SHA-256-Hash-Algorithmus gehasht und dann die resultierenden Bytes des Hash-Werts mit Base64-Codierung codiert. Beachten Sie, dass die Base64-Codierung auf die Bytes des Hash-Werts angewendet wird, nicht auf die hexadezimal codierte Zeichenfolgendarstellung.
Die folgende Tabelle zeigt ein Beispiel für eine einfache Eingabe-Telefonnummer, und das Ergebnis wird bei jedem Schritt angewendet, um einen sicheren, undurchsichtigen Wert zu erhalten.

| Typ | Beispiel | Kommentare und Verwendung |
|---|---|---|
| Rohe Telefonnummer | 1 (234) 567-8901 | Dies ist der Ausgangspunkt. |
| Normalisierte Telefonnummer | +12345678901 | Die Normalisierung ist immer der erste Schritt. |
| SHA-256-Hash der normalisierten Telefonnummer | 10e6f0b47054a83359477dcb35231db6de5c69fb1816e1a6b98e192de9e5b9ee | Diese 64-stellige Zeichenfolge ist eine hexadezimal codierte Darstellung des 32-Byte-SHA-256. |
| Hex zu Base64 SHA-256-Kodierung der normalisierten und gehashten Telefonnummer | EObwtHBUqDNZR33LNSMdtt5cafsYFuGMUY4ZLenlue4 | Diese 44-stellige Zeichenfolge ist eine Base64-kodierte Darstellung des 32-Byte-SHA-256. Der SHA-256-Hash ist ein Hexadezimalwert. Sie müssen einen Base64-Encoder verwenden, der einen Hexadezimalwert als Eingabe verwendet. Verwenden Sie diese Codierung für phone_hash-Werte, die im Anfrageinhalt gesendet werden. |

>[!IMPORTANT]
>
>Stellen Sie beim Anwenden der Base64-Codierung sicher, dass Sie eine Funktion verwenden, die einen Hexadezimalwert als Eingabe akzeptiert. Wenn Sie eine Funktion verwenden, die Text als Eingabe verwendet, ist das Ergebnis eine längere Zeichenfolge, die für UID2 ungültig ist.

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Audience mit den IDs (E-Mail oder Hash-E-Mail), die im Trade Desk-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Daily Batch]** | Da ein Profil in Experience Platform auf der Grundlage einer Zielgruppenbewertung aktualisiert wird, werden die Profile (Identitäten) einmal täglich nachgelagert auf der Zielplattform aktualisiert. Weitere Informationen über [Batch-Exporte](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

### Beim Ziel authentifizieren {#authenticate}

[!DNL The Trade Desk] CRM-Ziel ist ein täglicher Batch-Datei-Upload und erfordert keine Authentifizierung durch den Benutzer.

### Ausfüllen der Zieldetails {#fill-in-details}

Bevor Sie Zielgruppendaten an ein Ziel senden oder aktivieren können, müssen Sie eine Verbindung zu Ihrer eigenen Zielplattform einrichten. Beim [Einrichten](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=de) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Account Type]**: Bitte wählen Sie die **[!UICONTROL Existing Account]** Option.
* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Advertiser ID]**: Ihr [!DNL Trade Desk Advertiser ID], das entweder von Ihrem [!DNL Trade Desk] Account Manager freigegeben werden kann oder unter [!DNL Advertiser Preferences] in der [!DNL Trade Desk]-Benutzeroberfläche zu finden ist.

Screenshot der ![Experience Platform-Benutzeroberfläche mit Informationen zum Ausfüllen der Zieldetails.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Beim Herstellen einer Verbindung zum Ziel ist das Festlegen einer Data Governance-Richtlinie vollständig optional. Weitere Einzelheiten finden Sie in der [ zu Experience Platform ](/help/data-governance/policies/overview.md)Übersicht zu Data Governance).

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [ Aktivieren von Zielgruppen für ein Ziel finden Sie ](/help/destinations/ui/activate-batch-profile-destinations.md)Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele“.

Auf der Seite **[!UICONTROL Scheduling]** können Sie den Zeitplan und die Dateinamen für jede Audience konfigurieren, die Sie exportieren. Die Konfiguration des Zeitplans ist obligatorisch, die Konfiguration des Dateinamens ist jedoch optional.

Screenshot der ![Experience Platform-Benutzeroberfläche zum Planen der Zielgruppenaktivierung.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Alle für [!DNL The Trade Desk] CRM-Ziel aktivierten Zielgruppen werden automatisch auf eine tägliche Häufigkeit und einen vollständigen Dateiexport festgelegt.

Screenshot der ![Experience Platform-Benutzeroberfläche zum Planen der Zielgruppenaktivierung.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Auf der Seite **[!UICONTROL Mapping]** müssen Sie Attribute oder Identity-Namespaces aus der Quellspalte auswählen und der Zielspalte zuordnen.

Screenshot der ![Experience Platform-Benutzeroberfläche zur Zuordnung der Zielgruppenaktivierung.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Nachfolgend finden Sie ein Beispiel für die korrekte Identitätszuordnung beim Aktivieren von Zielgruppen für [!DNL The Trade Desk] CRM-Ziel.

Auswahl der Quell- und Zielfelder

| Quellfeld | Zielfeld |
|---|---|
| E-Mail | email |
| Email_LC_SHA256 | hashed_email |
| Telefon (E.164) | phone |
| Phone (SHA256_E.164) | hashed_phone |
| TDID | TDID |
| GAID | DAID |
| IDFA | Idfa |
| UID2 | uid2 |
| UID2Token | uid2_token |
| EUID | EUID |
| EUIDToken | EUID_TOKEN |
| RampID | Inaktiv |
| ID5 | ID5 |
| netID | net_id |
| FirstID | first_id |


## Datenexport validieren {#validate}

Um zu überprüfen, ob die Daten korrekt aus Experience Platform in [!DNL The Trade Desk] exportiert wurden, durchsuchen Sie die Zielgruppen auf der Registerkarte Adobe 1PD in [!DNL The Trade Desk] Bibliothek „Advertiser-Daten und -Identität“. Im Folgenden finden Sie die Schritte zum Auffinden der entsprechenden ID in der [!DNL Trade Desk]-Benutzeroberfläche:

1. Wählen Sie zunächst die Registerkarte **[!UICONTROL Libraries]** aus und lesen Sie den Abschnitt **[!UICONTROL Advertiser data and identity]** .
2. Klicken Sie auf das **[!UICONTROL Adobe 1PD]**, und es werden alle für die [!DNL The Trade Desk] aktivierten Zielgruppen aufgelistet.
3. Der Segmentname oder die Segment-ID aus Experience Platform wird als Segmentname in der [!DNL Trade Desk] Benutzeroberfläche angezeigt.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).
