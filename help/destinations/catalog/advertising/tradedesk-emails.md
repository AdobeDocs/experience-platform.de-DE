---
title: (Beta) Verbindung zwischen Trade Desk und CRM
description: Aktivieren Sie Profile in Ihrem Trade Desk-Konto für Zielgruppen-Targeting und -Unterdrückung basierend auf CRM-Daten.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 3c645ccf5b9dd17e4c3cc1267b60a9c4f1131668
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 18%

---

# (Beta) Die Verbindung [!DNL Trade Desk] - CRM

>[!IMPORTANT]
>
>Das Ziel für [!DNL The Trade Desk - CRM] in Platform befindet sich derzeit in der Beta-Phase. Dokumentation und Funktionalitäten können sich ändern.
>
>Mit Veröffentlichung der EUID (European Unified ID) sehen Sie jetzt zwei [!DNL The Trade Desk - CRM]-Ziele im [Zielkatalog](/help/destinations/catalog/overview.md).
>* Wenn Sie Daten in der EU beziehen, verwenden Sie bitte das **[!DNL The Trade Desk - CRM (EU)]**-Ziel.
>* Wenn Sie Daten in der APAC- oder NAMER-Region beziehen, verwenden Sie das **[!DNL The Trade Desk - CRM (NAMER & APAC)]**-Ziel.
>
>Beide Ziele in Experience Platform befinden sich derzeit in der Beta-Phase. Diese Ziel-Connector- und Dokumentationsseite werden vom *[!DNL Trade Desk]*-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte an Ihren [!DNL Trade Desk]-Support-Mitarbeiter. Die Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

Dieses Dokument soll Ihnen dabei helfen, Profile für Ihr [!DNL Trade Desk] -Konto zu aktivieren, um Zielgruppen-Targeting und -Unterdrückung auf der Basis von CRM-Daten zu ermöglichen.

Dieser Connector sendet Daten an den Erstanbieter-Endpunkt [!DNL The Trade Desk]. Die Integration zwischen Adobe Experience Platform und [!DNL The Trade Desk] unterstützt nicht den Export von Daten in den Drittanbieter-Endpunkt [!DNL The Trade Desk].

[!DNL The Trade Desk(TTD)] verarbeitet die Upload-Datei von E-Mail-Adressen zu keinem Zeitpunkt direkt und [!DNL The Trade Desk] speichert Ihre rohen (ungehashten) E-Mails nicht.

>[!TIP]
>
>Verwenden Sie [!DNL The Trade Desk] CRM-Ziele für die CRM-Datenzuordnung, z. B. E-Mail- oder Hash-E-Mail-Adresse. Verwenden Sie für Cookies und Geräte-ID-Zuordnungen das [andere Handelsvertretungs-Ziel](/help/destinations/catalog/advertising/tradedesk.md) im Adobe Experience Platform-Katalog.

## Voraussetzungen {#prerequisites}

Bevor Sie Zielgruppen für [!DNL The Trade Desk] aktivieren können, müssen Sie sich an Ihren [!DNL The Trade Desk] Kundenbetreuer wenden, um den CRM-Onboarding-Vertrag zu unterzeichnen. [!DNL The Trade Desk] gibt dann die Berechtigung und gibt Ihre Advertiser-ID frei, um Ihr Ziel zu konfigurieren.

## Anforderungen an die ID-Übereinstimmung {#id-matching-requirements}

Abhängig vom Typ der IDs, die Sie in Adobe Experience Platform erfassen, müssen Sie die entsprechenden Anforderungen erfüllen. Weitere Informationen finden Sie in der [Übersicht zum Identity-Namespace](/help/identity-service/features/namespaces.md) .

## Unterstützte Identitäten {#supported-identities}

[!DNL The Trade Desk] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt Anforderungen für die ID-Zuordnung und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mail-Adressen.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | E-Mail-Adressen (Klartext) | Geben Sie `email` als Zielidentität ein, wenn Ihre Quellidentität ein E-Mail-Namespace oder -Attribut ist. |
| Email_LC_SHA256 | E-Mail-Adressen müssen mit SHA256 gehasht und in Kleinbuchstaben geschrieben werden. Sie können diese Einstellung später nicht ändern. | Geben Sie `hashed_email` als Zielidentität ein, wenn Ihre Quellidentität ein Namespace oder Attribut E-Mail_LC_SHA256 ist. |

{style="table-layout:auto"}

## Anforderungen an das E-Mail-Hashing {#hashing-requirements}

Sie können E-Mail-Adressen hashen, bevor Sie sie in Adobe Experience Platform aufnehmen, oder Sie können E-Mail-Adressen als Rohdaten verwenden.

Weiterführende Informationen zur Aufnahme von E-Mail-Adressen in Experience Platform finden Sie in der [Batch-Erfassungsübersicht](/help/ingestion/batch-ingestion/overview.md).

Wenn Sie die E-Mail-Adressen selbst hash möchten, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

