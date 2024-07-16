---
title: Datenmodell der Gesundheitsbranche
description: Zeigen Sie ein Entitätsbeziehungsdiagramm (ERD) an, das ein standardisiertes Datenmodell für die Gesundheitsbranche beschreibt. Dieses Datenmodell ist mit dem Experience-Datenmodell (XDM) für die Verwendung in Adobe Experience Platform kompatibel.
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 8%

---

# [!UICONTROL Das branchenspezifische Datenmodell &quot;Healthcare]&quot;

Das folgende Entitätsbeziehungsdiagramm (ERD) stellt ein standardisiertes Datenmodell für die Gesundheitsbranche dar. Der ERD wird absichtlich denormalisiert und unter Berücksichtigung der Speicherung von Daten in Adobe Experience Platform präsentiert.

>[!NOTE]
>
>Der ERD wie beschrieben ist eine Empfehlung, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Platform nutzen zu können, müssen Sie die empfohlenen Schemas und deren Beziehungen selbst erstellen. Weitere Informationen finden Sie in den Handbüchern zum Verwalten von [Schemas](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche.

Verwenden Sie die folgende Legende, um diese ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einer zugrunde liegenden [Erlebnis-Datenmodell (XDM)-Klasse](../composition.md#class).
* Für eine bestimmte Entität stellt jede in **fett** markierte Zeile eine Feldergruppe oder einen Datentyp dar, wobei die entsprechenden Felder unten in unfettetem Text aufgeführt sind.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kunden verwendet werden können, werden als &quot;Identität&quot;gekennzeichnet, wobei eine dieser Eigenschaften als &quot;primäre Identität&quot;markiert ist.
* Entitätsbeziehungen werden als nicht abhängig markiert, da Cookie-basierte Ereignisse häufig nicht die Person oder Person bestimmen können, die die Transaktion getätigt hat.

![Bild mit dem Entitätsbeziehungsdiagramm für das Datenmodell der Gesundheitsbranche](../../images/industries/healthcare.png)

>[!NOTE]
>
>Jede Entität enthält ein Feld &quot;_ID&quot;, das das Attribut der eindeutigen Zeichenfolgenkennung (`_id`) für den betreffenden Datensatz oder das betreffende Ereignis darstellt. Dieses Feld wird verwendet, um die Eindeutigkeit des einzelnen Datensatzes oder Ereignisses zu verfolgen, um doppelte Daten zu verhindern und diese Daten in nachgelagerten Diensten nachzuschlagen. In einigen Fällen kann `_id` ein [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) oder ein [Globally Unique Identifier (GUID)](https://docs.microsoft.com/de-de/dotnet/api/system.guid?view=net-5.0) sein.<br><br>Es ist wichtig zu erkennen, dass **dieses Feld keine Identität repräsentiert, die mit einer Person in Verbindung steht**, sondern den Datensatz an sich. Identitätsdaten, die sich auf eine Person, ein Ereignis oder eine Geschäftsentität beziehen, sollten stattdessen auf [Identitätsfelder](../composition.md#identity) beschränkt werden, die von kompatiblen Feldergruppen bereitgestellt werden.

## [!UICONTROL Anwendungsfälle für das Gesundheitswesen]

In der folgenden Tabelle werden die empfohlenen Klassen und Schemafeldgruppen für verschiedene gängige Anwendungsfälle der Gesundheitsfürsorge beschrieben.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Verbesserung der digitalen Akquise und der Erfahrung bei Verbrauchern, die Versicherungen einkaufen. Zu den Beispielen gehören: <ul><li>Wenn Benutzer auf eine Seite zugreifen, die allgemeine Informationen enthält (z. B. Pläne, Planungsnamen/-stufen, Medikamente, Wellness-Programme usw.), verstehen sie ihr Verhalten und was sie suchen, um Werbe-E-Mails zu senden oder sie mit Anzeigen auf Drittanbieter-Plattformen anzusprechen.</li><li>Wenn Menschen nach Informationen über Herzgesundheit und Impfstoff suchen, senden Sie ihnen impfstoffbezogene Informationen über die Herzgesundheit, um Markenbewusstsein zu schaffen, oder bitten Sie sie, Impfstoffe zu planen.</li></ul> | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Details für Mitarbeiter im Gesundheitswesen]](../../field-groups/profile/healthcare-member-details.md)</li><li>Beziehungsfeld(e) zwischen `planID` Attributen und Schemas, die die Klasse [!UICONTROL Plan] verwenden.</li></ul></li><li>**[[!UICONTROL Player]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Details zum Gesundheitsplan]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Anwendungsdetails]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL SiteTool-Details]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  Marketingdetails der Kampagne]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| Steigerung der digitalen Akquise von Patienten durch gezielte Anzeigen auf der Grundlage von früheren Online-Verhaltensdaten und Gesundheitsdaten. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Details für Mitarbeiter im Gesundheitswesen]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Provider]](../../classes/provider.md)**:<ul><li>[[!UICONTROL Gesundheitsdienstleister]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web-Details]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising-Details]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Verbesserung der Registrierung und Kontoerstellung in Gesundheitsplänen durch die Verfolgung der Vermarktung von Versicherungen über verschiedene Kanäle, um zu verstehen, wie ein Kunde über ein Versicherungsunternehmen erfuhr. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Details für Mitarbeiter im Gesundheitswesen]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Player]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Details zum Gesundheitsplan]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web-Details]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising-Details]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Vermeiden Sie Versäumnisse bei der Krankenversicherung. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Details für Mitarbeiter im Gesundheitswesen]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Details zum Gesundheitsplan]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| Fördern Sie Informationen zu Arzneimitteln an Anbieter mithilfe von Direktwerbung (Direct-to-Customer, DTC). | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Details für Mitarbeiter im Gesundheitswesen]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Meditation]](../../classes/medication.md)**:<ul><li>[[!UICONTROL Gesundheitsmedikament]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web-Details]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising-Details]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
