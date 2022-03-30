---
title: Verwandte Konten in Real-Time CDP B2B Edition
type: Documentation
description: Eine Übersicht und weitere Informationen über die zugehörige Kontofunktion in der Echtzeit-Kundendatenplattform von Experience Platform B2B.
source-git-commit: 09fd6c30461a4229411ce67426fdcb247661f7cb
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 7%

---

# Verwandte Konten in Real-Time CDP B2B Edition

## Übersicht {#overview}

B2B-Unternehmen haben häufig ihre Kundeninformationen in mehreren Systemen gespeichert, von denen jede nur teilweise oder sogar widersprüchliche Daten für dieselbe reale Geschäftseinheit enthält. Dies stellt eine enorme Herausforderung dar, eine genaue Ansicht der Kunden zu erhalten und so die Effizienz und Effektivität ihrer B2B-Marketing- und Verkaufsaktivitäten zu reduzieren.

| ID | Name | Website | Branche | Land | Telefon | Hat eine Opportunity mit dem Wert > `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | Software | CA | (408)536-6000 |  |
| 2 | Acme | acm.com | Software | CA | 4085366000 | x |
| 3 | Acme Inc |  |  | CA | (408)5366000 |  |
| 4 | Acme Consulting Service | `http://www.acme.com/consulting` | Technologieberatung | NY | (212)471-0904 | x |
| 5 | Acme IT |  |  | CA |  |  |

{style=&quot;table-layout:auto&quot;}

mit den entsprechenden Konten, [!DNL Real-time CDP B2B] zeigt Ihnen jetzt eine Liste von Konten an, die dem Konto, das Sie durchsuchen, ähnlich sind.

![Bildschirm mit verwandten Konten in der Experience Platform-Benutzeroberfläche.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

Verwenden Sie diese Funktion, um verwandte Kontoprofile für ein Kontoprofil in der Experience Platform-Benutzeroberfläche anzuzeigen und dann die zugehörigen Konten in Ihre Segmentdefinitionen aufzunehmen, um Ihre Reichweite zu erweitern oder umfassendere Kriterien in Ihren  anzuwenden.

## Funktionsweise {#how-it-works}

Tägliche Aufträge für maschinelles Lernen verwenden einen hierarchischen Algorithmus, um ähnliche Kontoprofile basierend auf drei Faktoren in Gruppen zu gruppieren:

* Link zum übergeordneten Konto
* Webdomäne
* Kontoname

Nach einem erfolgreichen Verarbeitungsauftrag wird jedes Mitglied der Kontoprofilgruppe mit der Liste &quot;Zugehörige Konten&quot;getaggt. Sie können die Liste im **Verwandte Konten** auf der Seite &quot;Kontoprofil&quot;ein und verwenden Sie die zugehörigen Konten in Segmentdefinitionen.

Weitere Informationen zu [Vorgänge im Zusammenhang mit der Profilanreicherung](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).

## Darstellung verwandter Konten {#how-to-view}

Sie können zugehörige Konten für ein Konto, das Sie durchsuchen, in der Benutzeroberfläche von Experience Platform anzeigen.

Weitere Informationen zu [Finden verwandter Konten in der Benutzeroberfläche](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab).

## Verwendung verwandter Konten {#how-to-use}

Sie können Konten und zugehörige Konten bei der Segmentierung verwenden. Die Entscheidung, ob verwandte Konten in Ihren Segmentdefinitionen verwendet werden sollen, hängt von Ihrem Marketing-Anwendungsfall ab. Sie können beispielsweise verwandte Konten für E-Mail-Marketing- oder Werbekampagnen verwenden, bei denen Sie im Austausch für eine größere Reichweite eine geringere Genauigkeit akzeptieren können.

Siehe [Segmentierungsbeispiel](/help/rtcdp/segmentation/b2b.md#related-account) verwendet verwandte Konten.