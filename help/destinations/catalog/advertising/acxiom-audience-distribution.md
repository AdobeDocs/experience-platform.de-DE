---
title: Verteilung der Acxiom-Zielgruppe
description: Verwenden Sie das Ziel  [!DNL Acxiom Audience Distribution]  , um Zielgruppen mit der [!DNL Acxiom's Real ID] Technologie zu erweitern und Zielgruppen für mehrere Plattformen zu aktivieren, z. B.  [!DNL Altice],  [!DNL Ampersand],  [!DNL Comcast] und mehr.
badge: Beta
source-git-commit: 7db60161b638cce1845c430f6086441599a0bc61
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 14%

---


# [!DNL Acxiom Audience Distribution] Ziel

>[!NOTE]
>
>Das Ziel [!DNL Acxiom Audience Distribution] befindet sich in der Beta-Phase. Diese Ziel-Connector- und Dokumentationsseite werden vom [!DNL Acxiom]-Team erstellt und gepflegt. Bei Anfragen oder Aktualisierungsanfragen wenden Sie sich direkt an Acxiom [hier](mailto:acxiom-adobe-help@acxiom.com).

Verwenden Sie das Ziel [!DNL Acxiom Audience Distribution] , um Zielgruppen mit der Technologie [!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/) zu erweitern und Zielgruppen für mehrere Plattformen wie [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] und mehr zu aktivieren.

Dieses Tutorial enthält Anweisungen zum Erstellen eines [!DNL Acxiom Audience Distribution] Ziel-Connectors mithilfe der [!DNL Adobe Experience Platform] -Benutzeroberfläche. Dieser Connector wird zum Erstellen und Verteilen von Zielgruppen an ausgewählte Ziele verwendet.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das [!DNL Acxiom Audience Distribution]-Ziel verwenden sollten, finden Sie hier ein Beispielanwendungsbeispiel, das [!DNL Adobe Experience Platform] -Kunden mithilfe dieses Connectors lösen können.

### Senden von Zielgruppen von Experience Platform an Ihr Acxiom-Konto {#send-audiences}

Verwenden Sie diesen Ziel-Connector, wenn Sie ein Marketing-Experte sind, der Zielgruppen von [!DNL Experience Platform] zur kanalübergreifenden Akquise an Ihr [!DNL Acxiom]-Konto senden möchte.

So interessiert sich beispielsweise die Marketingabteilung einer Marke für globale Finanzdienstleistungen für die kanalübergreifende Kundenakquise über mehrere Werbeplattformen. Sie können den Ziel-Connector [!DNL Acxiom Audience Distribution] verwenden, um Zielgruppen von [!DNL Experience Platform] an [!DNL Acxiom] zu senden, die Zielgruppen mit der Technologie [!DNL Acxiom's Real ID] zu erweitern und die Zielgruppen für mehrere Plattformen wie [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] und mehr zu aktivieren.

## Voraussetzungen {#prerequisites}

* **Nutzungsbedingungen bestätigen:** Bevor Sie ein neues [!DNL Acxiom Audience Distribution]-Ziel konfigurieren können, müssen Sie die Nutzungsbedingungen von [!DNL Acxiom's] lesen und unterzeichnen. Sie erhalten den Link zur Vereinbarung, sobald Ihr ausführlicher Auftrag abgeschlossen ist. Bis Sie die Vereinbarung unterzeichnet haben, wird die [!DNL Acxiom Audience Distribution] -Zielkarte im Zielkatalog der Experience Platform nicht angezeigt. Nachdem Sie die Vereinbarung akzeptiert und unterzeichnet haben, schließt [!DNL Adobe] Ihren Onboarding-Prozess ab und Sie sehen die [!DNL Acxiom Audience Distribution] -Zielkarte.
* **Ihre Adobe-Organisations-ID kennen:** Ihre [!DNL Adobe] Organisations-ID ist erforderlich, um Ihre Nutzungsbedingungen abzuschließen. Weitere Informationen zum Anzeigen Ihrer Organisations-ID [ finden Sie unter [!DNL Adobe's] *Unternehmen unter Experience Cloud* .](https://experienceleague.adobe.com/de/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)

## Unterstützte Ziele {#supported-destinations}

Das Ziel [!DNL Acxiom Audience Distribution] unterstützt derzeit die Aktivierung der Zielgruppe für die folgenden Plattformen.<br>

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## Herstellen einer Verbindung mit dem Ziel {#connect}

Die Authentifizierung am Ziel [!DNL Acxiom's Audience Distribution] erfolgt automatisch hinter den Kulissen, damit Sie es bequem finden.

## Zielspezifische Einstellungen {#destination-settings}

Einige [!DNL Acxiom Audience Distribution] -Ziele erfordern zusätzliche Informationen. Die folgenden Abschnitte enthalten ausführliche Anleitungen zum Konfigurieren dieser Optionen.

### [!DNL LG Ads] {#lg-ads}

Füllen Sie die unten stehenden Felder aus, um Details für das Ziel zu konfigurieren.

* **Segmentkategorie**: Die Zielkategorie oder Vertikale, in die Ihr Segment fällt. Beispiel: Finanzdienstleistungen, Automobil, Gesundheit usw.

![LG Ads destination details](../../assets/catalog/advertising/acxiom-audience-distribution/lg_ads_destination_details.png)

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md).

>[!NOTE]
>
>Das Ziel [!DNL Acxiom Audience Distribution] unterstützt nur vollständige Dateiexporte.

### Zuordnen von Attributen und Identitäten {#map}

Damit das Ziel [!DNL Acxiom Audience Distribution] die Zielgruppendaten korrekt empfangen kann, müssen Sie die Quellfelder von der Experience Platform den korrekten [!DNL Acxiom Audience Distribution] Zielfeldern zuordnen.

[!DNL Acxiom Audience Distribution] erlaubt nur die Zuordnung zu den folgenden Zielfeldern. Die in der folgenden Tabelle beschriebenen Zielfelder müssen in der unten gezeigten Reihenfolge zugeordnet werden.

| Feldname | Beschreibung | Erforderlich | Feldreihenfolge | Max. Länge |
|---|---|---|---|---|          
| Vorname | Vorname der Person | Nein | 1 | 255 |
| Mittel | Mittlerer oder erster Name der Person | Nein | 2 | 50 |
| Nachname | Nachname der Person | Ja | 3 | 255 |
| Generations-Suffix | Suffix des Kontakts | Nein | 4 | 10 |
| Adresszeile 1 | Feld Adresse 1 des Hauptwohnsitzes | Ja | 5 | 255 |
| Adresszeile 2 | Feld Adresse 2 des Hauptwohnsitzes | Nein | 6 | 255 |
| Stadt | Wohnort | Ja | 7 | 255 |
| Land | Landesabkürzung des Hauptwohnsitzes | Ja | 8 | 2 |
| Postleitzahl | Vollständige Postleitzahl des Hauptwohnsitzes | Ja | 9 | 10 |
| E-Mail | Primäre E-Mail Standardmäßig wird dieses Feld als Deduplizierungsschlüssel verwendet, um die Datensätze eindeutig zu machen. | Nein | 10 | 255 |
| Telefon | Telefonnummer der Person (Bereichscode + Nummer)<br> Standardmäßig wird dieses Feld als Deduplizierungsschlüssel verwendet, um die Datensätze eindeutig zu machen. | Nein | 11 | 10 |

Geben Sie in der Spalte **[!UICONTROL Source-Feld]** den Namen der einzelnen Quellattribute ein, die Sie dem entsprechenden Zielfeld zuordnen möchten, oder wählen Sie das Pfeilsymbol aus, um den Bildschirm **[!UICONTROL Quellfeld auswählen]** zu öffnen.<br>
![Mapping screen](../../assets/catalog/advertising/acxiom-audience-distribution/mapping_screen.png)

Nachdem Sie alle Felder zugeordnet haben, wählen Sie **[!UICONTROL Weiter]** aus.

Wenn Sie das Standardschema [!DNL Adobe's] nicht verwenden, finden Sie in der Dokumentation zum [UI-Handbuch für Query Service](../../../query-service/ui/overview.md) Informationen dazu, wie Sie mit dem Abfragedienst das Standardschema [!DNL Adobe] mit Ihren Feldnamen füllen können.

### Überprüfung {#review}

Nachdem Sie alle oben genannten Schritte ausgeführt haben, können Sie Ihren Zielverbindungsstatus und die Zielgruppendetails überprüfen, bevor Sie ihn aktivieren (verteilen). Die von Ihnen ausgewählten Zielgruppen werden unten in einer Liste angezeigt. Jede Zielgruppe ist ein separater Aufruf der [!DNL Acxiom Audience Distribution] -API.

Wenn Sie mit den Ergebnissen zufrieden sind, wählen Sie **[!UICONTROL Beenden]** aus, um Ihr Ziel zu aktivieren.

![Überprüfen der Audience](../../assets/catalog/advertising/acxiom-audience-distribution/review_audience.png)

## Fehlerbehebung {#troubleshooting}

Wenn Ihr Zielvertreter Ihre Zielgruppe nicht finden kann, wenden Sie sich an Ihren [!DNL Adobe] -Support-Mitarbeiter.

Sie müssen Ihrem [!DNL Adobe] -Support-Mitarbeiter die folgenden Informationen zur Verfügung stellen:
* Zielgruppenname
* Name des Ziels
* Aktivierungsdatum der Zielgruppe
* Exportierter Dateiname

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich eine Zielgruppe für die ausgewählte Zielplattform aktiviert. Wenden Sie sich als Nächstes an Ihren für die Zielplattform zuständigen Support-Mitarbeiter, um mit der Einrichtung Ihrer Kampagne zu beginnen.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).


