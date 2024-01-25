---
title: XDM Individual Prospect Profile Class
description: Erfahren Sie mehr über die Klasse "XDM Individual Prospect Profile"im Experience-Datenmodell (XDM).
exl-id: 10fd9d16-4123-4ad4-971f-b715231ee6a9
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 15%

---

# [!UICONTROL XDM Individual Prospect Profile] class

Im Experience-Datenmodell (XDM) wird die [!UICONTROL XDM Individual Prospect Profile] -Klasse erfasst Interessenten-Profile, die normalerweise von Datenpartnern für die wichtigsten Anwendungsfälle der Kundenakquise bezogen werden.

![Das Schemadiagramm der XDM Prospect-Klasse.](../images/classes/individual-prospect-profile.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_repo` | Objekt | Mit dieser Klasse können Sie potenziellen Profilen, die von Datenanbietern bezogen werden, hinzufügen, um Anwendungsfälle für die Kundenakquise zu testen. |
| `_repo.createDate` | [!UICONTROL DateTime] | Datum und Uhrzeit des Servers, an dem die Ressource im Repository erstellt wurde. Die Erstellungszeit kann der Zeitpunkt sein, zu dem eine Asset-Datei zum ersten Mal hochgeladen wird oder ein Ordner vom Server als übergeordnetes Element eines neuen Assets erstellt wird. Die datetime-Eigenschaft sollte dem ISO 8601-Standard entsprechen. Ein Beispiel für dieses Format ist &quot;2004-10-23T12&quot;:00:00-06:00&quot;. |
| `_repo.modifyDate` | [!UICONTROL DateTime] | Das Server-Zeit (Datum und Uhrzeit), zu der die Ressource im Repository zuletzt geändert wurde, z. B. wenn eine neue Version eines Assets hochgeladen oder die untergeordnete Ressource eines Verzeichnisses hinzugefügt oder entfernt wird. Die datetime-Eigenschaft sollte dem ISO 8601-Standard entsprechen. Ein Beispiel ist „2004-10-23T12:00:“. |
| `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemgeneriert wird, liefert es während der Datenerfassung keinen expliziten Wert. Sie können jedoch bei Bedarf Ihre eigenen eindeutigen ID-Werte angeben. |
| `createdByBatchID` | [!UICONTROL String] | Die ID des erfassten Batches, der zur Erstellung des Datensatzes geführt hat. |
| `modifiedByBatchID` | [!UICONTROL String] | Die ID des letzten erfassten Batches, der zur Aktualisierung des Datensatzes geführt hat. |
| `partnerID` | [!UICONTROL String] | Normalerweise eine eindeutige pseudonyme Kennung, die einen einzelnen Interessenten identifiziert. Siehe die Dokumentation unter [Identitätstypen](../../identity-service/features/namespaces.md#identity-type) , um mehr über die Partner-ID und die anderen Identitätstypen zu erfahren, die in Adobe Experience Platform verfügbar sind. |
| `repositoryCreatedBy` | [!UICONTROL String] | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | [!UICONTROL String] | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. Wenn der Datensatz erstellt wird, wird die `modifiedByUser` -Wert festgelegt ist, wird als `createdByUser` -Wert. |

{style="table-layout:auto"}
