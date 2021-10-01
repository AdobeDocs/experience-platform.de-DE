---
title: Verbindung mit Verizon MediaYahoo DataX
description: DataX ist eine aggregierte Infrastruktur von Verizon Media/Yahoo, die verschiedene Komponenten hostet, mit denen Verizon Media/Yahoo Daten mit externen Partnern auf sichere, automatisierte und skalierbare Weise austauschen kann.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 16%

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

DataX ist durch die in der [DataX-Dokumentation](https://developer.verizonmedia.com/datax/guide/rate-limits/) beschriebenen Quotenbeschränkungen für Taxonomie- und Zielgruppenbeiträge begrenzt.


| Fehler-Code | Fehlermeldung | Beschreibung |
|---------|----------|---------|
| 429 Zu viele Anfragen | Ratenlimit überschritten pro Stunde **(Limit: 100)** | Anzahl der zulässigen Anforderungen in einer Stunde pro Provider. |

{style=&quot;table-layout:auto&quot;}

**Taxonomie-Metadaten**

Die Taxonomie-Ressource definiert eine Erweiterung über die Basisdatenstruktur

```
{

  >>(Base DataX Metadata)<<

        "extensions" : { "action" :
        {string}, "incrementalData" :
        {
                "taxonomyId": {string}
                },
                "links" : [{
                "rel"   : "https://datax.yahooapis.com/rels/fullTaxonomy", "title" : "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

Weitere Informationen zu [Taxonomy-Metadaten](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) finden Sie in der DataX-Entwicklerdokumentation.

## Unterstützte Identitäten {#supported-identities}

Verizon Media unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erfahren Sie mehr über [identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de#getting-started).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash. |
| GAID | Google Advertising ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |

{style=&quot;table-layout:auto&quot;}

## Exporttyp {#export-type}

**Segmentexport** : Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (E-Mail), die im Verizon Media-Ziel verwendet werden.

## Anwendungsfälle {#use-cases}

DataX-APIs sind für Advertiser verfügbar, die eine bestimmte Zielgruppen-Gruppe ansprechen möchten, die von E-Mail-Adressen in Verizon Media (VMG) abgeleitet wurde. Diese können schnell ein neues Segment erstellen und die gewünschte Zielgruppe mithilfe der API von VMGs nahezu in Echtzeit übertragen.

## Mit Ziel verbinden {#connect}

![Yahoo DataX-Zielkarte in der Platform-Benutzeroberfläche](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL MDM-ID]**: Dies ist eine eindeutige Kennung in Yahoo DataX und ein Pflichtfeld zum Einrichten von Datenexporten an dieses Ziel. Wenn Sie diese ID nicht kennen, wenden Sie sich an Ihren Yahoo Data X-Kundenbetreuer.  Mit MDM-IDs können Daten nur mit bestimmten exklusiven Benutzern (z. B. Erstanbieterdaten für Advertiser) für die Verwendung eingeschränkt werden.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für Ziele finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-segment-streaming-destinations.md) .

## Datennutzung und -verwaltung {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie [!DNL Adobe Experience Platform] Data Governance durchsetzt, finden Sie unter [Übersicht über Data Governance](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen finden Sie in der Dokumentation zu Yahoo/Verizon Media [zu DataX](https://developer.verizonmedia.com/datax/guide/).
