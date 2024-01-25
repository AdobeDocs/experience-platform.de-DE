---
title: (Beta) Verbindung zwischen Trade Desk und CRM
description: Aktivieren Sie Profile in Ihrem Trade Desk-Konto für Zielgruppen-Targeting und -Unterdrückung basierend auf CRM-Daten.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 18%

---

# (Beta) Die [!DNL Trade Desk] - CRM-Verbindung

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] Das Ziel in Platform befindet sich derzeit in der Beta-Phase. Dokumentation und Funktionalitäten können sich ändern.
>
>Mit Veröffentlichung der EUID (European Unified ID) sehen Sie jetzt zwei [!DNL The Trade Desk - CRM]-Ziele im [Zielkatalog](/help/destinations/catalog/overview.md).
>* Wenn Sie Daten in der EU beziehen, verwenden Sie bitte das **[!DNL The Trade Desk - CRM (EU)]**-Ziel.
>* Wenn Sie Daten in der APAC- oder NAMER-Region beziehen, verwenden Sie das **[!DNL The Trade Desk - CRM (NAMER & APAC)]**-Ziel.
>
>Beide Ziele in Experience Platform befinden sich derzeit in der Beta-Phase. Diese Ziel-Connector- und Dokumentationsseite wird von der *[!DNL Trade Desk]* Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte an Ihre [!DNL Trade Desk] -Support-Mitarbeiter, können sich die Dokumentation und Funktionalität ändern.

## Übersicht {#overview}

Dieses Dokument soll Ihnen helfen, Profile für Ihre [!DNL Trade Desk] Zielgruppen-Targeting und -Unterdrückung anhand von CRM-Daten.

[!DNL The Trade Desk(TTD)] verarbeitet die Upload-Datei von E-Mail-Adressen zu keinem Zeitpunkt direkt, noch [!DNL The Trade Desk] Speichern Sie Ihre ungehashten E-Mails.

>[!TIP]
>
>Verwendung [!DNL The Trade Desk] CRM-Ziele für das CRM-Daten-Mapping, z. B. E-Mail- oder Hash-E-Mail-Adresse. Verwenden Sie die [anderes Handelszentrum-Ziel](/help/destinations/catalog/advertising/tradedesk.md) im Adobe Experience Platform-Katalog für Cookies und Geräte-ID-Zuordnungen.

## Voraussetzungen {#prerequisites}

Vor der Aktivierung von Zielgruppen in [!DNL The Trade Desk]müssen Sie Ihre [!DNL The Trade Desk] Kundenbetreuer zur Unterzeichnung des CRM-Onboarding-Vertrags. [!DNL The Trade Desk] gibt dann die Erlaubnis und gibt Ihre Advertiser-ID frei, um Ihr Ziel zu konfigurieren.

## Anforderungen an die ID-Übereinstimmung {#id-matching-requirements}

Je nach der Art der IDs, die Sie in Adobe Experience Platform erfassen, müssen Sie die entsprechenden Anforderungen erfüllen. Bitte lesen Sie die [Übersicht über Identity Namespace](/help/identity-service/features/namespaces.md) für weitere Informationen.

## Unterstützte Identitäten {#supported-identities}

[!DNL The Trade Desk] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt Anforderungen für die ID-Zuordnung und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mail-Adressen.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | E-Mail-Adressen (Klartext) | Eingabe `email` als Zielidentität, wenn Ihre Quellidentität ein E-Mail-Namespace oder -Attribut ist. |
| Email_LC_SHA256 | E-Mail-Adressen müssen mit SHA256 gehasht und in Kleinbuchstaben geschrieben werden. Sie können diese Einstellung später nicht ändern. | Eingabe `hashed_email` als Zielidentität, wenn Ihre Quellidentität ein Namespace oder ein Attribut von Email_LC_SHA256 ist. |

{style="table-layout:auto"}

## Anforderungen an das E-Mail-Hashing {#hashing-requirements}

Sie können E-Mail-Adressen hashen, bevor Sie sie in Adobe Experience Platform aufnehmen, oder Sie können E-Mail-Adressen als Rohdaten verwenden.

Informationen zur Aufnahme von E-Mail-Adressen in Experience Platform finden Sie im Abschnitt [Batch-Erfassung - Übersicht](/help/ingestion/batch-ingestion/overview.md).

Wenn Sie die E-Mail-Adressen selbst hash möchten, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