* Entfernen Sie Leerzeichen am Anfang und am Ende.
* Konvertieren Sie alle ASCII-Zeichen in Kleinbuchstaben.
* Entfernen Sie in `gmail.com` E-Mail-Adressen die folgenden Zeichen aus dem Benutzernamen-Teil der E-Mail-Adresse:
   * Der Punkt (. (ASCII-Code 46). Normalisieren Sie beispielsweise `jane.doe@gmail.com` auf `janedoe@gmail.com`.
   * Das Pluszeichen (+ (ASCII-Code 43)) und alle nachfolgenden Zeichen. Normalisieren Sie beispielsweise `janedoe+home@gmail.com` auf `janedoe@gmail.com`.

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (E-Mail oder Hash-E-Mail), die im Trade Desk-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Täglicher Batch]** | Wenn ein Profil auf der Grundlage einer Zielgruppenbewertung im Experience Platform aktualisiert wird, wird das Profil (die Identitäten) einmal täglich nachgelagert zur Zielplattform aktualisiert. Weitere Informationen zu [Batch-Exporten](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

### Auf Ziel authentifizieren {#authenticate}

[!DNL The Trade Desk] CRM-Ziel ist ein täglicher Batch-Datei-Upload und erfordert keine Authentifizierung durch den Benutzer.

### Zieldetails ausfüllen {#fill-in-details}

Bevor Sie Zielgruppendaten an ein Ziel senden oder aktivieren können, müssen Sie eine Verbindung zu Ihrer eigenen Zielplattform herstellen. Beim [Einrichten](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=de) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Kontotyp]**: Wählen Sie die Option **[!UICONTROL Vorhandenes Konto]** aus.
* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Advertiser-ID]**: Ihre [!DNL Trade Desk Advertiser ID], die entweder von Ihrem [!DNL Trade Desk]-Kundenbetreuer oder unter [!DNL Advertiser Preferences] in der [!DNL Trade Desk] -Benutzeroberfläche freigegeben werden kann.

![Screenshot der Platform-Benutzeroberfläche, der zeigt, wie Zieldetails ausgefüllt werden.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Beim Herstellen einer Verbindung zum Ziel ist das Festlegen einer Data Governance-Richtlinie vollständig optional. Weitere Informationen finden Sie unter Experience Platform [Data Governance - Übersicht](/help/data-governance/policies/overview.md) .

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für ein Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profilexportziele](/help/destinations/ui/activate-batch-profile-destinations.md) .

Auf der Seite **[!UICONTROL Planung]** können Sie den Zeitplan und die Dateinamen für jede Zielgruppe konfigurieren, die Sie exportieren. Die Konfiguration des Zeitplans ist obligatorisch, die Konfiguration des Dateinamens ist jedoch optional.

![Screenshot der Platform-Benutzeroberfläche zur Planung der Aktivierung der Zielgruppe.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Alle für das CRM-Ziel [!DNL The Trade Desk] aktivierten Zielgruppen werden automatisch auf eine tägliche Häufigkeit und einen vollständigen Dateiexport eingestellt.

![Screenshot der Platform-Benutzeroberfläche zur Planung der Aktivierung der Zielgruppe.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Auf der Seite **[!UICONTROL Zuordnung]** müssen Sie Attribute oder Identitäts-Namespaces aus der Quellspalte auswählen und der Zielspalte zuordnen.

![Screenshot der Platform-Benutzeroberfläche zur Zuordnung der Zielgruppenaktivierung.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Nachstehend finden Sie ein Beispiel für die korrekte Identitätszuordnung bei der Aktivierung von Zielgruppen für das CRM-Ziel [!DNL The Trade Desk] .

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM-Ziel akzeptiert keine rohen und gehashten E-Mail-Adressen als Identitäten im selben Aktivierungsfluss. Erstellen Sie separate Aktivierungsflüsse für Roh- und Hash-E-Mail-Adressen.

Quellfelder auswählen:

* Wählen Sie den Namespace oder das Attribut `Email` als Quellidentität aus, wenn Sie die E-Mail-Adresse bei der Datenerfassung als Rohdaten verwenden.
* Wählen Sie den Namespace oder das Attribut `Email_LC_SHA256` als Quellidentität aus, wenn Sie bei der Datenerfassung in Platform E-Mail-Adressen von Kunden gehasht haben.

Zielgruppenfelder auswählen:

* Geben Sie `email` als Zielidentität ein, wenn Ihr Quellnamespace oder -attribut `Email` ist.
* Geben Sie `hashed_email` als Zielidentität ein, wenn Ihr Quellnamespace oder -attribut `Email_LC_SHA256` ist.

## Datenexport überprüfen {#validate}

Um zu überprüfen, ob Daten ordnungsgemäß aus dem Experience Platform in [!DNL The Trade Desk] exportiert wurden, suchen Sie die Zielgruppen in der Datenkachel Adobe 1PD in [!DNL The Trade Desk] Data Management Platform (DMP). Im Folgenden finden Sie die Schritte zum Auffinden der entsprechenden ID in der Benutzeroberfläche von [!DNL Trade Desk]:

1. Wählen Sie zunächst die Registerkarte **[!UICONTROL Daten]** aus und überprüfen Sie den Abschnitt **[!UICONTROL Erstanbieter]** .
2. Scrollen Sie auf der Seite nach unten, unter **[!UICONTROL Importierte Daten]**, finden Sie die Kachel **[!UICONTROL Adobe 1PD]**.
3. Klicken Sie auf die Kachel **[!UICONTROL Adobe 1PD]** und listet alle Zielgruppen auf, die für das Ziel [!DNL Trade Desk] Ihres Advertisers aktiviert sind. Sie können auch die Suchfunktion verwenden.
4. Die Segment-ID-Nummer von Experience Platform wird als Segmentname in der Benutzeroberfläche von [!DNL Trade Desk] angezeigt.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).
