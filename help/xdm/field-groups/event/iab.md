---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; iab; tcf; Einverständnis;
solution: Experience Platform
title: IAB TCF 2.0-Gruppe für Einverständnisschema-Feld
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die IAB TCF 2.0-Schemafeldgruppe für Einwilligungen für die XDM ExperienceEvent-Klasse.
source-git-commit: 7a0ac3970713e95438c6f0fdbd6175545ea7fdd0
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---


# [!UICONTROL IAB TCF 2.0-] Feldergruppe &quot;Einwilligungsschema&quot;

>[!IMPORTANT]
>
>Dieses Dokument behandelt die Schemafeldgruppe [!UICONTROL IAB TCF 2.0 Consent] für die XDM ExperienceEvent-Klasse. Diese Feldergruppe sollte nur verwendet werden, wenn Sie Zustimmungsänderungsereignisse im Laufe der Zeit verfolgen möchten.
>
>Beachten Sie, dass in Ereignisdaten aufgezeichnete Zustimmungswerte in automatischen Durchsetzungs-Workflows nicht berücksichtigt werden. Damit eine automatische Durchsetzung erfolgt, müssen Zustimmungswerte in die Klasse &quot;XDM Individual Profile&quot;aufgenommen und für Echtzeit-Kundenprofil aktiviert werden.
>
>Die Feldergruppe, die für die Klasse &quot;XDM Individual Profile&quot;vorgesehen ist, finden Sie stattdessen im folgenden [Dokument](../profile/iab.md) .

[!UICONTROL IAB TCF 2.0 ] Konfiguriert eine Schemafeldgruppe für die  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) Klasse, die zum Erfassen einer IAB-Zustimmungszeichenfolge mit Zeitstempel verwendet wird, um Zustimmungsänderungen im Laufe der Zeit zu verfolgen.

![](../../images/field-groups/iab-event.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `consentStrings` | Array von [Einverständniszeichenfolgen](../../data-types/consent-string.md) | Ein Array von Zustimmungszeichenfolgenwerten, die mit dem Ereignis verknüpft sind. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Anwendungsfall dieser Feldergruppe finden Sie im Handbuch zur [IAB TCF 2.0-Unterstützung in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) . Weitere Informationen zur Feldergruppe selbst finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