* Entfernen Sie Leerzeichen am Anfang und am Ende.
* Konvertieren Sie alle ASCII-Zeichen in Kleinbuchstaben.
* In `gmail.com` E-Mail-Adressen die folgenden Zeichen aus dem Benutzernamen-Teil der E-Mail-Adresse entfernen:
   * Der Punkt (. (ASCII-Code 46). Beispiel: normalisieren `jane.doe@gmail.com` nach `janedoe@gmail.com`.
   * Das Pluszeichen (+ (ASCII-Code 43)) und alle nachfolgenden Zeichen. Beispiel: normalisieren `janedoe+home@gmail.com` nach `janedoe@gmail.com`.

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (E-Mail oder Hash-E-Mail), die im Trade Desk-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Täglicher Batch]** | Wenn ein Profil auf der Grundlage einer Zielgruppenbewertung im Experience Platform aktualisiert wird, wird das Profil (die Identitäten) einmal täglich nachgelagert zur Zielplattform aktualisiert. Mehr dazu [Stapelexporte](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

### Auf Ziel authentifizieren {#authenticate}

[!DNL The Trade Desk] Das CRM-Ziel ist ein täglicher Batch-Datei-Upload und erfordert keine Authentifizierung durch den Benutzer.

### Zieldetails ausfüllen {#fill-in-details}

Bevor Sie Zielgruppendaten an ein Ziel senden oder aktivieren können, müssen Sie eine Verbindung zu Ihrer eigenen Zielplattform herstellen. Beim [Einrichten](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=de) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Kontotyp]**: Bitte wählen Sie die **[!UICONTROL Vorhandenes Konto]** -Option.
* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Advertiser-ID]**: your [!DNL Trade Desk Advertiser ID], die entweder von Ihrer [!DNL Trade Desk] Kundenbetreuer oder finden Sie unter [!DNL Advertiser Preferences] im [!DNL Trade Desk] Benutzeroberfläche.

![Screenshot der Platform-Benutzeroberfläche, in dem gezeigt wird, wie Zieldetails ausgefüllt werden.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Beim Herstellen einer Verbindung zum Ziel ist das Festlegen einer Data Governance-Richtlinie vollständig optional. Lesen Sie die Experience Platform . [Data Governance - Übersicht](/help/data-governance/policies/overview.md) für weitere Details.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Lesen [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für ein Ziel.

Im **[!UICONTROL Planung]** können Sie den Zeitplan und die Dateinamen für jede Zielgruppe konfigurieren, die Sie exportieren. Die Konfiguration des Zeitplans ist obligatorisch, die Konfiguration des Dateinamens ist jedoch optional.

![Screenshot der Platform-Benutzeroberfläche zur Planung der Aktivierung der Zielgruppe.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Alle für aktivierten Zielgruppen [!DNL The Trade Desk] Das CRM-Ziel wird automatisch auf eine tägliche Häufigkeit und einen vollständigen Dateiexport eingestellt.

![Screenshot der Platform-Benutzeroberfläche zur Planung der Aktivierung der Zielgruppe.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Im **[!UICONTROL Zuordnung]** -Seite, müssen Sie Attribute oder Identitäts-Namespaces aus der Quellspalte auswählen und der Zielspalte zuordnen.

![Screenshot der Platform-Benutzeroberfläche zur Zuordnung der Zielgruppenaktivierung.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Nachstehend finden Sie ein Beispiel für die korrekte Identitätszuordnung bei der Aktivierung von Zielgruppen zu [!DNL The Trade Desk] CRM-Ziel.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM-Ziel akzeptiert keine rohen und Hash-E-Mail-Adressen als Identitäten im selben Aktivierungsfluss. Erstellen Sie separate Aktivierungsflüsse für Roh- und Hash-E-Mail-Adressen.

Quellfelder auswählen:

* Wählen Sie die `Email` Namespace oder Attribut als Quellidentität verwenden, wenn die E-Mail-Adresse bei der Datenerfassung verwendet wird.
* Wählen Sie die `Email_LC_SHA256` -Namespace oder -Attribut als Quellidentität verwenden, wenn Sie bei der Datenerfassung in Platform einen Hash für E-Mail-Adressen von Kunden durchführen.

Zielgruppenfelder auswählen:

* Eingabe  `email` als Zielidentität verwenden, wenn Ihr Quell-Namespace oder -Attribut `Email`.
* Eingabe  `hashed_email` als Zielidentität verwenden, wenn Ihr Quell-Namespace oder -Attribut `Email_LC_SHA256`.

## Datenexport überprüfen {#validate}

Überprüfen, ob die Daten von Experience Platform und nach ordnungsgemäß exportiert wurden [!DNL The Trade Desk], finden Sie die Zielgruppen unter der Adobe 1PD-Datenkachel in [!DNL The Trade Desk] Data Management Platform (DMP). Im Folgenden finden Sie die Schritte zum Auffinden der entsprechenden ID im [!DNL Trade Desk] Benutzeroberfläche:

1. Klicken Sie zunächst auf die **[!UICONTROL Daten]** Registerkarte und Überprüfung **[!UICONTROL Erstanbieter]**.
2. Scrollen Sie nach unten, unter **[!UICONTROL Importierte Daten]**, finden Sie **[!UICONTROL Adobe 1PD-Kachel]**.
3. Klicken Sie auf die Schaltfläche **[!UICONTROL Adobe 1PD]Die Kachel ** enthält alle Zielgruppen, die für die [!DNL Trade Desk] Ziel für Ihren Advertiser. Sie können auch die Suchfunktion verwenden.
4. Die Segment-ID-Nummer von Experience Platform wird als Segmentname in der [!DNL Trade Desk] Benutzeroberfläche.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).
