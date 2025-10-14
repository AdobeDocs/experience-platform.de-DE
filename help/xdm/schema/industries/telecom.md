---
solution: Experience Platform
title: Datenmodell ERD der Telekommunikationsbranche
description: Zeigen Sie ein Entitätsbeziehungsdiagramm (Entity Relationship Diagram, ERD) an, das ein standardisiertes Datenmodell für die Telekommunikationsbranche beschreibt, das mit dem Experience-Datenmodell (XDM) für die Verwendung in Adobe Experience Platform kompatibel ist.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 1%

---

# [!UICONTROL Telekommunikation] Datenmodell ERD

Das folgende Entitätsbeziehungsdiagramm (Entity Relationship Diagram, ERD) stellt ein standardisiertes Datenmodell für die Telekommunikationsbranche dar. Das ERD wird absichtlich auf entnormierte Weise und unter Berücksichtigung der Art und Weise präsentiert, wie Daten in Adobe Experience Platform gespeichert werden.

>[!NOTE]
>
>Das ERD wie beschrieben ist eine Empfehlung dafür, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Experience Platform verwenden zu können, müssen Sie die empfohlenen Schemata und ihre Beziehungen selbst erstellen. Weitere Informationen finden Sie in den Handbüchern zur Verwaltung [Schemata](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche.

Folgende Legende verwenden, um dieses ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einer zugrunde liegenden [Experience-Datenmodell (XDM)-](../composition.md#class).
* Unter einem übergeordneten Feld eingerückte Felder stellen ein untergeordnetes Feld oder Unterfeld dar, das zur Feldergruppe des übergeordneten Felds gehört.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kundinnen und Kunden verwendet werden können, werden als „Identität“ gekennzeichnet, wobei eine dieser Eigenschaften als „primäre Identität“ markiert ist.
* Entitätsbeziehungen werden als nicht abhängig gekennzeichnet, da Cookie-basierte Ereignisse häufig nicht die Person oder Einzelperson bestimmen können, die die Transaktion durchgeführt hat.


![Ein Beispiel-ERD für ein Datenmodell der Telekommunikationsbranche](../../images/industries/telecom.png)

>[!NOTE]
>
>Die Erlebnisereignisentität enthält ein Feld „_ID“, das das von der XDM ExperienceEvent-Klasse bereitgestellte Attribut für die eindeutige Kennung (`_id`) darstellt. Weitere Informationen dazu, was für [&#x200B; Wert erwartet wird, finden Sie &#x200B;](../../classes/experienceevent.md) Referenzdokument unter XDM ExperienceEvent .

## [!UICONTROL Telekommunikation] Anwendungsfälle

In der folgenden Tabelle sind die empfohlenen Klassen und Schemafeldgruppen für mehrere gängige Anwendungsfälle für die Telekommunikationsbranche aufgeführt.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Verstehen Sie Kunden, die sich für Upsell- oder Crosssell-Möglichkeiten eignen, basierend auf ihrem aktuellen Bestand und ihrem Browsing-Verhalten. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Upsell-Details]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL Upgrade-Details]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Telekom-Abonnement]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdaten]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Retargeting von Warenkorbabbrüchen durch relevante Anzeigen und automatisierte personalisierte E-Mails. Unterdrücken Sie Anzeigen, wenn sie konvertieren. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Commerce-Details]](../../field-groups/event/upsell-details.md) (zur Erfassung von Warenkorbabbrüchen)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Telekom-Abonnement]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdaten]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Wenn ein Kunde mit Abwanderungswahrscheinlichkeit gekennzeichnet ist (basierend auf einer Mitarbeiterinteraktion oder einem Algorithmus für automatisiertes maschinelles Lernen), senden Sie die Kundendetails an digitale und nicht digitale Kanäle. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Kampagnen-Marketing-Details]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL Kanaldetails]](../../field-groups/event/channel-details.md)</li><li>Eine benutzerdefinierte Feldergruppe mit personalisierten Inhalten</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdaten]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
