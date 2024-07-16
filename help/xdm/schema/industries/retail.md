---
solution: Experience Platform
title: Datenmodell der Einzelhandelsbranche
description: Sehen Sie sich ein standardisiertes Datenmodell für den Einzelhandel an, das mit dem Experience-Datenmodell (XDM) kompatibel ist und in Adobe Experience Platform verwendet werden kann.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 5ceb261dbf1cac58d0cfe620875b8fa7c761abf2
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 6%

---

# [!UICONTROL Einzelhandel] - Branchendatenmodell

Das folgende Entitätsbeziehungsdiagramm (ERD) stellt ein standardisiertes Datenmodell für die Einzelhandelsbranche dar. Der ERD wird absichtlich denormalisiert und unter Berücksichtigung der Speicherung von Daten in Adobe Experience Platform präsentiert.

>[!NOTE]
>
>Der ERD wie beschrieben ist eine Empfehlung, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Platform nutzen zu können, müssen Sie die empfohlenen Schemas und deren Beziehungen selbst erstellen. Weitere Informationen finden Sie in den Handbüchern zum Verwalten von [Schemas](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche.

Verwenden Sie die folgende Legende, um diese ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einer zugrunde liegenden [Erlebnis-Datenmodell (XDM)-Klasse](../composition.md#class).
* Für eine bestimmte Entität stellt jede in **fett** markierte Zeile eine Feldergruppe oder einen Datentyp dar, wobei die entsprechenden Felder unten in unfettetem Text aufgeführt sind.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kunden verwendet werden können, werden als &quot;Identität&quot;gekennzeichnet, wobei eine dieser Eigenschaften als &quot;primäre Identität&quot;markiert ist.
* Entitätsbeziehungen werden als nicht abhängig markiert, da Cookie-basierte Ereignisse häufig nicht die Person oder Person bestimmen können, die die Transaktion getätigt hat.

![](../../images/industries/retail.png)

>[!NOTE]
>
>Die Entität &quot;Erlebnisereignis&quot;enthält das Feld &quot;_ID&quot;, das das von der XDM ExperienceEvent-Klasse bereitgestellte Attribut für die eindeutige Kennung (`_id`) darstellt. Weitere Informationen dazu, was für diesen Wert erwartet wird, finden Sie im Referenzdokument zu [XDM ExperienceEvent](../../classes/experienceevent.md) .

## Anwendungsfälle für [!UICONTROL Einzelhandel]

In der folgenden Tabelle sind die empfohlenen Klassen und Schemafeldgruppen für verschiedene gängige Einzelhandelsanwendungsfälle aufgeführt.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Kombinieren Sie Online- und Offline-Datenquellen und lösen Sie geräteübergreifende und Online-/Offline-Identitäten auf, um eine ganzheitliche kanalübergreifende und geräteübergreifende Attributionsberichterstellung bereitzustellen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsdetails](../../field-groups/event/commerce-details.md)</li><li>[Web-Details](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produkt](../../classes/product.md)**:<ul><li>[Produktkatalog](../../field-groups/product/product-catalog.md)</li><li>[Produktkategorie](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Stellen Sie zielgerichtete und personalisierte Erlebnisse für verschiedene Segmente bereit, um den Umsatz zu steigern und die Plattform bei der Omnichannel-Orchestrierung zu erweitern. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Kampagnen-Marketing-Details](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanaldetails](../../field-groups/event/channel-details.md)</li><li>[Handelsdetails](../../field-groups/event/commerce-details.md)</li><li>[Umgebungsdetails](../../field-groups/event/environment-details.md)</li><li>[Web-Details](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktdetails](../../field-groups/profile/personal-contact-details.md)</li><li>[Kontaktdetails für die Arbeit](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analysieren Sie die Multitouch-Attribution, um die Marketingeffizienz zu verbessern. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Kampagnen-Marketing-Details](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanaldetails](../../field-groups/event/channel-details.md)</li><li>[Handelsdetails](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Verbessern der E-Mail-Relevanz durch verbesserte Segmentierung von Männern und Frauen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsdetails](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[Produkt](../../classes/product.md)**:<ul><li>[Produktkatalog](../../field-groups/product/product-catalog.md)</li><li>[Produktkategorie](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Erfassen Sie Loyalitätsdaten (Partner), um relevante Produktinformationen über Web-, E-Mail- und digitale Marketingkanäle hinweg zu verbessern. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Web-Details](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Details zum Treueprogramm](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[Produkt](../../classes/product.md)**:<ul><li>[Produktkatalog](../../field-groups/product/product-catalog.md)</li><li>[Produktkategorie](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Retargeting von Warenkorbabbrüchen durch automatisierte und personalisierte E-Mails. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsdetails](../../field-groups/event/commerce-details.md)</li><li>[Web-Details](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produkt](../../classes/product.md)**:<ul><li>[Produktkatalog](../../field-groups/product/product-catalog.md)</li><li>[Produktkategorie](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}
