---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;XDM;individuelles Profil;Felder;Schemas;Schemas;Identitätszuordnung;Identitätszuordnung;Schema-Design;Map;Map;Vereinigungsschema;Vereinigungsschema
solution: Experience Platform
title: XDM Individual Profile Class
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Klasse "XDM Individual Profile".
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: ecb9c9a4158f3d2981ab60ee3bf419464ac7b8f1
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die eine Einzeldarstellung (oder ein &quot;Profil&quot;) einer einzelnen Person bildet. Insbesondere erfasst die Klasse (und ihre kompatiblen Mixins) die Attribute und Interessen sowohl identifizierter als auch nur teilweise identifizierter Personen, die mit Ihrer Marke interagieren.

Profile können von anonymen Verhaltenssignalen (wie Browser-Cookies) bis hin zu hoch identifizierten Profilen mit detaillierten Informationen wie Name, Geburtsdatum, Ort und E-Mail-Adresse reichen. Mit zunehmendem Profil wird es zu einem robusten Repository mit personenbezogenen Daten, Identitäten, Kontaktdaten und Kommunikationseinstellungen für eine Person. Weiterführende Informationen zur Verwendung dieser Klasse im Platform-Ökosystem finden Sie in der [XDM-Übersicht](../home.md#data-behaviors).

Die [!DNL XDM Individual Profile]-Klasse stellt mehrere systemgenerierte Werte bereit, die bei der Datenerfassung automatisch ausgefüllt werden, während alle anderen Felder durch die Verwendung von [kompatiblen Schemafeldgruppen](#field-groups) hinzugefügt werden müssen:

![](../images/classes/individual-profile.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_repo` | Ein Objekt, das die folgenden [!UICONTROL DateTime]-Felder enthält: <ul><li>`createDate`: Datum und Uhrzeit der Erstellung der Ressource im Datenspeicher, z. B. Zeitpunkt der ersten Datenerfassung.</li><li>`modifyDate`: Datum und Uhrzeit der letzten Änderung der Ressource.</li></ul> |
| `_id` | Eine eindeutige Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, eine Duplizierung von Daten zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen. In einigen Fällen kann `_id` eine [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) oder [Globally Unique Identifier (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0) sein.<br><br>Wenn Sie Daten aus einer Quellverbindung streamen oder direkt aus einer Parquet-Datei erfassen, sollten Sie diesen Wert generieren, indem Sie eine bestimmte Kombination von Feldern miteinander verknüpfen, die den Datensatz eindeutig machen, z. B. eine primäre ID, einen Zeitstempel, einen Datensatztyp usw. Der verkettete Wert muss eine `uri-reference` formatierte Zeichenfolge sein, d. h. alle Doppelpunkt-Zeichen müssen entfernt werden. Danach sollte der verkettete Wert mit SHA-256 oder einem anderen Algorithmus Ihrer Wahl gehasht werden.<br><br>Es ist wichtig zu unterscheiden, dass  **dieses Feld keine Identität darstellt, die mit einer Person** in Verbindung steht, sondern vielmehr den Datensatz selbst. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen auf [Identitätsfelder](../schema/composition.md#identity) beschränkt werden, die von kompatiblen Feldergruppen bereitgestellt werden. |
| `createdByBatchID` | Die ID des erfassten Batches, der zur Erstellung des Datensatzes geführt hat. |
| `modifiedByBatchID` | Die ID des letzten erfassten Batches, der zur Aktualisierung des Datensatzes geführt hat. |
| `personID` | Eine eindeutige Kennung für die Person, auf die sich dieser Datensatz bezieht. Dieses Feld stellt nicht unbedingt eine mit der Person verwandte Identität dar, es sei denn, es ist auch als [Identitätsfeld](../schema/composition.md#identity) gekennzeichnet. |
| `repositoryCreatedBy` | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. |

{style=&quot;table-layout:auto&quot;}

## Kompatible Feldergruppen {#field-groups}

>[!NOTE]
>
>Die Namen mehrerer Feldergruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../field-groups/name-updates.md) .

Adobe stellt mehrere Standardfeldgruppen für die Verwendung mit der Klasse [!DNL XDM Individual Profile] bereit. Im Folgenden finden Sie eine Liste einiger häufig verwendeter Feldergruppen für die Klasse:

* [[!UICONTROL Demografische Details]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Treuedetails]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Persönliche Kontaktangaben]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Datenschutz/Personalisierung/Marketing-Voreinstellungen (Einverständnis)]](../field-groups/profile/consents.md)
* [[!UICONTROL Details zur Segmentzugehörigkeit]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Kontaktangaben für Arbeitskontakte]](../field-groups/profile/work-contact-details.md)

Eine vollständige Liste aller kompatiblen Feldergruppen für [!DNL XDM Individual Profile] finden Sie im [XDM GitHub-Repository](https://github.com/adobe/xdm/tree/master/components/mixins/profile).
