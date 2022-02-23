---
title: Schlüssel-Wert-Paar-Datentyp
description: Dieses Dokument bietet einen Überblick über den Datentyp "Key Value Pair Experience Data Model (XDM)".
source-git-commit: bf815eb014dc87f74ba3d42478eadcb1e8144c3c
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 7%

---

# [!UICONTROL Schlüssel-Wert-Paar] Datentyp

[!UICONTROL Schlüssel-Wert-Paar] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die Details eines generischen Schlüssel-Wert-Paares erfasst. Dieser Datentyp wird im [[!UICONTROL Adobe Analytics ExperienceEvent Full Extension] Feldergruppe](../field-groups/event/analytics-full-extension.md) um die Array-Elemente einer Listenvariablen zu beschreiben.

![Schlüsselwertpaarstruktur](../images/data-types/key-value-pair.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `key` | Zeichenfolge | Ein Schlüssel (Name) für eine generische Variable oder einen allgemeinen Wert. |
| `value` | Zeichenfolge | Der -Wert der -Variablen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie unter [das öffentliche XDM-Repository](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
