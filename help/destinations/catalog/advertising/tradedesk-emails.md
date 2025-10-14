---
title: The Trade Desk - CRM-Verbindung
description: Profile für Ihr Trade Desk-Konto aktivieren, um Zielgruppen-Targeting und -Unterdrückung auf der Grundlage von CRM-Daten durchzuführen.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 17%

---

# Die [!DNL Trade Desk] - CRM-Verbindung

>[!IMPORTANT]
>
>Mit Veröffentlichung der EUID (European Unified ID) sehen Sie jetzt zwei [!DNL The Trade Desk - CRM]-Ziele im [Zielkatalog](/help/destinations/catalog/overview.md).
>* Wenn Sie Daten in der EU beziehen, verwenden Sie bitte das **[!DNL The Trade Desk - CRM (EU)]**-Ziel.
>* Wenn Sie Daten in der APAC- oder NAMER-Region beziehen, verwenden Sie das **[!DNL The Trade Desk - CRM (NAMER & APAC)]**-Ziel.
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden vom *[!DNL Trade Desk]*-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte an Ihren [!DNL Trade Desk].

## Überblick {#overview}

Erfahren Sie, wie Sie Profile in Ihrem [!DNL Trade Desk]-Konto aktivieren können, um Zielgruppen-Targeting und -Unterdrückung auf der Grundlage von CRM-Daten durchzuführen.

Dieser Connector sendet Daten an den [!DNL The Trade Desk] Erstanbieter-Endpunkt. Die Integration zwischen Adobe Experience Platform und [!DNL The Trade Desk] unterstützt nicht den Export von Daten an den [!DNL The Trade Desk] Drittanbieterendpunkt.

[!DNL The Trade Desk(TTD)] verarbeitet die Upload-Datei mit E-Mail-Adressen zu keinem Zeitpunkt direkt und speichert [!DNL The Trade Desk] Ihre rohen (ungehashten) E-Mails.

>[!TIP]
>
>Verwenden Sie [!DNL The Trade Desk] CRM-Ziele für die CRM-Datenzuordnung, z. B. E-Mail oder gehashte E-Mail-Adresse. Verwenden Sie das [andere Trade Desk-Ziel](/help/destinations/catalog/advertising/tradedesk.md) im Adobe Experience Platform-Katalog für Cookies und Geräte-ID-Zuordnungen.

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
>Bevor Sie Zielgruppen für das Trade Desk aktivieren können, müssen Sie sich an Ihren [!DNL Trade Desk] Account Manager wenden, um den CRM-Onboarding-Vertrag zu unterzeichnen. [!DNL The Trade Desk] aktivieren die Verwendung von UID2/EUID und geben andere Details weiter, um Sie bei der Konfiguration Ihres Ziels zu unterstützen.

## Anforderungen für den ID-Abgleich {#id-matching-requirements}

Je nach Typ der IDs, die Sie in Adobe Experience Platform aufnehmen, müssen Sie die entsprechenden Anforderungen erfüllen. Weitere Informationen finden Sie [&#x200B; „Übersicht &#x200B;](/help/identity-service/features/namespaces.md) Identitäts-Namespaces“.

## Unterstützte Identitäten {#supported-identities}

[!DNL The Trade Desk] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt Anforderungen an den ID-Abgleich und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mail-Adressen.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | E-Mail-Adressen (Klartext) | Geben Sie `email` als Zielidentität ein, wenn Ihre Quellidentität ein E-Mail-Namespace oder -Attribut ist. |
| Email_LC_SHA256 | E-Mail-Adressen müssen mit SHA256 in Kleinbuchstaben gehasht werden. Sie können diese Einstellung später nicht mehr ändern. | Geben Sie `hashed_email` als Zielidentität ein, wenn Ihre Quellidentität ein Email_LC_SHA256-Namespace oder -Attribut ist. |

{style="table-layout:auto"}

## Hash-Anforderungen für E-Mails {#hashing-requirements}

Sie können E-Mail-Adressen hashen, bevor Sie sie in Adobe Experience Platform aufnehmen, oder rohe E-Mail-Adressen verwenden.

Weitere Informationen zum Aufnehmen von E-Mail-Adressen in Experience Platform finden Sie unter [Übersicht über die Batch-Aufnahme](/help/ingestion/batch-ingestion/overview.md).

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hashen, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

* Leerzeichen am Anfang und Ende entfernen.
* Wandeln Sie alle ASCII-Zeichen in Kleinbuchstaben um.
* Entfernen Sie in `gmail.com` E-Mail-Adressen die folgenden Zeichen aus dem Teil Benutzername der E-Mail-Adresse:
   * Der Zeitraum (. (ASCII-Code 46). Normalisieren Sie beispielsweise `jane.doe@gmail.com` auf `janedoe@gmail.com`.
   * Das Pluszeichen (+ (ASCII-Code 43)) und alle nachfolgenden Zeichen. Normalisieren Sie beispielsweise `janedoe+home@gmail.com` auf `janedoe@gmail.com`.

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Audience mit den IDs (E-Mail oder Hash-E-Mail), die im Trade Desk-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Täglicher Batch]** | Da ein Profil in Experience Platform auf der Grundlage einer Zielgruppenbewertung aktualisiert wird, werden die Profile (Identitäten) einmal täglich nachgelagert auf der Zielplattform aktualisiert. Weitere Informationen über [Batch-Exporte](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

### Beim Ziel authentifizieren {#authenticate}

[!DNL The Trade Desk] CRM-Ziel ist ein täglicher Batch-Datei-Upload und erfordert keine Authentifizierung durch den Benutzer.

### Ausfüllen der Zieldetails {#fill-in-details}

Bevor Sie Zielgruppendaten an ein Ziel senden oder aktivieren können, müssen Sie eine Verbindung zu Ihrer eigenen Zielplattform einrichten. Beim [Einrichten](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=de) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Kontotyp]**: Wählen Sie die Option **[!UICONTROL Vorhandenes Konto]** aus.
* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Advertiser-ID]**: Ihr [!DNL Trade Desk Advertiser ID], das entweder von Ihrem [!DNL Trade Desk] Account Manager freigegeben werden kann oder unter [!DNL Advertiser Preferences] in der [!DNL Trade Desk]-Benutzeroberfläche zu finden ist.

