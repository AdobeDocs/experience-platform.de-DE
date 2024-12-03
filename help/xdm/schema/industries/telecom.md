---
solution: Experience Platform
title: Datenmodell für die Telekommunikationsbranche ERD
description: Zeigen Sie ein Entitäts-Beziehungsdiagramm (ERD) an, das ein standardisiertes Datenmodell für die Telekommunikationsbranche beschreibt, das mit Experience-Datenmodell (XDM) für die Verwendung in Adobe Experience Platform kompatibel ist.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 23bf89977b13a1f51e1ea7a0bb0561522a09745d
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 1%

---

# [!UICONTROL Telekommunikation] Industriedatenmodell ERD

Das folgende Entitätsbeziehungsdiagramm (ERD) stellt ein standardisiertes Datenmodell für die Telekommunikationsbranche dar. Der ERD wird absichtlich denormalisiert und unter Berücksichtigung der Speicherung von Daten in Adobe Experience Platform präsentiert.

>[!NOTE]
>
>Der ERD wie beschrieben ist eine Empfehlung, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Platform nutzen zu können, müssen Sie die empfohlenen Schemas und deren Beziehungen selbst erstellen. Weitere Informationen finden Sie in den Handbüchern zum Verwalten von [Schemas](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche.

Verwenden Sie die folgende Legende, um diese ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einer zugrunde liegenden [Erlebnis-Datenmodell (XDM)-Klasse](../composition.md#class).
* Die unter einem übergeordneten Feld eingerückten Felder stellen ein untergeordnetes Feld oder Unterfeld dar, das zur Feldergruppe des übergeordneten Felds gehört.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kunden verwendet werden können, werden als &quot;Identität&quot;gekennzeichnet, wobei eine dieser Eigenschaften als &quot;primäre Identität&quot;markiert ist.
* Entitätsbeziehungen werden als nicht abhängig markiert, da Cookie-basierte Ereignisse häufig nicht die Person oder Person bestimmen können, die die Transaktion getätigt hat.


![Beispiel-ERD für ein Datenmodell der Telekommunikationsbranche](../../images/industries/telecom.png)

>[!NOTE]
>
>Die Entität &quot;Erlebnisereignis&quot;enthält das Feld &quot;_ID&quot;, das das von der XDM ExperienceEvent-Klasse bereitgestellte Attribut für die eindeutige Kennung (`_id`) darstellt. Weitere Informationen dazu, was für diesen Wert erwartet wird, finden Sie im Referenzdokument zu [XDM ExperienceEvent](../../classes/experienceevent.md) .

## Anwendungsfälle für [!UICONTROL Telekommunikation]

In der folgenden Tabelle werden die empfohlenen Klassen und Schemafeldgruppen für verschiedene gängige Anwendungsfälle für die Telekommunikationsbranche beschrieben.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Verstehen Sie Kunden, die anhand ihrer aktuellen Beteiligungen und ihres Browsing-Verhaltens gute Kandidaten für Upsell- oder Crosssell-Möglichkeiten sind. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Upsell Details]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL Upgrade-Details]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Telekom-Abonnement]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdetails]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Retargeting von Warenkorbabbrüchen durch relevante Anzeigen und automatisierte personalisierte E-Mails. Unterdrücken Sie Anzeigen bei der Konvertierung. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Commerce Details]](../../field-groups/event/upsell-details.md) (zum Erfassen von Warenkorbabbrüchen)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Telekom-Abonnement]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdetails]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Wenn ein Kunde als abwanderungswahrscheinlich markiert ist (basierend auf einer Mitarbeiterinteraktion oder einem automatisierten maschinellen Lernalgorithmus), senden Sie die Kundendetails an digitale und nicht-digitale Kanäle. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Kampagnen-Marketing-Details]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL Kanaldetails]](../../field-groups/event/channel-details.md)</li><li>Eine benutzerdefinierte Feldergruppe mit personalisiertem Inhalt</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdetails]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
