---
title: XDM Business Person Components Schema Field Group
description: Dieses Dokument bietet einen Überblick über die Schemakomponentenfeldgruppe "XDM Business Person Components".
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 6%

---

# [!UICONTROL XDM-Geschäftspersonenkomponenten] Schemafeldgruppe

[!UICONTROL XDM-Geschäftspersonenkomponenten] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) , das mehrere Quelldatensätze für eine Person und andere Attribute erfasst, die für die Personensegmentierung erforderlich sind.

Wenn ein Profil für eine Person durch erstellt wird [Echtzeit-Kundenprofil](../../../profile/home.md) in der B2B-Ausgabe von Real-Time CDP können die zur Erstellung dieses Profils verwendeten Informationen möglicherweise aus vielen Quelldatensätzen stammen. Wenn beispielsweise eine Person für zwei verschiedene Unternehmen arbeitet, erstellen viele CRM-Systeme eine absichtlich doppelte Kopie dieser Person, sodass eine Kopie mit Firma A verknüpft ist, die andere mit Firma B. Beim Importieren dieser Daten in Adobe Experience Platform wird diese Feldergruppe verwendet, um diese verschiedenen Quelldatensätze in einer Darstellung zusammenzuführen.

Die Feldergruppe stellt eine Stammebene bereit `personComponents` -Feld, das ein Array von Objekten ist. Jedes Objekt im Array stellt einen anderen Quelldatensatz dar.

>[!IMPORTANT]
>
>Sie müssen die Aufnahmemuster befolgen, wie im Abschnitt [Quelldokumentation](../../../rtcdp/sources/b2b.md). Andere Feldzuordnungsmethoden funktionieren nicht immer.
>
>Beispielsweise jedes Objekt der `personComponents` -Array wird einzeln während standardmäßigen Erfassungsmustern gesendet und dann von Platform zum Array hinzugefügt. Wenn Sie der Business Person-Komponente manuell ein Array von Objekten hinzufügen, wird ein Fehler zurückgegeben.
>Sie sollten beim Erstellen von Schemas für Ihre B2B-Daten das Dienstprogramm zur automatischen Generierung verwenden. Anweisungen zur Verwendung der [B2B-Namespace- und Schema-Dienstprogramm zur automatischen Generierung](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md). Wenn Sie das Dienstprogramm zur automatischen Generierung nicht verwenden und Ihr Datenmodell manuell zuordnen möchten, lesen Sie die Dokumentation im Abschnitt [Adobe Real-time Customer Data Platform B2B Edition XDM-Klassen](../../../rtcdp/schemas/b2b.md) vor der Zuordnung Ihrer Daten.
>
>Siehe [End-to-End-Tutorial](../../../rtcdp/b2b-tutorial.md) für Informationen zu empfohlenen Workflows für B2B-Daten.

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

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
