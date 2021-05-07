---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schema;Segment;Segmentmitgliedschaft;Segmentmitgliedschaft;Schema-Design;Landkarte;Landkarte;
solution: Experience Platform
title: Schema-Feldgruppe "Details der Segmentmitgliedschaft"
topic-legacy: overview
description: In diesem Dokument erhalten Sie eine Übersicht über die Feldgruppe "Details zum Segmentmitgliedschaftsdetail"im Schema.
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 1%

---


# [!UICONTROL Feldgruppe &quot;] Details zur Segmentmitgliedschaft&quot;

>[!NOTE]
>
>Die Namen mehrerer Schema-Feldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md).

[!UICONTROL Segmentmitgliedsdetails ] sind eine Standardfeldgruppe für Schemas für die  [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Die Feldgruppe bietet ein Feld für eine einzelne Zuordnung, in dem Informationen zur Segmentmitgliedschaft erfasst werden, einschließlich der Segmente, zu denen die betreffende Person gehört, der letzten Qualifikationszeit und des Zeitpunkts, zu dem die Mitgliedschaft gültig ist, bis zu dem Zeitpunkt, zu dem sie gültig ist.

>[!WARNING]
>
>Während das Feld `segmentMembership` manuell mit dieser Feldgruppe zu Ihrem Profil-Schema hinzugefügt werden muss, sollten Sie nicht versuchen, dieses Feld manuell zu füllen oder zu aktualisieren. Das System aktualisiert die `segmentMembership`-Zuordnung für jedes Profil automatisch, wenn Segmentierungsaufträge ausgeführt werden.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `segmentMembership` | Zuordnung | Ein Map-Objekt, das die Segmentmitgliedschaften der jeweiligen Person beschreibt. Die Struktur dieses Objekts wird nachfolgend detailliert beschrieben. |

Im Folgenden finden Sie ein Beispiel für die Zuordnung `segmentMembership`, die das System für ein bestimmtes Profil aufgefüllt hat. Segmentmitgliedschaften werden nach Namensraum sortiert, wie durch die Schlüssel auf der Stammebene des Objekts angegeben. Die einzelnen Schlüssel unter jedem Namensraum stellen die IDs der Segmente dar, denen das Profil angehört. Jedes Segmentobjekt enthält mehrere Unterfelder, die weitere Details zur Mitgliedschaft bieten:

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
| `xdm:version` | Die Segmentversion, für die dieses Profil qualifiziert ist. |
| `xdm:lastQualificationTime` | Ein Zeitstempel, der angibt, wann sich dieses Profil zum letzten Mal für das Segment qualifiziert hat. |
| `xdm:validUntil` | Ein Zeitstempel, der angibt, wann die Segmentmitgliedschaft nicht mehr als gültig betrachtet werden soll. |
| `xdm:status` | Gibt an, ob die Segmentmitgliedschaft als Teil der aktuellen Anforderung ausgeführt wurde. Die folgenden Werte werden akzeptiert: <ul><li>`existing`: Das Profil war bereits vor dem Antrag Teil des Segments und bleibt weiterhin Mitglied.</li><li>`realized`: Das Profil gibt das Segment als Teil der aktuellen Anforderung ein.</li><li>`exited`: Das Profil beendet das Segment im Rahmen der aktuellen Anforderung.</li></ul> |
| `xdm:payload` | Einige Segmentmitgliedschaften beinhalten eine Payload, die zusätzliche Werte beschreibt, die direkt mit der Mitgliedschaft zusammenhängen. Für jede Mitgliedschaft kann nur eine Nutzlast eines bestimmten Typs angegeben werden. `xdm:payloadType` gibt den Nutzlasttyp (`boolean`,  `number`,  `propensity`oder  `string`) an, während seine Geschwistereigenschaft den Wert für den Nutzlasttyp bereitstellt. |

Weitere Informationen zur Feldgruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
