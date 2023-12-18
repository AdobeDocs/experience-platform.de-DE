---
title: Anbieterklasse
description: Erfahren Sie mehr über die Provider-Klasse im Experience-Datenmodell (XDM).
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 4%

---

# [!UICONTROL Anbieter] class

Im Experience-Datenmodell (XDM) wird die [!UICONTROL Anbieter] -Klasse erfasst den Mindestsatz von Eigenschaften, die eine Anbietergeschäftseinheit definieren (z. B. einen Gesundheitsdienstleister oder einen Versicherer).

![Klassenstruktur](../images/classes/provider.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Personenname]](../data-types/person-name.md) | Der Name des Anbieters. |
| `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemgeneriert ist, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten. |
| `providerId` | [!UICONTROL String] | Eine eindeutige Kennung für den Provider. |

{style="table-layout:auto"}

Die Klasse kann mit der [[!UICONTROL Gesundheitsdienstleister] Feldergruppe](../field-groups/provider/healthcare-provider.md) weitere Informationen über einen Gesundheitsdienstleister.
