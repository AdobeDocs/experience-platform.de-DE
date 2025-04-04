---
title: Schemafeldgruppe „XDM-Geschäftspersonenkomponenten“
description: Erfahren Sie mehr über die Schemafeldgruppe „XDM-Geschäftspersonenkomponenten“.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 4%

---

# Schemafeldgruppe [!UICONTROL XDM-Geschäftspersonenkomponenten]

[!UICONTROL XDM Business Person Components] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md) die mehrere Quelldatensätze für eine Person und andere Attribute erfasst, die für die Personensegmentierung erforderlich sind.

Wenn ein Profil für eine Person über das [Echtzeit-Kundenprofil](../../../profile/home.md) in der B2B edition von Real-Time CDP erstellt wird, können die zum Erstellen dieses Profils verwendeten Informationen aus vielen Quelldatensätzen stammen. Wenn eine Person beispielsweise für zwei verschiedene Unternehmen arbeitet, erstellen viele CRM-Systeme eine absichtlich duplizierte Kopie dieser Person, sodass eine Kopie mit Unternehmen A verknüpft wird, während die andere mit Unternehmen B verknüpft ist. Beim Übertragen dieser Daten in Adobe Experience Platform wird diese Feldergruppe verwendet, um die verschiedenen Quelldatensätze in einer einzigen Darstellung zusammenzuführen.

Die Feldergruppe stellt ein `personComponents`-Feld auf Stammebene bereit, das ein Array von -Objekten ist. Jedes Objekt im Array stellt einen anderen Quelldatensatz dar.

>[!IMPORTANT]
>
>Sie müssen die Aufnahmemuster befolgen, wie in der [Quellendokumentation“ ](../../../rtcdp/sources/b2b.md). Andere Feldzuordnungsmethoden funktionieren nicht immer.
>
>Beispielsweise wird jedes Objekt des `personComponents`-Arrays während standardmäßiger Aufnahmemuster einzeln übermittelt und dann von Experience Platform zum Array hinzugefügt. Wenn Sie der Geschäftspersonenkomponente manuell ein Array von Objekten hinzufügen, wird ein Fehler zurückgegeben.
>Sie sollten das Dienstprogramm zur automatischen Generierung verwenden, wenn Sie Schemas für Ihre B2B-Daten erstellen. Anweisungen zur Verwendung des B2B-Namespace und [ Dienstprogramms zur automatischen Schemaerstellung finden Sie in der Dokumentation ](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md). Wenn Sie das Dienstprogramm zur automatischen Generierung nicht verwenden und Ihr Datenmodell manuell zuordnen möchten, lesen Sie unbedingt die Dokumentation zu den [Adobe Real-Time Customer Data Platform B2B edition XDM-Klassen](../../../rtcdp/schemas/b2b.md) bevor Sie Ihre Daten zuordnen.
>
>Informationen [ empfohlenen Workflows für B2B-Daten ](../../../rtcdp/b2b-tutorial.md) Sie im End-to-End-Tutorial .

![](../../images/field-groups/business-person-components.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das mit der Person verknüpfte Konto. |
| `sourceConvertedContactKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für den zugehörigen Kontakt, wenn dieser Lead konvertiert wurde. |
| `sourceExternalKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das Quellsystem, aus dem die Daten der Person stammen. |
| `sourcePersonKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person. |
| `workEmail` | [[!UICONTROL E-Mail-Adresse]](../../data-types/b2b-source.md) | Die geschäftliche E-Mail-ID der Person. |
| `personGroupID` | String | Eine Gruppenkennung für die Person. |
| `personScore` | String | Ein von einem CRM-System für die Person generierter Score. |
| `personSource` | String | Eine eindeutige, auf Zeichenfolgen basierende Kennung für das Quellsystem, aus dem die Daten der Person stammen. |
| `personStatus` | String | Der aktuelle Marketing- oder Verkaufsstatus der Person. |
| `personType` | String | Der Typ der Person in einem B2B-Kontext. |
| `sourceAccountID` | String | Eine eindeutige, auf Zeichenfolgen basierende Kennung für das Konto im Quellsystem, das mit der Person verknüpft ist. Dieses Feld wird vom System als Fremdschlüssel zum Suchen der verschiedenen Unternehmen verwendet, für die diese Person arbeitet. |
| `sourceConvertedContactID` | String | Eine eindeutige, auf Zeichenfolgen basierende Kennung für den zugehörigen Kontakt, wenn dieser Lead konvertiert wurde. |
| `sourceExternalID` | String | Eine eindeutige, auf Zeichenfolgen basierende Kennung für das Quellsystem, aus dem die Daten der Person stammen. |
| `sourcePersonID` | String | Eine eindeutige, zeichenfolgenbasierte Kennung für die Person. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
