---
title: Schemafeldgruppe „Anwendungsdetails“
description: Erfahren Sie mehr über die Schemafeldgruppe „Anwendungsdetails“.
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 3%

---

# [!UICONTROL Anwendungsdetails] Schemafeldgruppe

[!UICONTROL Anwendungsdetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md). Die Feldergruppe stellt ein einzelnes `application` für ein Schema bereit, das anwendungsbezogene Details wie Abstürze, Funktionsnutzung, Starts und Upgrades erfasst.

![](../../images/field-groups/application-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `application` | [[!UICONTROL Anwendung]](../../data-types/financial-account.md) | Erfasst Anwendungsinformationen zu einem Ereignis, einschließlich des Namens der Anwendung, der Anwendungsversion, Installationen, Starts, Abstürze und Schließungen. Dabei kann es sich entweder um die Anwendung handeln, auf die das Ereignis abzielt (z. B. das Ziel für den Versand einer Push-Benachrichtigung), oder um die Anwendung, die das Ereignis auslöst (z. B. ein Klick oder eine Anmeldung). |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie unter [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
