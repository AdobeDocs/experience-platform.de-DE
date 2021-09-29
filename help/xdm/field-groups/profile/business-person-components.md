---
title: XDM Business Person Components Schema Field Group
description: Dieses Dokument bietet einen Überblick über die Schemakomponentenfeldgruppe "XDM Business Person Components".
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 5%

---

# [!UICONTROL Feldergruppe &quot;XDM Business Person ] Components&quot;(Beta)

>[!IMPORTANT]
>
>Diese Feldergruppe ist als Teil der Echtzeit-Kundendatenplattform B2B Edition verfügbar, die sich derzeit in der Betaphase befindet. Dokumentation und Funktionalität können sich ändern.

[!UICONTROL XDM Business Person ] Component ist eine Standardschemafeldgruppe für die  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) Klasse, die mehrere Quelldatensätze für eine Person und andere Attribute erfasst, die für die Personensegmentierung erforderlich sind.

Wenn ein Profil für eine Person über [Echtzeit-Kundenprofil](../../../profile/home.md) in der B2B-Ausgabe der Echtzeit-Kundendatenplattform erstellt wird, können die zum Erstellen dieses Profils verwendeten Informationen möglicherweise aus vielen Quelldatensätzen stammen. Wenn beispielsweise eine Person für zwei verschiedene Unternehmen arbeitet, erstellen viele CRM-Systeme eine absichtlich doppelte Kopie dieser Person, sodass eine Kopie mit Firma A verknüpft ist, die andere mit Firma B. Beim Importieren dieser Daten in Adobe Experience Platform wird diese Feldergruppe verwendet, um diese verschiedenen Quelldatensätze in einer Darstellung zusammenzuführen.

Die Feldergruppe stellt ein `personComponents`-Feld auf der Stammebene bereit, bei dem es sich um ein Array von Objekten handelt. Jedes Objekt im Array stellt einen anderen Quelldatensatz dar.

![](../../images/field-groups/business-person-components.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das mit der Person verknüpfte Konto. |
| `sourceConvertedContactKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für den zugehörigen Kontakt, wenn dieser Lead konvertiert wurde. |
| `sourceExternalKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das Quellsystem, aus dem die Daten der Person stammen. |
| `sourcePersonKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person. |
| `workEmail` | [[!UICONTROL E-Mail-Adresse]](../../data-types/b2b-source.md) | Die geschäftliche E-Mail-ID der Person. |
| `personGroupID` | Zeichenfolge | Eine Gruppenkennung für die Person. |
| `personScore` | Zeichenfolge | Ein von einem CRM-System für die Person generierter Wert. |
| `personSource` | Zeichenfolge | Eine eindeutige zeichenfolgenbasierte Kennung für das Quellsystem, aus dem die Daten der Person stammen. |
| `personStatus` | Zeichenfolge | Der aktuelle Marketing- oder Verkaufsstatus der Person. |
| `personType` | Zeichenfolge | Die Art der Person in einem B2B-Kontext. |
| `sourceAccountID` | Zeichenfolge | Eine eindeutige zeichenfolgenbasierte Kennung für das Konto im Quellsystem, das der Person zugeordnet ist. Dieses Feld wird vom System als Fremdschlüssel verwendet, um nach den verschiedenen Unternehmen zu suchen, für die diese Person arbeitet. |
| `sourceConvertedContactID` | Zeichenfolge | Eine eindeutige zeichenfolgenbasierte Kennung für den zugehörigen Kontakt, wenn dieser Lead konvertiert wurde. |
| `sourceExternalID` | Zeichenfolge | Eine eindeutige zeichenfolgenbasierte Kennung für das Quellsystem, aus dem die Daten der Person stammen. |
| `sourcePersonID` | Zeichenfolge | Eine eindeutige zeichenfolgenbasierte Kennung für die Person. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
