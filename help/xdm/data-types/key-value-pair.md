---
title: Datentyp „Schlüssel-Wert-Paar“
description: Dieses Dokument bietet einen Überblick über den Datentyp „Schlüssel-Wert-Paar-Experience-Datenmodell (XDM)“.
exl-id: 2a1a7537-9019-4cf2-bfa1-9c760f9656dd
source-git-commit: 1d023ce6184e54693401eb68a04ceeb1464dcaa0
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 100%

---

# Datentyp [!UICONTROL Schlüssel-Wert-Paar]

[!UICONTROL Schlüssel-Wert-Paar] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die Details eines generischen Schlüssel-Wert-Paares erfasst. Dieser Datentyp wird in der [[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]-Feldgruppe](../field-groups/event/analytics-full-extension.md) verwendet, um die Array-Elemente einer Listenvariablen zu beschreiben.

![Struktur eines Schlüssel-Wert-Paares](../images/data-types/key-value-pair.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `key` | Zeichenfolge | Ein Schlüssel (Name) für eine generische Variable oder einen allgemeinen Wert. |
| `value` | Zeichenfolge | Der Wert der Variablen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
