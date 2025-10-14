---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;XDM;ExperienceEvent;Felder;Schemata;Schemata;Schemadesign;Feldergruppe;Feldergruppe;iab;tcf;Zustimmung;
solution: Experience Platform
title: IAB TCF 2.0-Einverständnis-Feldergruppe für Ereignisschemata
description: Erfahren Sie mehr über die Feldergruppe des IAB TCF 2.0-Einverständnisschemas für die XDM ExperienceEvent-Klasse.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 1%

---

# [!UICONTROL IAB TCF 2.0 Consent]-Feldergruppe für Ereignisschemata

>[!IMPORTANT]
>
>Dieses Dokument behandelt die Schemafeldgruppe [!UICONTROL IAB TCF 2.0 Consent] für die XDM ExperienceEvent-Klasse. Diese Feldergruppe sollte nur verwendet werden, wenn Sie Einverständnisänderungsereignisse im Laufe der Zeit verfolgen möchten.
>
>Beachten Sie, dass in Ereignisdaten aufgezeichnete Einverständniswerte in automatischen Erzwingungs-Workflows nicht berücksichtigt werden. Damit die automatische Durchsetzung erfolgt, müssen Einverständniswerte in die Klasse „XDM Individual Profile“ aufgenommen und für das Echtzeit-Kundenprofil aktiviert werden.
>
>Für die Feldergruppe, die für die Klasse „XDM Individual Profile“ vorgesehen ist, verweisen Sie stattdessen auf [&#x200B; folgende &#x200B;](../profile/iab.md).

[!UICONTROL IAB TCF 2.0 Consent] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), mit der eine Zeitstempelserie von IAB-Einverständniszeichenfolgen erfasst wird, um Einverständnisänderungsmuster im Zeitverlauf zu verfolgen.

![](../../images/field-groups/iab-event.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `consentStrings` | Array von [Einverständniszeichenfolgen](../../data-types/consent-string.md) | Ein Array von Einverständnis-Zeichenfolgenwerten, die mit dem Ereignis verknüpft sind. |

{style="table-layout:auto"}

Weitere Informationen zum Anwendungsfall [&#x200B; Feldergruppe finden Sie im Handbuch &#x200B;](../../../landing/governance-privacy-security/consent/iab/overview.md) IAB TCF 2.0-Unterstützung in Experience Platform . Weitere Informationen zur Feldgruppe selbst finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
