---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;Schemas;Schemas;Schema-Design;Feldergruppe;Feldergruppe;iab;tcf;consent;
solution: Experience Platform
title: IAB TCF 2.0-Feldergruppe für Einverständniserklärungen für Ereignisschemata
description: Erfahren Sie mehr über die Feldgruppe des IAB TCF 2.0-Einverständnisschemas für die XDM ExperienceEvent-Klasse.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# [!UICONTROL IAB TCF 2.0-Zustimmung] Feldergruppe für Ereignisschemata

>[!IMPORTANT]
>
>Dieses Dokument behandelt die [!UICONTROL IAB TCF 2.0-Zustimmung] Schemafeldgruppe für die XDM ExperienceEvent-Klasse. Diese Feldergruppe sollte nur verwendet werden, wenn Sie Zustimmungsänderungsereignisse im Laufe der Zeit verfolgen möchten.
>
>Beachten Sie, dass in Ereignisdaten aufgezeichnete Zustimmungswerte in automatischen Durchsetzungs-Workflows nicht berücksichtigt werden. Damit die automatische Durchsetzung erfolgt, müssen Zustimmungswerte in die Klasse &quot;XDM Individual Profile&quot;aufgenommen und für das Echtzeit-Kundenprofil aktiviert werden.
>
>Die Feldergruppe, die für die Klasse &quot;XDM Individual Profile&quot;vorgesehen ist, finden Sie im Folgenden. [Dokument](../profile/iab.md) anstatt.

[!UICONTROL IAB TCF 2.0-Zustimmung] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) wird verwendet, um IAB-Zustimmungszeichenfolgen mit Zeitstempel zu erfassen, um Zustimmungsänderungen im Laufe der Zeit zu verfolgen.

![](../../images/field-groups/iab-event.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `consentStrings` | Array von [Einverständniszeichenfolgen](../../data-types/consent-string.md) | Ein Array von Zustimmungszeichenfolgenwerten, die mit dem Ereignis verknüpft sind. |

{style="table-layout:auto"}

Siehe Handbuch unter [IAB TCF 2.0-Unterstützung in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) für weitere Informationen zum Anwendungsfall dieser Feldergruppe. Weitere Informationen zur Feldergruppe selbst finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
