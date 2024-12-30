---
solution: Experience Platform
title: Datenmodell der Einzelhandelsbranche
description: Sehen Sie sich ein standardisiertes Datenmodell für die Einzelhandelsbranche an, das mit dem Experience-Datenmodell (XDM) für die Verwendung in Adobe Experience Platform kompatibel ist.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 23bf89977b13a1f51e1ea7a0bb0561522a09745d
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 8%

---

# [!UICONTROL Einzelhandel] Datenmodell der Branche

Das folgende Entitätsbeziehungsdiagramm (Entity Relationship Diagram, ERD) stellt ein standardisiertes Datenmodell für den Einzelhandel dar. Das ERD wird absichtlich auf entnormierte Weise und unter Berücksichtigung der Art und Weise präsentiert, wie Daten in Adobe Experience Platform gespeichert werden.

>[!NOTE]
>
>Das ERD wie beschrieben ist eine Empfehlung dafür, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Platform verwenden zu können, müssen Sie die empfohlenen Schemas und deren Beziehungen selbst erstellen. Weitere Informationen finden Sie in den Handbüchern zur Verwaltung [Schemata](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche.

Folgende Legende verwenden, um dieses ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einer zugrunde liegenden [Experience-Datenmodell (XDM)-](../composition.md#class).
* Unter einem übergeordneten Feld eingerückte Felder stellen ein untergeordnetes Feld oder Unterfeld dar, das zur Feldergruppe des übergeordneten Felds gehört.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kundinnen und Kunden verwendet werden können, werden als „Identität“ gekennzeichnet, wobei eine dieser Eigenschaften als „primäre Identität“ markiert ist.
* Entitätsbeziehungen werden als nicht abhängig gekennzeichnet, da Cookie-basierte Ereignisse häufig nicht die Person oder Einzelperson bestimmen können, die die Transaktion durchgeführt hat.

![Ein Beispiel-ERD für ein Datenmodell der Einzelhandelsbranche](../../images/industries/retail.png)

>[!NOTE]
>
>Die Erlebnisereignisentität enthält ein Feld „_ID“, das das von der XDM ExperienceEvent-Klasse bereitgestellte Attribut für die eindeutige Kennung (`_id`) darstellt. Weitere Informationen dazu, was für [ Wert erwartet wird, finden Sie ](../../classes/experienceevent.md) Referenzdokument unter XDM ExperienceEvent .

## [!UICONTROL Einzelhandel] Anwendungsfälle

In der folgenden Tabelle sind die empfohlenen Klassen und Schemafeldgruppen für mehrere gängige Anwendungsfälle für den Einzelhandel aufgeführt.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Kombinieren Sie Online- und Offline-Datenquellen und lösen Sie geräteübergreifende und Online-/Offline-Identitäten auf, um ganzheitliche kanalübergreifende und geräteübergreifende Attributionsberichte bereitzustellen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsdetails](../../field-groups/event/commerce-details.md)</li><li>[Web-Details](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produkt](../../classes/product.md)**:<ul><li>[Produktkatalog](../../field-groups/product/product-catalog.md)</li><li>[Produktkategorie](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Bereitstellen zielgerichteter und personalisierter Erlebnisse für verschiedene Segmente, um den Umsatz zu steigern und die Plattform bei der Omni-Channel-Orchestrierung zu erweitern. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Kampagnen-Marketing-Details](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanaldetails](../../field-groups/event/channel-details.md)</li><li>[Handelsdetails](../../field-groups/event/commerce-details.md)</li><li>[Umgebungsdetails](../../field-groups/event/environment-details.md)</li><li>[Web-Details](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktdaten](../../field-groups/profile/personal-contact-details.md)</li><li>[Details zum Arbeitskontakt](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analysieren Sie die Multi-Touch-Attribution, um die Marketing-Effizienz zu verbessern. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Kampagnen-Marketing-Details](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanaldetails](../../field-groups/event/channel-details.md)</li><li>[Handelsdetails](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Verbessern Sie die E-Mail-Relevanz durch eine verbesserte Segmentierung von Männern und Frauen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsdetails](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[Produkt](../../classes/product.md)**:<ul><li>[Produktkatalog](../../field-groups/product/product-catalog.md)</li><li>[Produktkategorie](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Nehmen Sie Treueprogramm-(Partner-)Daten auf, um relevante Produktinformationen über Web-, E-Mail- und digitale Marketing-Kanäle zu erhöhen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Web-Details](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Treuedetails](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[Produkt](../../classes/product.md)**:<ul><li>[Produktkatalog](../../field-groups/product/product-catalog.md)</li><li>[Produktkategorie](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Retargeting von Warenkorbabbrüchen über automatisierte und personalisierte E-Mails. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsdetails](../../field-groups/event/commerce-details.md)</li><li>[Web-Details](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produkt](../../classes/product.md)**:<ul><li>[Produktkatalog](../../field-groups/product/product-catalog.md)</li><li>[Produktkategorie](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}