Screenshot der ![Experience Platform-Benutzeroberfläche mit Informationen zum Ausfüllen der Zieldetails.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Beim Herstellen einer Verbindung zum Ziel ist das Festlegen einer Data Governance-Richtlinie vollständig optional. Weitere Einzelheiten finden Sie in der [&#x200B; zu Experience Platform &#x200B;](/help/data-governance/policies/overview.md)Übersicht zu Data Governance).

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [&#x200B; Aktivieren von Zielgruppen für ein Ziel finden Sie &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md)Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele“.

Auf der **[!UICONTROL Planung]** können Sie den Zeitplan und die Dateinamen für jede Audience konfigurieren, die Sie exportieren. Die Konfiguration des Zeitplans ist obligatorisch, die Konfiguration des Dateinamens ist jedoch optional.

Screenshot der ![Experience Platform-Benutzeroberfläche zum Planen der Zielgruppenaktivierung.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Alle für [!DNL The Trade Desk] CRM-Ziel aktivierten Zielgruppen werden automatisch auf eine tägliche Häufigkeit und einen vollständigen Dateiexport festgelegt.

Screenshot der ![Experience Platform-Benutzeroberfläche zum Planen der Zielgruppenaktivierung.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Auf der **[!UICONTROL Zuordnung]** müssen Sie Attribute oder Identity-Namespaces aus der Quellspalte auswählen und der Zielspalte zuordnen.

Screenshot der ![Experience Platform-Benutzeroberfläche zur Zuordnung der Zielgruppenaktivierung.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Nachfolgend finden Sie ein Beispiel für die korrekte Identitätszuordnung beim Aktivieren von Zielgruppen für [!DNL The Trade Desk] CRM-Ziel.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM-Ziel akzeptiert keine rohen und gehashten E-Mail-Adressen als Identitäten im selben Aktivierungsfluss. Separate Aktivierungsflüsse für unbearbeitete und gehashte E-Mail-Adressen erstellen.

Auswahl der Quellfelder:

* Wählen Sie den `Email` Namespace oder das Attribut als Quellidentität aus, wenn Sie die rohe E-Mail-Adresse bei der Datenaufnahme verwenden.
* Wählen Sie den `Email_LC_SHA256` Namespace oder das Attribut als Quellidentität aus, wenn Sie bei der Datenaufnahme in Experience Platform die E-Mail-Adressen von Kunden gehasht haben.

Auswählen der Zielfelder:

* Geben Sie `email` als Zielidentität ein, wenn Ihr Quell-Namespace oder -Attribut `Email` ist.
* Geben Sie `hashed_email` als Zielidentität ein, wenn Ihr Quell-Namespace oder -Attribut `Email_LC_SHA256` ist.

## Datenexport validieren {#validate}

Um zu überprüfen, ob die Daten korrekt aus Experience Platform in [!DNL The Trade Desk] exportiert werden, durchsuchen Sie die Zielgruppen unter der Adobe 1PD-Datenkachel in [!DNL The Trade Desk] Data Management Platform (DMP). Im Folgenden finden Sie die Schritte zum Auffinden der entsprechenden ID in der [!DNL Trade Desk]-Benutzeroberfläche:

1. Wählen Sie zunächst die Registerkarte **[!UICONTROL Daten]** und lesen Sie den Abschnitt **[!UICONTROL Erstanbieter]**.
2. Scrollen Sie auf der Seite nach unten **[!UICONTROL Importierte Daten]** finden Sie die **[!UICONTROL Adobe 1PD-Kachel]**.
3. Klicken Sie auf die Kachel **[!UICONTROL Adobe 1PD]**. Dort werden alle Zielgruppen aufgelistet, die für das [!DNL Trade Desk]-Ziel Ihres Advertisers aktiviert sind. Sie können auch die Suchfunktion verwenden.
4. Die Segment-ID # aus Experience Platform wird als Segmentname in der [!DNL Trade Desk] Benutzeroberfläche angezeigt.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).
