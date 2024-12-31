---
title: Provider-Klasse
description: Erfahren Sie mehr über die Provider-Klasse im Experience-Datenmodell (XDM).
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 4%

---

# [!UICONTROL Provider]-Klasse

Im Experience-Datenmodell (XDM) erfasst die [!UICONTROL Provider]-Klasse den Mindestsatz von Eigenschaften, die eine Geschäftsentität eines Anbieters definieren (z. B. einen Gesundheitsdienstleister oder einen Versicherungsanbieter).

![Klassenstruktur](../images/classes/provider.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Personenname]](../data-types/person-name.md) | Der Name des Anbieters. |
| `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes nachzuverfolgen, Doppelungen von Daten zu verhindern und diesen Datensatz in nachgelagerten Services nachzuschlagen.<br><br>Da dieses Feld systemgeneriert ist, wird bei der Datenaufnahme kein expliziter Wert bereitgestellt. Sie können jedoch auch weiterhin eigene eindeutige ID-Werte angeben, wenn Sie dies wünschen. |
| `providerId` | [!UICONTROL String] | Eine eindeutige Kennung für den Provider. |

{style="table-layout:auto"}

Die Klasse kann mit der Feldergruppe [[!UICONTROL Gesundheitsdienstleister] erweitert werden, ](../field-groups/provider/healthcare-provider.md) weitere Details zu einem Gesundheitsdienstleister zu beschreiben.
