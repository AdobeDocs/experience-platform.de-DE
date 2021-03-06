---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; individuelles Profil; Felder; Schemas; Schemas; Segment; Segmentzugehörigkeit; Segmentmitgliedschaft; Schemadesign; Karte; Map;
solution: Experience Platform
title: Schemafeldgruppe "Segmentzugehörigkeitsdetails"
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Schemakonzerne "Segmentzugehörigkeitsdetails".
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: 5f28c9eceb42ee19f7a8b22604ff36f8ffbd89b1
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 6%

---


# [!UICONTROL Details zur Segmentzugehörigkeit] Schemafeldgruppe

>[!NOTE]
>
>Die Namen verschiedener Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Details zur Segmentzugehörigkeit] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). Die Feldergruppe bietet ein einzelnes Zuordnungsfeld, das Informationen zur Segmentzugehörigkeit erfasst, einschließlich der Segmente, zu denen die Person gehört, der letzten Qualifikationszeit und des Zeitpunkts, zu dem die Mitgliedschaft gültig ist, bis.

>[!WARNING]
>
>Während `segmentMembership` muss mithilfe dieser Feldergruppe manuell zum Profilschema hinzugefügt werden. Sie sollten nicht versuchen, dieses Feld manuell zu füllen oder zu aktualisieren. Das System aktualisiert automatisch die `segmentMembership` für jedes Profil zuordnen, da Segmentierungsaufträge ausgeführt werden.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `segmentMembership` | Zuordnung | Ein map -Objekt, das die Segmentmitgliedschaften des Kontakts beschreibt. Die Struktur dieses Objekts wird im Folgenden detailliert beschrieben. |

{style=&quot;table-layout:auto&quot;}

Im Folgenden finden Sie ein Beispiel `segmentMembership` zuordnen, dass das System für ein bestimmtes Profil ausgefüllt wurde. Segmentmitgliedschaften werden nach Namespace sortiert, wie durch die Schlüssel auf der Stammebene des Objekts angegeben. Die einzelnen Schlüssel unter jedem Namespace stellen wiederum die IDs der Segmente dar, denen das Profil angehört. Jedes Segmentobjekt enthält mehrere Unterfelder, die weitere Details zur Mitgliedschaft bieten:

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "existing",
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
| `xdm:version` | Die Version des Segments, für das dieses Profil qualifiziert ist. |
| `xdm:lastQualificationTime` | Ein Zeitstempel, der angibt, wann sich dieses Profil zuletzt für das Segment qualifiziert hat. |
| `xdm:validUntil` | Ein Zeitstempel, der angibt, wann die Segmentzugehörigkeit nicht mehr als gültig betrachtet werden soll. |
| `xdm:status` | Ein Zeichenfolgenfeld, das anzeigt, ob die Segmentzugehörigkeit im Rahmen der aktuellen Anforderung realisiert wurde. Folgende Werte werden akzeptiert: <ul><li>`existing`: Das Profil war bereits vor der Anfrage Teil des Segments und behält weiterhin seine Mitgliedschaft bei.</li><li>`realized`: Das Profil gibt das Segment als Teil der aktuellen Anforderung ein.</li><li>`exited`: Das Profil beendet das Segment als Teil der aktuellen Anforderung.</li></ul> |
| `xdm:payload` | Einige Segmentmitgliedschaften enthalten eine Payload, die zusätzliche Werte beschreibt, die direkt mit der Mitgliedschaft in Verbindung stehen. Für jede Mitgliedschaft kann nur eine Payload eines bestimmten Typs angegeben werden. `xdm:payloadType` gibt den Payload-Typ an (`boolean`, `number`, `propensity`oder `string`), während seine gleichrangige Eigenschaft den Wert für den Payload-Typ bereitstellt. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
