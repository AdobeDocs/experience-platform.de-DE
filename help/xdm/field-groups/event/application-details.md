---
title: Feldgruppe "Anwendungsdetails"
description: Dieses Dokument bietet einen Überblick über die Feldergruppe Anwendungsdetails .
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 5%

---

# [!UICONTROL Anwendungsdetails] Schemafeldgruppe

[!UICONTROL Anwendungsdetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Die Feldergruppe stellt eine `application` -Objekt zu einem Schema, das anwendungsbezogene Details wie Abstürze, Nutzung von Funktionen, Starts und Aktualisierungen erfasst.

![](../../images/field-groups/application-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `application` | [[!UICONTROL Programm]](../../data-types/financial-account.md) | Erfasst Anwendungsinformationen zu einem Ereignis, einschließlich des Namens der Anwendung, der Anwendungsversion, Installationen, Starts, Abstürze und Schließungen. Dabei kann es sich entweder um die Anwendung handeln, auf die das Ereignis abzielt (z. B. das Ziel einer Push-Benachrichtigung, die gesendet wird), oder um die Anwendung, die das Ereignis auslöst (z. B. ein Klick oder eine Anmeldung). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
