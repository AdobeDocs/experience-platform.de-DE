---
solution: Experience Platform
title: Schemafeldgruppe für Segmentzugehörigkeitsdetails
description: Erfahren Sie mehr über die Schemafeldgruppe „Details zur Segmentzugehörigkeit“.
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 20%

---


# [!UICONTROL Details zur Segmentzugehörigkeit] Schemafeldgruppe

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Details zur Segmentzugehörigkeit] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Die Feldergruppe bietet ein einzelnes Zuordnungsfeld, das Informationen zur Segmentzugehörigkeit erfasst, einschließlich der Zugehörigkeit zu welchen Segmenten, der letzten Qualifikationszeit und der Gültigkeitsdauer der Zugehörigkeit.

>[!WARNING]
>
>Während das `segmentMembership` Feld manuell mithilfe dieser Feldergruppe zu Ihrem Profilschema hinzugefügt werden muss, sollten Sie nicht versuchen, dieses Feld manuell auszufüllen oder zu aktualisieren. Das System aktualisiert automatisch die `segmentMembership` für jedes Profil, wenn Segmentierungsaufträge ausgeführt werden.

![Profilsegmentierung](../../images/data-types/profile-segmentation.png){width=400}

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `segmentMembership` | Zuordnung | Ein Zuordnungs-Objekt, das die Segmentzugehörigkeiten des Kontakts beschreibt. Die Struktur dieses Objekts wird nachfolgend detailliert beschrieben. |

{style="table-layout:auto"}

Im Folgenden finden Sie ein Beispiel `segmentMembership` Zuordnung, die das System für ein bestimmtes Profil ausgefüllt hat. Segmentzugehörigkeiten werden nach Namespace sortiert, wie durch die Stammschlüssel des -Objekts angegeben. Die einzelnen Schlüssel unter jedem Namespace stellen wiederum die IDs der Segmente dar, denen das Profil angehört. Jedes Segmentobjekt enthält mehrere Unterfelder, die weitere Details zur Mitgliedschaft bereitstellen:

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadBooleanValue": true,
          "xdm:payloadType": "boolean"
        }
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "xdm:version": "3",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2018-04-27T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadPropensityValue": 0.5,
          "xdm:payloadType": "propensity"
        }
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "xdm:version": "1",
        "xdm:lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "xdm:validUntil": "2017-12-26T15:52:25+00:00",
        "xdm:status": "exited"
      }
    }
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm:version` | Die Version des Segments, für das sich dieses Profil qualifiziert hat. |
| `xdm:lastQualificationTime` | Ein Zeitstempel, der angibt, wann sich dieses Profil zuletzt für das Segment qualifiziert hat. |
| `xdm:validUntil` | Ein Zeitstempel, der angibt, wann die Segmentzugehörigkeit nicht mehr als gültig angenommen werden soll. Wenn dieses Feld nicht festgelegt ist, wird die Segmentzugehörigkeit für externe Zielgruppen ab dem `lastQualificationTime` nur für 30 Tage beibehalten. |
| `xdm:status` | Ein Zeichenfolgenfeld, das anzeigt, ob die Segmentzugehörigkeit im Rahmen der aktuellen Anfrage realisiert wurde. Folgende Werte werden akzeptiert: <ul><li>`realized`: Das Profil ist für das Segment qualifiziert.</li><li>`exited`: Das Profil verlässt das Segment als Teil der aktuellen Anfrage.</li></ul> |
| `xdm:payload` | Einige Segmentzugehörigkeiten enthalten eine Payload, die zusätzliche Werte beschreibt, die direkt mit der Zugehörigkeit zusammenhängen. Pro Mitgliedschaft kann nur eine Payload eines bestimmten Typs bereitgestellt werden. `xdm:payloadType` gibt den Payload-Typ an (`boolean`, `number`, `propensity` oder `string`), während seine gleichrangige -Eigenschaft den Wert für den Payload-Typ angibt. |

{style="table-layout:auto"}

>[!NOTE]
>
>Jede Segmentzugehörigkeit, die sich basierend auf dem `lastQualificationTime` für mehr als 30 Tage im `exited` befindet, wird gelöscht.

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
