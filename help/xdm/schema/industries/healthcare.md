---
title: Datenmodell ERD der Gesundheitsbranche
description: Zeigen Sie ein Entitätsbeziehungsdiagramm (Entity Relationship Diagram, ERD) an, das ein standardisiertes Datenmodell für die Gesundheitsbranche beschreibt. Dieses Datenmodell ist mit dem Experience-Datenmodell (XDM) für die Verwendung in Adobe Experience Platform kompatibel.
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 8%

---

# [!UICONTROL Gesundheitswesen] Datenmodell ERD der Branche

Das folgende Entitätsbeziehungsdiagramm (Entity Relationship Diagram, ERD) stellt ein standardisiertes Datenmodell für die Gesundheitsbranche dar. Das ERD wird absichtlich auf entnormierte Weise und unter Berücksichtigung der Art und Weise präsentiert, wie Daten in Adobe Experience Platform gespeichert werden.

>[!NOTE]
>
>Das ERD wie beschrieben ist eine Empfehlung dafür, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Experience Platform verwenden zu können, müssen Sie die empfohlenen Schemata und ihre Beziehungen selbst erstellen. Weitere Informationen finden Sie in den Handbüchern zur Verwaltung [Schemata](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche.

Folgende Legende verwenden, um dieses ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einer zugrunde liegenden [Experience-Datenmodell (XDM)-](../composition.md#class).
* Unter einem übergeordneten Feld eingerückte Felder stellen ein untergeordnetes Feld oder Unterfeld dar, das zur Feldergruppe des übergeordneten Felds gehört.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kundinnen und Kunden verwendet werden können, werden als „Identität“ gekennzeichnet, wobei eine dieser Eigenschaften als „primäre Identität“ markiert ist.
* Entitätsbeziehungen werden als nicht abhängig gekennzeichnet, da Cookie-basierte Ereignisse häufig nicht die Person oder Einzelperson bestimmen können, die die Transaktion durchgeführt hat.

![Ein Beispiel-ERD für ein Datenmodell der Gesundheitsbranche](../../images/industries/healthcare.png)

>[!NOTE]
>
>Jede Entität enthält ein Feld „_ID“, das das Attribut der eindeutigen Zeichenfolgenkennung (`_id`) für den betreffenden Datensatz oder das betreffende Ereignis darstellt. Dieses Feld wird verwendet, um die Eindeutigkeit des einzelnen Datensatzes oder Ereignisses nachzuverfolgen, Doppelungen von Daten zu verhindern und diese Daten in nachgelagerten Services nachzuschlagen. In einigen Fällen kann `_id` ein [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) oder ein [Globally Unique Identifier (GUID)](https://docs.microsoft.com/de-de/dotnet/api/system.guid?view=net-5.0) sein.<br><br>Es ist wichtig zu erkennen, dass **dieses Feld keine Identität repräsentiert, die mit einer Person in Verbindung steht**, sondern den Datensatz an sich. Identitätsdaten, die sich auf eine Person, ein Ereignis oder eine Geschäftseinheit beziehen, sollten stattdessen auf [Identitätsfelder](../composition.md#identity) relegiert werden, die von kompatiblen Feldergruppen bereitgestellt werden.

## [!UICONTROL Gesundheitswesen] Anwendungsfälle

In der folgenden Tabelle sind die empfohlenen Klassen und Schemafeldgruppen für mehrere gängige Anwendungsfälle im Gesundheitswesen aufgeführt.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Verbesserung der digitalen Akquise und des Erlebnisses von Verbrauchern, die Versicherungen kaufen. Zu den Beispielen gehören: <ul><li>Wenn Personen auf eine Seite zugreifen, die allgemeine Informationen enthält (z. B. Pläne, Plannamen/Ebenen, Medicaid, Wellness-Programme usw.), verstehen Sie ihr Verhalten und das, wonach sie suchen, um Werbe-E-Mails zu senden oder sie mit Anzeigen auf Drittanbieter-Plattformen anzusprechen.</li><li>Wenn Personen nach Informationen über Herzgesundheit und Impfstoff suchen, senden Sie ihnen Informationen über den Impfstoff zur Herzgesundheit, um auf die Marke aufmerksam zu machen, oder bitten Sie sie, Impfungen zu planen.</li></ul> | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Details zum versicherten Mitglied]](../../field-groups/profile/healthcare-member-details.md)</li><li>Beziehungsfeld(er), das/die zwischen `planID` Attributen und Schemata erstellt wurde(n), die die Klasse [!UICONTROL Plan] verwenden.</li></ul></li><li>**[[!UICONTROL Zahler]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Details zum Gesundheitsplan]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Anwendungsdetails]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Sitetool-Details]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL &#x200B; Details zum Kampagnen-Marketing]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| Steigerung der digitalen Akquise von Patienten durch gezielte Anzeigen auf der Grundlage früherer Online-Verhaltens- und Gesundheitsdaten. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Details zum versicherten Mitglied]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Provider]](../../classes/provider.md)**:<ul><li>[[!UICONTROL Gesundheitsdienstleister]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web-Details]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising-Details]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Verbessern Sie die Registrierung und Kontoerstellung in Gesundheitsplänen, indem Sie die Vermarktung von Versicherungen über verschiedene Kanäle verfolgen, um zu verstehen, wie ein Kunde von einem Versicherungsunternehmen erfahren hat. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Details zum versicherten Mitglied]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Zahler]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Details zum Gesundheitsplan]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web-Details]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising-Details]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Lücken im Krankenversicherungsschutz vermeiden. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Details zum versicherten Mitglied]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Details zum Gesundheitsplan]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| Werbung für Arzneimittelinformationen bei Anbietern, die Anzeigen mit direkter Kundenansprache (Direct-to-Customer, DTC) schalten. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Details zum versicherten Mitglied]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Medizin]](../../classes/medication.md)**:<ul><li>[[!UICONTROL Arzneimittel]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web-Details]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising-Details]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |

