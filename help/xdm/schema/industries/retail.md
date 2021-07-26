---
solution: Experience Platform
title: Datenmodell der Einzelhandelsbranche
topic-legacy: overview
description: Sehen Sie sich ein standardisiertes Datenmodell für den Einzelhandel an, das mit dem Experience-Datenmodell (XDM) kompatibel ist und in Adobe Experience Platform verwendet werden kann.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 38fa2345cb87e50bd4c8788996f03939fb199cf9
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

#  Einzelhandelsdatenmodell

Das folgende Entitätsbeziehungsdiagramm (ERD) stellt ein standardisiertes Datenmodell für die Einzelhandelsbranche dar. Der ERD wird absichtlich denormalisiert und unter Berücksichtigung der Art und Weise, wie Daten in Adobe Experience Platform gespeichert werden, präsentiert.

>[!NOTE]
>
>Der ERD wie beschrieben ist eine Empfehlung, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Platform nutzen zu können, müssen Sie die empfohlenen Schemas und deren Beziehungen selbst erstellen. Weitere Informationen finden Sie in den Handbüchern zum Verwalten von [Schemas](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche.

Verwenden Sie die folgende Legende, um diese ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einer zugrunde liegenden [Experience-Datenmodell (XDM)-Klasse](../composition.md#class).
* Für eine bestimmte Entität steht jede in **bold** markierte Zeile für eine Feldergruppe oder einen Datentyp mit den entsprechenden Feldern, die unten in unfettetem Text aufgeführt sind.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kunden verwendet werden können, werden als &quot;Identität&quot;gekennzeichnet, wobei eine dieser Eigenschaften als &quot;primäre Identität&quot;markiert ist.
* Entitätsbeziehungen werden als nicht abhängig markiert, da Cookie-basierte Ereignisse häufig nicht die Person oder Person bestimmen können, die die Transaktion getätigt hat.

![](../../images/industries/retail.png)

>[!NOTE]
>
>Die Entität &quot;Erlebnisereignis&quot;enthält ein Feld &quot;_ID&quot;, das das von der XDM ExperienceEvent-Klasse bereitgestellte Attribut für die eindeutige Kennung (`_id`) darstellt. Weitere Informationen dazu, was für diesen Wert erwartet wird, finden Sie im Referenzdokument zu [XDM ExperienceEvent](../../classes/experienceevent.md) .

##  Einzelhandelsfälle

In der folgenden Tabelle sind die empfohlenen Klassen und Schemafeldgruppen für verschiedene gängige Einzelhandelsanwendungsfälle aufgeführt.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Kombinieren Sie Online- und Offline-Datenquellen und lösen Sie geräteübergreifende und Online-/Offline-Identitäten auf, um eine ganzheitliche kanalübergreifende und geräteübergreifende Attributionsberichterstellung bereitzustellen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Commerce-Details](../../field-groups/event/commerce-details.md)</li><li>[Webdetails](../../field-groups/event/web-details.md)</li></ul></li><li>**Produkt**  (benutzerdefinierte Klasse)\*:<ul><li>Produkt (benutzerdefinierte Feldergruppe)\*</li></ul></li></ul> |
| Stellen Sie zielgerichtete und personalisierte Erlebnisse für verschiedene Segmente bereit, um den Umsatz zu steigern und die Plattform bei der Omnichannel-Orchestrierung zu erweitern. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Kampagnen-Marketingdetails](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanaldetails](../../field-groups/event/channel-details.md)</li><li>[Commerce-Details](../../field-groups/event/commerce-details.md)</li><li>[Umgebungsdetails](../../field-groups/event/environment-details.md)</li><li>[Webdetails](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktangaben](../../field-groups/profile/personal-contact-details.md)</li><li>[Kontaktangaben für Arbeitskontakte](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analysieren Sie die Multitouch-Attribution, um die Marketingeffizienz zu verbessern. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Kampagnen-Marketingdetails](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanaldetails](../../field-groups/event/channel-details.md)</li><li>[Commerce-Details](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Verbessern der E-Mail-Relevanz durch verbesserte Segmentierung von Männern und Frauen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Commerce-Details](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**Produkt**  (benutzerdefinierte Klasse)\*:<ul><li>Produkt (benutzerdefinierte Feldergruppe)\*</li></ul></li></ul> |
| Erfassen Sie Loyalitätsdaten (Partner), um relevante Produktinformationen über Web-, E-Mail- und digitale Marketingkanäle hinweg zu verbessern. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Webdetails](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Treuedetails](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**Produkt**  (benutzerdefinierte Klasse)\*:<ul><li>Produkt (benutzerdefinierte Feldergruppe)\*</li></ul></li></ul> |
| Retargeting von Warenkorbabbrüchen durch automatisierte und personalisierte E-Mails. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Commerce-Details](../../field-groups/event/commerce-details.md)</li><li>[Webdetails](../../field-groups/event/web-details.md)</li></ul></li><li>**Produkt**  (benutzerdefinierte Klasse)\*:<ul><li>Produkt (benutzerdefinierte Feldergruppe)\*</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

*\*Während eine standardmäßige Produktklasse für eine zukünftige Version geplant ist, müssen Produktschemata derzeit stattdessen mit einer benutzerdefinierten Klasse erstellt werden. Daher müssen Sie die Struktur der Klasse des Schemas sowie die aller Feldergruppen, die Sie hinzufügen, manuell erstellen. Weitere Informationen finden Sie im Abschnitt [Erstellen einer benutzerdefinierten Klasse](../../ui/resources/classes.md#create) im Handbuch zur XDM-Benutzeroberfläche.*
