---
title: Verbindung mit Verizon MediaYahoo DataX
description: DataX ist eine aggregierte Infrastruktur von Verizon Media/Yahoo, die verschiedene Komponenten hostet, mit denen Verizon Media/Yahoo Daten mit externen Partnern auf sichere, automatisierte und skalierbare Weise austauschen kann.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 22%

---

# Verbindung zwischen Verizon Media/Yahoo DataX

## Übersicht {#overview}

DataX ist eine aggregierte Infrastruktur von Verizon Media/Yahoo, die verschiedene Komponenten hostet, mit denen Verizon Media/Yahoo Daten mit externen Partnern auf sichere, automatisierte und skalierbare Weise austauschen kann.

>[!IMPORTANT]
>
>Diese Dokumentationsseite wurde vom DataX-Team von Verizon Media/Yahoo erstellt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Voraussetzungen {#prerequisites}

**MDM-ID**

Dies ist eine eindeutige Kennung in Yahoo DataX und ein Pflichtfeld zum Einrichten von Datenexporten an dieses Ziel. Wenn Sie diese ID nicht kennen, wenden Sie sich an Ihren Yahoo Data X-Kundenbetreuer.

**Ratenbeschränkung**

DataX ist durch die im Abschnitt [DataX-Dokumentation](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Fehler-Code | Fehlermeldung | Beschreibung |
|---------|----------|---------|
| 429 Zu viele Anfragen | Ratenlimit überschritten pro Stunde **(Limit: 100)** | Anzahl der zulässigen Anforderungen in einer Stunde pro Provider. |

{style=&quot;table-layout:auto&quot;}

**Taxonomie-Metadaten**

Die Taxonomie-Ressource definiert eine Erweiterung über die Basisdatenstruktur

```
{

  >>(Base DataX Metadata)<<

        "extensions": { "action":
        {string}, "incrementalData":
        {
                "taxonomyId": {string}
                },
                "links": [{
                "rel": "https://datax.yahooapis.com/rels/fullTaxonomy", "title": "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

Mehr dazu [Taxonomie-Metadaten](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) in der DataX-Entwicklerdokumentation.

## Unterstützte Identitäten {#supported-identities}

Verizon Media unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Weitere Informationen [identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de#getting-started).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, um [!DNL Platform] die Daten bei Aktivierung automatisch hash. |
| GAID | Google Advertising ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |

{style=&quot;table-layout:auto&quot;}

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (E-Mail, GAID, IDFA), die im Verizon Media-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Anwendungsfälle {#use-cases}

DataX-APIs sind für Advertiser verfügbar, die eine bestimmte Zielgruppen-Gruppe ansprechen möchten, die von E-Mail-Adressen in Verizon Media (VMG) abgeleitet wurde. Diese können schnell ein neues Segment erstellen und die gewünschte Zielgruppe mithilfe der API von VMGs nahezu in Echtzeit übertragen.

## Mit Ziel verbinden {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

![Yahoo DataX-Zielkarte in der Platform-Benutzeroberfläche](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL MDM-ID]**: Dies ist eine eindeutige Kennung in Yahoo DataX und ein Pflichtfeld zum Einrichten von Datenexporten an dieses Ziel. Wenn Sie diese ID nicht kennen, wenden Sie sich an Ihren Yahoo Data X-Kundenbetreuer.  Mit MDM-IDs können Daten nur mit bestimmten exklusiven Benutzern (z. B. Erstanbieterdaten für Advertiser) für die Verwendung eingeschränkt werden.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für Ziele.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

## Weitere Ressourcen {#additional-resources}

Weitere Informationen finden Sie in den Yahoo/Verizon-Medien [Dokumentation zu DataX](https://developer.verizonmedia.com/datax/guide/).
