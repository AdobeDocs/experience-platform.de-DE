---
title: Verbindung mit Verizon MediaYahoo DataX
description: DataX ist eine aggregierte Infrastruktur von Verizon Media/Yahoo, die verschiedene Komponenten hostet, mit denen Verizon Media/Yahoo Daten mit externen Partnern auf sichere, automatisierte und skalierbare Weise austauschen kann.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 43%

---

# [!DNL Verizon Media/Yahoo DataX]-Verbindung

## Übersicht {#overview}

[!DNL DataX] ist eine aggregierte [!DNL Verizon Media/Yahoo] Infrastruktur, die verschiedene Komponenten hostet, die es [!DNL Verizon Media/Yahoo] ermöglichen, Daten mit externen Partnern auf sichere, automatisierte und skalierbare Weise auszutauschen.

>[!IMPORTANT]
>
>Diese Ziel-Connector- und Dokumentationsseite werden vom [!DNL DataX]-Team von [!DNL Verizon Media/Yahoo] erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Voraussetzungen {#prerequisites}

**MDM ID**

Dies ist eine eindeutige Kennung in [!DNL Yahoo DataX] und ein Pflichtfeld zum Einrichten von Datenexporten an dieses Ziel. Wenn Sie diese ID nicht kennen, wenden Sie sich an Ihren [!DNL Yahoo DataX] -Kundenbetreuer.

**Taxonomy metadata**

Die Taxonomieressource definiert eine Erweiterung über die Basis-Metadatenstruktur [!DNL DataX]

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

Weitere Informationen zu [Taxonomy-Metadaten](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) finden Sie in der Entwicklerdokumentation von [!DNL DataX] .

## Ratenbeschränkungen und Limits {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Wenn Sie mehr als 100 Zielgruppen auf [!DNL Verizon Media/Yahoo DataX] aktivieren, erhalten Sie möglicherweise Fehler mit Ratenbegrenzung vom Ziel. Versuchen Sie beim Aktivieren von Zielgruppen für dieses Ziel, weniger als 100 Zielgruppen in einem Aktivierungsdatenfluss zu aktivieren. Wenn Sie weitere Segmente aktivieren müssen, erstellen Sie ein neues Ziel für dasselbe Konto.

[!DNL DataX] ist durch die Quotenbegrenzungen für Taxonomie- und Zielgruppenbeiträge begrenzt, die in der [DataX-Dokumentation](https://developer.verizonmedia.com/datax/guide/rate-limits/) beschrieben sind.


| Fehler-Code | Fehlermeldung | Beschreibung |
|---------|----------|---------|
| 429 Zu viele Anfragen | Ratenlimit überschritten pro Stunde **(Limit: 100)** | Anzahl der zulässigen Anforderungen in einer Stunde pro Provider. |

{style="table-layout:auto"}

## Unterstützte Identitäten {#supported-identities}

[!DNL Verizon Media] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (E-Mail, GAID, IDFA), die im Verizon Media-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anwendungsfälle {#use-cases}

[!DNL DataX] APIs sind für Advertiser verfügbar, die eine bestimmte Zielgruppen-Gruppe ansprechen möchten, die von E-Mail-Adressen in [!DNL Verizon Media] (VMG) abgeleitet wurde, und die schnell eine neue Zielgruppe erstellen und die gewünschte Zielgruppe mithilfe der nahezu Echtzeit-API von VMG übertragen können.

## Mit Ziel verbinden {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

![Yahoo DataX-Zielkarte in der Platform-Benutzeroberfläche](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL MDM-ID]**: Dies ist eine eindeutige Kennung in [!DNL Yahoo DataX] und ein Pflichtfeld zum Einrichten von Datenexporten an dieses Ziel. Wenn Sie diese ID nicht kennen, wenden Sie sich an Ihren [!DNL Yahoo DataX] -Kundenbetreuer.  Mit MDM-IDs können Daten nur mit bestimmten exklusiven Benutzern (z. B. Erstanbieterdaten für Advertiser) für die Verwendung eingeschränkt werden.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für Ziele finden Sie unter [Profile und Zielgruppen für ein Ziel aktivieren](../../ui/activate-segment-streaming-destinations.md) .

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen finden Sie in der Dokumentation zu [!DNL Yahoo/Verizon Media] [auf  [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
