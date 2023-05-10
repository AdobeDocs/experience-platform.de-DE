---
solution: Experience Platform
title: Datenmodell für die Telekommunikationsbranche ERD
description: Zeigen Sie ein Entitäts-Beziehungsdiagramm (ERD) an, das ein standardisiertes Datenmodell für die Telekommunikationsbranche beschreibt, das mit Experience-Datenmodell (XDM) für die Verwendung in Adobe Experience Platform kompatibel ist.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 10%

---

# [!UICONTROL Telekommunikation] Branchendatenmodell ERD

Das folgende Entitätsbeziehungsdiagramm (ERD) stellt ein standardisiertes Datenmodell für die Telekommunikationsbranche dar. Der ERD wird absichtlich denormalisiert und unter Berücksichtigung der Art und Weise, wie Daten in Adobe Experience Platform gespeichert werden, präsentiert.

>[!NOTE]
>
>Der ERD wie beschrieben ist eine Empfehlung, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Platform nutzen zu können, müssen Sie die empfohlenen Schemas und deren Beziehungen selbst erstellen. Siehe Handbücher zur Verwaltung [Schemas](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche für weitere Informationen.

Verwenden Sie die folgende Legende, um diese ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einem zugrunde liegenden [Experience-Datenmodell (XDM)-Klasse](../composition.md#class).
* Für eine bestimmte Entität jede Zeile, die in **fett** stellt eine Feldergruppe oder einen Datentyp mit den entsprechenden Feldern dar, die unten im unfetteten Text aufgeführt sind.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kunden verwendet werden können, werden als &quot;Identität&quot;gekennzeichnet, wobei eine dieser Eigenschaften als &quot;primäre Identität&quot;markiert ist.
* Entitätsbeziehungen werden als nicht abhängig markiert, da Cookie-basierte Ereignisse häufig nicht die Person oder Person bestimmen können, die die Transaktion getätigt hat.


![](../../images/industries/telecom.png)

>[!NOTE]
>
>Die Entität &quot;Erlebnisereignis&quot;enthält ein Feld &quot;_ID&quot;, das die eindeutige Kennung (`_id`), das von der XDM ExperienceEvent-Klasse bereitgestellt wird. Siehe Referenzdokument unter [XDM ExperienceEvent](../../classes/experienceevent.md) für weitere Details darüber, was für diesen Wert erwartet wird.

## [!UICONTROL Telekommunikation] Anwendungsfälle

In der folgenden Tabelle werden die empfohlenen Klassen und Schemafeldgruppen für verschiedene gängige Anwendungsfälle für die Telekommunikationsbranche beschrieben.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Verstehen Sie Kunden, die anhand ihrer aktuellen Beteiligungen und ihres Browsing-Verhaltens gute Kandidaten für Upsell- oder Crosssell-Möglichkeiten sind. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Upselling-Details]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL Upgrade-Details]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL Individuelles XDM-Profil]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Telekom-Abonnement]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdaten]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Retargeting von Warenkorbabbrüchen durch relevante Anzeigen und automatisierte personalisierte E-Mails. Unterdrücken Sie Anzeigen bei der Konvertierung. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Commerce-Details]](../../field-groups/event/upsell-details.md) (So erfassen Sie Warenkorbabbrüche)</li></ul></li><li>**[[!UICONTROL Individuelles XDM-Profil]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Telekom-Abonnement]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdaten]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Wenn ein Kunde als abwanderungswahrscheinlich markiert ist (basierend auf einer Mitarbeiterinteraktion oder einem automatisierten maschinellen Lernalgorithmus), senden Sie die Kundendetails an digitale und nicht-digitale Kanäle. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Kampagnen-Marketing-Details]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL Kanaldetails]](../../field-groups/event/channel-details.md)</li><li>Eine benutzerdefinierte Feldergruppe mit personalisiertem Inhalt</li></ul></li><li>**[[!UICONTROL Individuelles XDM-Profil]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdaten]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
