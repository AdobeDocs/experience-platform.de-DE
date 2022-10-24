---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;XDM;individuelles Profil;Felder;Schemas;Schemas;Identitätszuordnung;Identitätszuordnung;Schema-Design;Map;Map;Vereinigungsschema;Vereinigungsschema
solution: Experience Platform
title: XDM Individual Profile Class
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Klasse "XDM Individual Profile".
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 32%

---

# [!DNL XDM Individual Profile]-Klasse:

[!DNL XDM Individual Profile] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die eine Einzeldarstellung (oder ein &quot;Profil&quot;) einer einzelnen Person bildet. Insbesondere erfasst die Klasse (und ihre kompatiblen Feldergruppen) die Attribute und Interessen sowohl identifizierter als auch nur teilweise identifizierter Personen, die mit Ihrer Marke interagieren.

Profile können von anonymen Verhaltenssignalen (wie Browser-Cookies) bis hin zu hoch identifizierten Profilen mit detaillierten Informationen wie Name, Geburtsdatum, Ort und E-Mail-Adresse reichen. Mit zunehmendem Profil wird es zu einem robusten Repository mit personenbezogenen Daten, Identitäten, Kontaktdaten und Kommunikationseinstellungen für eine Person. Weitere wichtige Informationen zur Verwendung dieser Klasse im Platform-Ökosystem finden Sie im Abschnitt [XDM-Übersicht](../home.md#data-behaviors).

Die [!DNL XDM Individual Profile] -Klasse selbst stellt mehrere systemgenerierte Werte bereit, die automatisch ausgefüllt werden, wenn Daten erfasst werden, während alle anderen Felder durch Verwendung von [kompatible Schemafeldgruppen](#field-groups):

![](../images/classes/individual-profile.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_repo` | Ein Objekt, das Folgendes enthält: [!UICONTROL DateTime] -Felder: <ul><li>`createDate`: Datum und Uhrzeit der Erstellung der Ressource im Datenspeicher, z. B. Zeitpunkt der ersten Datenerfassung.</li><li>`modifyDate`: Datum und Uhrzeit der letzten Änderung der Ressource.</li></ul> |
| `_id` | Eine eindeutige Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, eine Duplizierung von Daten zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen. In einigen Fällen kann `_id` ein [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) oder ein [Globally Unique Identifier (GUID)](https://docs.microsoft.com/de-de/dotnet/api/system.guid?view=net-5.0) sein.<br><br>Wenn Sie Daten aus einer Quellverbindung streamen oder direkt aus einer Parquet-Datei erfassen, sollten Sie diesen Wert generieren, indem Sie eine bestimmte Kombination von Feldern miteinander verknüpfen, die den Datensatz eindeutig machen, z. B. eine primäre ID, einen Zeitstempel, einen Datensatztyp usw. Der verkettete Wert muss eine formatierte Zeichenfolge des Typs `uri-reference` sein, was bedeutet, dass alle Doppelpunkt-Zeichen entfernt werden müssen. Danach sollte der verkettete Wert mit SHA-256 oder einem anderen Algorithmus Ihrer Wahl gehasht werden.<br><br>Es ist wichtig zu erkennen, dass **dieses Feld keine Identität repräsentiert, die mit einer Person in Verbindung steht**, sondern den Datensatz an sich. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen auf [Identitätsfelder](../schema/composition.md#identity) relegiert werden, die von kompatiblen Feldergruppen bereitgestellt werden. |
| `createdByBatchID` | Die ID des erfassten Batches, der zur Erstellung des Datensatzes geführt hat. |
| `modifiedByBatchID` | Die ID des letzten erfassten Batches, der zur Aktualisierung des Datensatzes geführt hat. |
| `personID` | Eine eindeutige Kennung für die Person, auf die sich dieser Datensatz bezieht. Dieses Feld muss nicht unbedingt eine mit der Person verwandte Identität darstellen, es sei denn, es ist auch als [Identitätsfeld](../schema/composition.md#identity). |
| `repositoryCreatedBy` | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. |

{style=&quot;table-layout:auto&quot;}

## Kompatible Feldergruppen {#field-groups}

>[!NOTE]
>
>Die Namen mehrerer Feldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../field-groups/name-updates.md).

Adobe bietet mehrere Standardfeldgruppen zur Verwendung mit der [!DNL XDM Individual Profile]-Klasse. Im Folgenden finden Sie eine Liste einiger häufig verwendeter Feldergruppen für die Klasse:

* [[!UICONTROL Einverständnis und Voreinstellungen]](../field-groups/profile/consents.md)
* [[!UICONTROL Demografische Details]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Treuedetails]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Persönliche Kontaktdaten]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Details zur Segmentzugehörigkeit]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Telekom-Abonnement]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL Details zu Arbeitskontakten]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL XDM-Geschäftspersonenkomponenten]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL XDM-Geschäftspersonendetails]](../field-groups/profile/business-person-details.md)\*

*\*Diese Feldergruppe steht nur Organisationen zur Verfügung, die Zugriff auf die B2B-Edition von Adobe Real-time Customer Data Platform haben.*

Eine vollständige Liste aller kompatiblen Feldergruppen für [!DNL XDM Individual Profile], siehe [XDM GitHub-Repository](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
