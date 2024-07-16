---
title: PubMatic Connect
description: PubMatic maximiert den Kundenwert durch die Bereitstellung der programmatischen Digital-Marketing-Lieferkette der Zukunft. PubMatic Connect kombiniert Plattformtechnologie mit dediziertem Service, um Inventar und Daten zu verpacken und zu verarbeiten.
last-substantial-update: 2023-12-14T00:00:00Z
exl-id: 21e07d2c-9a6a-4cfa-a4b8-7ca48613956c
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 42%

---

# PubMatic Connect-Ziel {#pubmatic-connect}

## Übersicht {#overview}

Verwenden Sie [!DNL PubMatic Connect], um den Kundenwert zu maximieren, indem Sie die programmatische digitale Marketing-Lieferkette der Zukunft bereitstellen. [!DNL PubMatic Connect] kombiniert Plattformtechnologie mit dediziertem Service, um die Verpackung und den Austausch von Bestand und Daten zu verbessern.

Verwenden Sie dieses Ziel, um Zielgruppendaten an die [!DNL PubMatic Connect]-Plattform zu senden.

>[!IMPORTANT]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom [!DNL PubMatic]-Team erstellt und gepflegt. Bei Anfragen oder Aktualisierungsanfragen kontaktieren Sie diese direkt unter `support@pubmatic.com`.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL PubMatic Connect]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

### Nutzer der Zielgruppe auf mobilen, Web- und CTV-Plattformen {#targeting}

Herausgeber oder Datenanbieter möchten Zielgruppen von Adobe Experience Platform an [!DNL PubMatic Connect] senden, um Benutzer auf mobilen, Web- und CTV-Plattformen mit einer großen Auswahl an Kennungen anzusprechen.

## Voraussetzungen {#prerequisites}

Wenden Sie sich an Ihren [!DNL PubMatic] -Kundenbetreuer, um sicherzustellen, dass Ihr Konto korrekt konfiguriert ist und das Einstieg in Zielgruppensegmente unterstützt. Sie werden auch sicherstellen, dass Sie über alle relevanten Details verfügen, um dieses Ziel zu verwenden und Sie während der Einrichtung zu unterstützen.

## Unterstützte Identitäten {#supported-identities}

[!DNL PubMatic Connect] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
| --------------- | ------ | --- |
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| extern_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
| --- | --------- | ------ |
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die durch den Experience Platform [Segmentierungsdienst](../../../segmentation/home.md) generiert wurden. |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
| --- | --- | --- |
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder andere), die im PubMatic Connect-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil auf der Grundlage einer Segmentbewertung im Experience Platform aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
> Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Authentifizieren](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL Bearer-Token]**: Füllen Sie das Bearer-Token aus, um sich beim Ziel zu authentifizieren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Zieldetails](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
- **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
- **[!UICONTROL Datenpartner-ID]**: Die in Ihrem [!DNL PubMatic]-Konto für diese Integration eingerichtete Datenpartner-ID.
- **[!UICONTROL Standard-Ländercode]**: Der standardmäßige Ländercode, der auf alle Identitäten angewendet werden soll, wenn im Profil keiner angegeben ist.
- **[!UICONTROL Konto-ID]**: Ihre [!DNL PubMatic Connect] Konto-ID.
- **[!UICONTROL Kontotyp]**: Der Kontotyp Ihres [!DNL PubMatic] Plattformkontos. Wenden Sie sich an Ihren [!DNL PubMatic] -Kundenbetreuer, wenn Sie Fragen zur Auswahl haben. Folgende Optionen sind verfügbar:
   - [!UICONTROL PUBLISHER]
   - [!UICONTROL DEMAND_PARTNER]
   - [!UICONTROL KÄUFER]

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
>
> - Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>
> - Um _identities_ zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](../../assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Quellfelder auswählen:

- Wählen Sie einen Bezeichner aus (normalerweise Namespaces wie IDFA oder einen benutzerdefinierten ID-Namespace).

Zielgruppenfelder auswählen:

- Wenden Sie sich an Ihren [!DNL PubMatic] -Kundenbetreuer, um Informationen dazu zu erhalten, welcher UID-Typ während dieses Schritts korrekt ist.
- Wählen Sie die Nummer vom Typ [!DNL PubMatic UID] aus, die der im ersten Schritt ausgewählten Kennung entspricht.

![Attribute und Identitäten zuordnen](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

## Exportierte Daten/Datenexport validieren {#exported-data}

Mit der Benutzeroberfläche von [!DNL PubMatic] können Sie überprüfen, ob die Daten korrekt übermittelt wurden und ob die Segmente verfügbar sind. Es kann bis zu 24 Stunden dauern, bis Daten gepusht wurden, damit die [!DNL PubMatic] -Benutzeroberfläche aktualisiert wird.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
