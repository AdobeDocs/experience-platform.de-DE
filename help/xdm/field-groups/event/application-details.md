---
title: Feldgruppe "Anwendungsdetails"
description: Erfahren Sie mehr über die Feldergruppe Anwendungsdetails .
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 4%

---

# [!UICONTROL Anwendungsdetails] Schemafeldgruppe

[!UICONTROL Anwendungsdetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Die Feldergruppe stellt eine einzelne `application` -Objekt zu einem Schema, das anwendungsbezogene Details wie Abstürze, Nutzung von Funktionen, Starts und Aktualisierungen erfasst.

![](../../images/field-groups/application-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `application` | [[!UICONTROL Programm]](../../data-types/financial-account.md) | Erfasst Anwendungsinformationen zu einem Ereignis, einschließlich Name der Anwendung, Anwendungsversion, Installationen, Starts, Abstürze und Schließungen. Dabei kann es sich entweder um die Anwendung handeln, auf die das Ereignis abzielt (z. B. das Ziel einer Push-Benachrichtigung, die gesendet wird), oder um die Anwendung, die das Ereignis auslöst (z. B. ein Klick oder eine Anmeldung). |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
