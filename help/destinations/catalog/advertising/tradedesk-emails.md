---
title: (Beta) Verbindung zwischen Trade Desk und CRM
description: Aktivieren Sie Profile in Ihrem Trade Desk-Konto für Zielgruppen-Targeting und -Unterdrückung basierend auf CRM-Daten.
source-git-commit: 69bf43f86ab3369ad0c7febcb69ec41d3bcac8bb
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 10%

---


# (Beta) Die [!DNL Trade Desk] - CRM-Verbindung

>[!IMPORTANT]
>
> [!DNL The Trade Desk - CRM] Das Ziel in Platform befindet sich derzeit in der Beta-Phase. Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

>[!IMPORTANT]
>
> Diese Dokumentationsseite wurde von der *[!DNL Trade Desk]* Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte an Ihre [!DNL Trade Desk] Vertreter.

Dieses Dokument soll Ihnen helfen, Profile für Ihre [!DNL Trade Desk] Zielgruppen-Targeting und -Unterdrückung anhand von CRM-Daten.

>[!TIP]
>
>Verwendung [!DNL The Trade Desk] CRM-Ziel für das CRM-Daten-Mapping, z. B. E-Mail- oder Hash-E-Mail-Adresse. Verwenden Sie die [anderes Handelszentrum-Ziel](/help/destinations/catalog/advertising/tradedesk.md) im Adobe Experience Platform-Katalog für Cookies und Geräte-ID-Zuordnungen.

[!DNL The Trade Desk] (TTD) verarbeitet die Upload-Datei von E-Mail-Adressen zu keinem Zeitpunkt direkt und [!DNL The Trade Desk] Speichern Sie Ihre ungehashten E-Mails.

## Voraussetzungen {#prerequisites}

Bevor Sie Segmente aktivieren können, um [!DNL The Trade Desk]müssen Sie Ihre [!DNL The Trade Desk] Kundenbetreuer zur Unterzeichnung des CRM-Onboarding-Vertrags. [!DNL The Trade Desk] gibt dann die Erlaubnis und gibt Ihre Advertiser-ID frei, um Ihr Ziel zu konfigurieren.

## Anforderungen an die ID-Übereinstimmung (#id-match-requirements)

Je nach der Art der IDs, die Sie in Adobe Experience Platform erfassen, müssen Sie die entsprechenden Anforderungen erfüllen. Bitte lesen Sie die [Übersicht über Identity Namespace](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de) für weitere Informationen.

## Unterstützte Identitäten {#supported-identities}

[!DNL The Trade Desk] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Weitere Informationen [identities](/help/identity-service/namespaces.md).

Sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt Anforderungen für die ID-Zuordnung und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mail-Adressen.

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | E-Mail-Adressen (Klartext) | Wählen Sie die `Email` Zielidentität, wenn Ihre Quellidentität ein E-Mail-Namespace oder -Attribut ist. |
| Email_LC_SHA256 | E-Mail-Adressen müssen mit SHA256 gehasht und in Kleinbuchstaben geschrieben werden. Achten Sie darauf, [E-Mail-Normalisierung](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) Regeln erforderlich. Sie können diese Einstellung später nicht ändern. | Wählen Sie die `Email_LC_SHA256` Zielidentität, wenn Ihre Quellidentität ein Namespace oder ein Attribut vom Typ E-Mail_LC_SHA256 ist. |

{style=&quot;table-layout:auto&quot;}

## Anforderungen an das E-Mail-Hashing (#hashing-requirements)

Sie können E-Mail-Adressen hashen, bevor Sie sie in Adobe Experience Platform aufnehmen, oder Sie können E-Mail-Adressen als Rohdaten verwenden.

Informationen zur Aufnahme von E-Mail-Adressen in Experience Platform finden Sie in der [Batch-Erfassung - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en).

Wenn Sie die E-Mail-Adressen selbst hash möchten, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

