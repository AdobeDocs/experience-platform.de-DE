---
title: Verwandte Konten in Real-Time CDP B2B Edition
type: Documentation
description: Eine Übersicht und weitere Informationen über die zugehörige Kontofunktion in Experience Platform Real-Time CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 14%

---

# Verwandte Konten in Real-Time CDP B2B Edition

## Übersicht {#overview}

B2B-Unternehmen haben häufig ihre Kundeninformationen in mehreren Systemen gespeichert, von denen jedes nur teilweise oder sogar widersprüchliche Daten für dieselbe reale Geschäftseinheit enthält. Dies stellt eine enorme Herausforderung dar, eine genaue Ansicht der Kunden zu erhalten und so die Effizienz und Effektivität ihrer B2B-Marketing- und Verkaufsaktivitäten zu reduzieren.

| ID | Name | Website | Branche | Land | Telefon | Hat offene Gelegenheit mit einem Betrag > `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | Software | CA | (408)536-6000 |   |
| 2 | Acme | acm.com | Software | CA | 4085366000 | x |
| 3 | Acme Inc |   |   | CA | (408)5366000 |   |
| 4 | Acme Consulting Service | `http://www.acme.com/consulting` | Technologieberatung | NY | (212)471-0904 | x |
| 5 | Acme IT |   |   | CA |   |   |

{style="table-layout:auto"}

Mit verwandten Konten zeigt Ihnen [!DNL Real-Time CDP B2B] jetzt eine Liste von Konten an, die dem von Ihnen verwendeten Konto ähnlich sind.

![Bildschirm mit verwandten Konten in der Experience Platform-Benutzeroberfläche.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

Verwenden Sie diese Funktion, um verwandte Kontoprofile für ein Kontoprofil in der Experience Platform-Benutzeroberfläche anzuzeigen und dann die zugehörigen Konten in Ihre Segmentdefinitionen aufzunehmen, um Ihre Reichweite zu erweitern oder umfassendere Kriterien in Ihren Zielgruppen anzuwenden.

## Aktivieren des zugehörigen Kontodienstes {#enable}

Um den Dienst zu aktivieren, wählen Sie **[!UICONTROL Profile]** in der Seitenleiste gefolgt von **[!UICONTROL Einstellungen]** aus.

![Experience Platform UI, die Profile und Einstellungen hervorhebt.](../assets/../b2b-ai-ml-services/assets/related-account-settings.png)

Wählen Sie den Umschalter neben [!UICONTROL Zugehörige Konten aktivieren] aus, um den Dienst zu aktivieren, und wählen Sie dann **[!UICONTROL Speichern]** aus.

![Bildschirm &quot;Kontoeinstellungen&quot;, der den Umschalter und das Speichern markiert.](../assets/../b2b-ai-ml-services/assets/related-account-toggle.png)

## Funktionsweise {#how-it-works}

Tägliche Aufträge für maschinelles Lernen verwenden einen hierarchischen Algorithmus, um ähnliche Kontoprofile basierend auf drei Faktoren in Gruppen zu gruppieren:

* Link zum übergeordneten Konto
* Webdomain
* Kontoname

Nach einem erfolgreichen Verarbeitungsauftrag wird jedes Mitglied der Kontoprofilgruppe mit der Liste Zugehörige Konten markiert. Sie können die Liste auf der Registerkarte **Zugehörige Konten** der Seite &quot;Kontoprofil&quot;anzeigen und die zugehörigen Konten in Segmentdefinitionen verwenden.

Weitere Informationen zu den [Aufträgen zur Profilanreicherung von Konten](/help/dataflows/ui/b2b/monitor-profile-enrichment.md) finden Sie in der Dokumentation .

## Darstellung verwandter Konten {#how-to-view}

Sie können zugehörige Konten für ein Konto, das Sie durchsuchen, in der Experience Platform-Benutzeroberfläche anzeigen.

Weitere Informationen zum Auffinden verwandter Konten in der Benutzeroberfläche finden Sie in der Dokumentation [ .](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)

## Verwendung verwandter Konten {#how-to-use}

Sie können Konten und zugehörige Konten bei der Segmentierung verwenden. Die Entscheidung, ob verwandte Konten in Ihren Segmentdefinitionen verwendet werden sollen, hängt von Ihrem Marketing-Anwendungsfall ab. Sie können beispielsweise verwandte Konten für E-Mail-Marketing- oder Werbekampagnen verwenden, bei denen Sie im Austausch für eine größere Reichweite eine geringere Genauigkeit akzeptieren können.

Siehe ein [Segmentierungsbeispiel](/help/rtcdp/segmentation/b2b.md#related-accounts), das verwandte Konten verwendet.
