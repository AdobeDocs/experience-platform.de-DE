---
title: XDM Individual Prospect Profile Class
description: Erfahren Sie mehr über die Klasse "XDM Individual Prospect Profile"im Experience-Datenmodell (XDM).
exl-id: 10fd9d16-4123-4ad4-971f-b715231ee6a9
source-git-commit: f4ddcf14de7a5cec42b5ebc521203cfdd1498a9f
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 16%

---

# Klasse [!UICONTROL XDM Individual Prospect Profile]

Im Experience-Datenmodell (XDM) erfasst die Klasse [!UICONTROL XDM Individual Prospect Profile] Interessenten-Profile, die normalerweise von Datenpartnern bezogen werden, um die wichtigsten Anwendungsfälle für die Kundenakquise zu ermitteln.

>[!NOTE]
>
>Um ein Feld im individuellen XDM-Prospect-Profil als Entität festzulegen, müssen Sie zunächst mindestens einen Partner-ID-Namespace erstellen. Weitere Informationen zur Partner-ID finden Sie im Abschnitt [Identitätstypen](../../identity-service/features/namespaces.md).

![Das Schemadiagramm der XDM Prospect-Klasse.](../images/classes/individual-prospect-profile.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_repo` | Objekt | Mit dieser Klasse können Sie potenziellen Profilen, die von Datenanbietern bezogen werden, hinzufügen, um Anwendungsfälle für die Kundenakquise zu testen. |
| `_repo.createDate` | [!UICONTROL DateTime] | Datum und Uhrzeit des Servers, an dem die Ressource im Repository erstellt wurde. Die Erstellungszeit kann der Zeitpunkt sein, zu dem eine Asset-Datei zum ersten Mal hochgeladen wird oder ein Ordner vom Server als übergeordnetes Element eines neuen Assets erstellt wird. Die datetime-Eigenschaft sollte dem ISO 8601-Standard entsprechen. Ein Beispiel für dieses Format ist &quot;2004-10-23T12:00:00-06:00&quot;. |
| `_repo.modifyDate` | [!UICONTROL DateTime] | Das Server-Zeit (Datum und Uhrzeit), zu der die Ressource im Repository zuletzt geändert wurde, z. B. wenn eine neue Version eines Assets hochgeladen oder die untergeordnete Ressource eines Verzeichnisses hinzugefügt oder entfernt wird. Die datetime-Eigenschaft sollte dem ISO 8601-Standard entsprechen. Ein Beispiel ist „2004-10-23T12:00:“. |
| `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld vom System generiert wird, liefert es während der Datenerfassung keinen expliziten Wert. Sie können jedoch bei Bedarf Ihre eigenen eindeutigen ID-Werte angeben. |
| `createdByBatchID` | [!UICONTROL String] | Die ID des erfassten Batches, der zur Erstellung des Datensatzes geführt hat. |
| `modifiedByBatchID` | [!UICONTROL String] | Die ID des letzten erfassten Batches, der zur Aktualisierung des Datensatzes geführt hat. |
| `partnerID` | [!UICONTROL String] | Normalerweise eine eindeutige pseudonyme Kennung, die einen einzelnen Interessenten identifiziert. Weitere Informationen zur Partner-ID und zu den anderen in Adobe Experience Platform verfügbaren Identitätstypen finden Sie in der Dokumentation zu [Identitätstypen](../../identity-service/features/namespaces.md#identity-type) . |
| `repositoryCreatedBy` | [!UICONTROL String] | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | [!UICONTROL String] | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. Wenn der Datensatz erstellt wird, wird der `modifiedByUser` -Wert als `createdByUser` -Wert festgelegt. |

{style="table-layout:auto"}
