---
title: Verwandte Konten in Real-Time CDP B2B Edition
type: Documentation
description: Eine Übersicht und weitere Informationen zur Funktion „Verknüpfte Konten“ in Experience Platform Real-Time CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 14%

---

# Verwandte Konten in Real-Time CDP B2B Edition

## Übersicht {#overview}

B2B-Unternehmen haben häufig ihre Kundeninformationen in mehreren Systemen gespeichert, von denen jedes nur teilweise oder sogar widersprüchliche Daten für dieselbe reale Geschäftseinheit enthält. Dies stellt eine enorme Herausforderung dar, eine präzise Ansicht der Kunden zu erhalten und mindert so die Effizienz und Effektivität der B2B-Marketing- und Verkaufsaktivitäten.

| ID | Name | Website | Branche | Land | Telefon | Hat offene Opportunity mit Betrag > `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Spitze | acme.com | Software | CA | (408)536-6000 |   |
| 2 | Spitze | acm.com | Software | CA | 4085366000 | x |
| 3 | ACME erh |   |   | CA | (408)5366000 |   |
| 4 | ACME Consulting Service | `http://www.acme.com/consulting` | Technologieberatung | NY | (212)471-0904 | x |
| 5 | Acme IT |   |   | CA |   |   |

{style="table-layout:auto"}

Bei verwandten Konten zeigt [!DNL Real-Time CDP B2B] jetzt eine Liste von Konten an, die dem Konto, das Sie durchsuchen, ähnlich sind.

![Bildschirm mit verwandten Konten in der Experience Platform-Benutzeroberfläche.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

Verwenden Sie diese Funktion, um verwandte Account-Profile für ein Account-Profil in der Experience Platform-Benutzeroberfläche anzuzeigen und dann die verwandten Accounts in Ihre Segmentdefinitionen aufzunehmen, um Ihre Reichweite zu erweitern oder umfassendere Kriterien auf Ihre Audiences anzuwenden.

## Aktivieren des zugehörigen Kontodienstes {#enable}

Um den Dienst zu aktivieren, wählen **[!UICONTROL Profile]** in der Seitenleiste aus, gefolgt von **[!UICONTROL Einstellungen]**.

![Experience Platform-Benutzeroberfläche mit Hervorhebung von Profilen und Einstellungen.](../assets/../b2b-ai-ml-services/assets/related-account-settings.png)

Wählen Sie den Umschalter neben [!UICONTROL Verknüpfte Konten aktivieren] aus, um den Service zu aktivieren, und klicken Sie dann auf **[!UICONTROL Speichern]**.

![Bildschirm mit den Kontoeinstellungen, in dem der Umschalter hervorgehoben und gespeichert wird.](../assets/../b2b-ai-ml-services/assets/related-account-toggle.png)

## Funktionsweise {#how-it-works}

Täglich ausgeführte maschinelle Lernaufträge verwenden einen hierarchischen Algorithmus, um ähnliche Kontoprofile basierend auf drei Faktoren in Gruppen zu gruppieren:

* Übergeordneter Kontolink
* Webdomain
* Kontoname

Nach einem erfolgreichen Verarbeitungsauftrag wird jedes Mitglied der Kontoprofilgruppe mit der Liste Zugehörige Konten getaggt. Sie können die Liste auf der Registerkarte **Verwandte Konten** der Seite Kontoprofil anzeigen und die verwandten Konten in Segmentdefinitionen verwenden.

Weitere Informationen zu den Vorgängen [Profilanreicherung für Konten](/help/dataflows/ui/b2b/monitor-profile-enrichment.md) finden Sie in der Dokumentation.

## Anzeigen verwandter Konten {#how-to-view}

Sie können verwandte Konten für ein Konto, das Sie durchsuchen, in der Experience Platform-Benutzeroberfläche anzeigen.

Weitere Informationen finden Sie in der Dokumentation über [So finden Sie verwandte Konten in der Benutzeroberfläche](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab).

## Wie Sie verwandte Konten verwenden können {#how-to-use}

Sie können in der Segmentierung Konten und zugehörige Konten verwenden. Die Entscheidung, ob verwandte Konten in Ihren Segmentdefinitionen verwendet werden, hängt von Ihrem Marketing-Anwendungsfall ab. Sie können beispielsweise verwandte Konten für E-Mail-Marketing- oder Werbekampagnen verwenden, bei denen Sie im Gegenzug für eine größere Reichweite eine geringere Genauigkeit akzeptieren können.

Siehe ein [Segmentierungsbeispiel](/help/rtcdp/segmentation/b2b.md#related-accounts) das verwandte Konten verwendet.