* Entfernen Sie Leerzeichen am Anfang und am Ende.
* Konvertieren Sie alle ASCII-Zeichen in Kleinbuchstaben.
* In `gmail.com` E-Mail-Adressen die folgenden Zeichen aus dem Benutzernamen-Teil der E-Mail-Adresse entfernen:
   * Der Punkt (. (ASCII-Code 46). Beispiel: normalisieren `jane.doe@gmail.com` nach `janedoe@gmail.com`.
   * Das Pluszeichen (+ (ASCII-Code 43)) und alle nachfolgenden Zeichen. Beispiel: normalisieren `janedoe+home@gmail.com` nach `janedoe@gmail.com`.

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (E-Mail oder Hash-E-Mail), die im Trade Desk-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Täglicher Batch]** | Da ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, wird das Profil (die Identitäten) einmal täglich nachgelagert zur Zielplattform aktualisiert. Mehr dazu [Batch-Uploads](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en#file-based). |

{style=&quot;table-layout:auto&quot;}

## Herstellen einer Verbindung mit der Datenbank {#connect}

### Bei Ziel authentifizieren (#authenticate)

[!DNL The Trade Desk] Das CRM-Ziel ist ein täglicher Batch-Datei-Upload und erfordert keine Authentifizierung durch den Benutzer.

### Füllen Sie Zieldetails aus (#fill-in-details)

Bevor Sie Zielgruppendaten an ein Ziel senden oder aktivieren können, müssen Sie eine Verbindung zu Ihrer eigenen Zielplattform herstellen. Beim [Einrichten](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Kontotyp]**: Bitte wählen Sie die **[!UICONTROL Vorhandenes Konto]** -Option.
* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Advertiser-ID]**: Ihre [!DNL Trade Desk Advertiser ID], die entweder von Ihrer [!DNL Trade Desk] Kundenbetreuer oder finden Sie unter [!DNL Advertiser Preferences] im [!DNL Trade Desk] Benutzeroberfläche.

Beim Herstellen einer Verbindung zum Ziel ist das Festlegen einer Data Governance-Richtlinie vollständig optional. Lesen Sie die Experience Platform [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=en) für weitere Details.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=de) für Anweisungen zum Aktivieren von Zielgruppensegmenten für ein Ziel.

Auf der Seite **[!UICONTROL Planung]** können Sie den Zeitplan und die Dateinamen für jedes Segment konfigurieren, das Sie exportieren. Die Konfiguration des Zeitplans ist obligatorisch, die Konfiguration des Dateinamens ist jedoch optional.

>[!NOTE]
>
>Alle Segmente, die für aktiviert sind [!DNL The Trade Desk] Das CRM-Ziel wird automatisch auf eine tägliche Häufigkeit und einen vollständigen Dateiexport eingestellt.

Im **[!UICONTROL Zuordnung]** -Seite, müssen Sie Attribute oder Identitäts-Namespaces aus der Quellspalte auswählen und der Zielspalte zuordnen.

Nachstehend finden Sie ein Beispiel für die korrekte Identitätszuordnung bei der Aktivierung von Segmenten für [!DNL The Trade Desk] CRM-Ziel.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM-Ziel akzeptiert keine rohen und Hash-E-Mail-Adressen als Identitäten im selben Aktivierungsfluss. Erstellen Sie separate Aktivierungsflüsse für Roh- und Hash-E-Mail-Adressen.

Auswählen von Quellfeldern:

* Wählen Sie die `Email` Namespace oder Attribut als Quellidentität verwenden, wenn die E-Mail-Adresse bei der Datenerfassung verwendet wird.
* Wählen Sie die `Email_LC_SHA256` -Namespace oder -Attribut als Quellidentität verwenden, wenn Sie bei der Datenerfassung in Platform einen Hash für E-Mail-Adressen von Kunden durchführen.

Zielgruppenfelder auswählen:

* Wählen Sie die `Email` Namespace als Zielidentität, wenn Ihr Quell-Namespace oder -Attribut `Email`.
* Wählen Sie die `Email_LC_SHA256` Namespace als Zielidentität, wenn Ihr Quell-Namespace oder -Attribut `Email_LC_SHA256`.

## Datenexport überprüfen (#validate)

Überprüfen, ob die Daten ordnungsgemäß aus der Experience Platform in [!DNL The Trade Desk]finden Sie die Segmente unter der Datenkachel Adobe 1PD in [!DNL The Trade Desk] Data Management Platform (DMP). Im Folgenden finden Sie die Schritte zum Auffinden der entsprechenden ID im [!DNL Trade Desk] Benutzeroberfläche:

1. Klicken Sie zunächst auf die **[!UICONTROL Daten]** Registerkarte und Überprüfung **[!UICONTROL Erstanbieter]**.
2. Scrollen Sie nach unten, unter **[!UICONTROL Importierte Daten]** finden Sie **[!UICONTROL Adobe 1PD-Kachel]**.
3. Klicken Sie auf die Schaltfläche **[!UICONTROL Adobe 1PD]** -Kachel und listet alle Segmente auf, die für die [!DNL Trade Desk] Ziel für Ihren Advertiser. Sie können auch die Suchfunktion verwenden.
4. Die Segment-ID-Nummer aus der Experience Platform wird als Segmentname in der [!DNL Trade Desk] Benutzeroberfläche.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](/help/data-governance/home.md).
