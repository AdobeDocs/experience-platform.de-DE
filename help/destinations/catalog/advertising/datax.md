---
title: Verizon MediaYahoo DataX-Verbindung
description: DataX ist eine aggregierte Infrastruktur von Verizon Media/Yahoo, die verschiedene Komponenten hostet, mit denen Verizon Media/Yahoo Daten mit externen Partnern auf sichere, automatisierte und skalierbare Weise austauschen kann.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 65809628e8535027edb08e54e84b308777036ab2
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 43%

---

# [!DNL Verizon Media/Yahoo DataX]-Verbindung

## Übersicht {#overview}

[!DNL DataX] ist eine aggregierte [!DNL Verizon Media/Yahoo], die verschiedene Komponenten hostet, mit denen [!DNL Verizon Media/Yahoo] Daten sicher, automatisiert und skalierbar mit externen Partnern austauschen können.

>[!IMPORTANT]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden vom [!DNL Verizon Media/Yahoo]-Team von [!DNL DataX] erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [dataoperations@yahooinc.com](mailto:dataoperations@yahooinc.com)

## Voraussetzungen {#prerequisites}

**MDM-ID**

Dies ist eine eindeutige Kennung in [!DNL Yahoo DataX] und ein obligatorisches Feld zum Einrichten von Datenexporten an dieses Ziel. Wenn Sie diese ID nicht kennen, wenden Sie sich an Ihren [!DNL Yahoo DataX] Account Manager.

**Taxonomie-Metadaten**

Die Taxonomie-Ressource definiert eine Erweiterung über die [!DNL DataX]-Metadatenstruktur

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

Weitere Informationen zu [Taxonomie-Metadaten](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) finden Sie in der [!DNL DataX]-Entwicklerdokumentation.

## Ratenbeschränkungen und Leitplanken {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Beim Aktivieren von mehr als 100 Zielgruppen für die [!DNL Verizon Media/Yahoo DataX] erhalten Sie möglicherweise Ratenbegrenzungsfehler vom Ziel. Versuchen Sie beim Aktivieren von Zielgruppen für dieses Ziel, in einem Aktivierungsdatenfluss weniger als 100 Zielgruppen zu aktivieren. Wenn Sie mehr Segmente aktivieren müssen, erstellen Sie ein neues Ziel im selben Konto.

[!DNL DataX] ist gemäß den Quotenbegrenzungen für Taxonomie- und Zielgruppen-Posts, die in der (DataX[Dokumentation) beschrieben ](https://developer.verizonmedia.com/datax/guide/rate-limits/), ratenbegrenzt.


| Fehler-Code | Fehlermeldung | Beschreibung |
|---------|----------|---------|
| 429 Zu viele Anfragen | Ratenlimit pro Stunde überschritten **(Limit: 100)** | Anzahl der zulässigen Anfragen in einer Stunde pro Anbieter. |

{style="table-layout:auto"}

## Unterstützte Identitäten {#supported-identities}

[!DNL Verizon Media] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de#getting-started).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Experience Platform] die Daten bei Aktivierung automatisch hasht. |
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple-ID für Werbetreibende | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (E-Mail, GAID, IDFA), die im Verizon Media-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anwendungsfälle {#use-cases}

[!DNL DataX] APIs sind für Werbetreibende verfügbar, die eine bestimmte Zielgruppe ansprechen möchten, die von E-Mail-Adressen in [!DNL Verizon Media] (VMG) abgeleitet wurde. Sie können schnell eine neue Zielgruppe erstellen und mithilfe der Fast-Echtzeit-API von VMG an die gewünschte Zielgruppe senden.

## Mit Ziel verbinden {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

![Yahoo DataX-Zielkarte in der Experience Platform-Benutzeroberfläche](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL MDM-ID]**: Dies ist eine eindeutige Kennung in [!DNL Yahoo DataX] und ein obligatorisches Feld zum Einrichten von Datenexporten an dieses Ziel. Wenn Sie diese ID nicht kennen, wenden Sie sich an Ihren [!DNL Yahoo DataX] Account Manager.  Mit MDM-IDs können Daten auf die Verwendung bei einer bestimmten Gruppe exklusiver Benutzer beschränkt werden (z. B. First-Party-Daten für Werbetreibende).

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [ Aktivieren von Zielgruppen für Ziele finden Sie ](../../ui/activate-segment-streaming-destinations.md)Aktivieren von Profilen und Zielgruppen für ein Ziel“.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen finden Sie in der [!DNL Yahoo/Verizon Media] [Dokumentation unter [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
