---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemas;Identitätskarte;Identitätskarte;Schema-Design;Map;Vereinigung Schema;Vereinigung
solution: Experience Platform
title: XDM Individuelle Profil-Klasse
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die XDM Individual Profil-Klasse.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
translation-type: tm+mt
source-git-commit: 612917b23d1841556a71f6378497e1d033bc3b62
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] ist eine Standard-XDM-Klasse, die eine Singular-Darstellung (oder &quot;Profil&quot;) der Attribute und Interessen von identifizierten und teilweise identifizierten Personen bildet.

Profil können von anonymen Verhaltenssignalen (z. B. Browser-Cookies) bis hin zu eindeutig identifizierten Profilen mit detaillierten Informationen wie Name, Geburtsdatum, Ort und E-Mail-Adresse reichen. Mit zunehmendem Profil wird es zu einem robusten Archiv mit persönlichen Informationen, Identitäten, Kontaktdaten und Kommunikationsvorlieben für eine Einzelperson. Weitere Informationen zur Verwendung dieser Klasse im Plattform-Ökosystem finden Sie in der [XDM-Übersicht](../home.md#data-behaviors).

Die [!DNL XDM Individual Profile]-Klasse selbst stellt mehrere systemgenerierte Werte bereit, die beim Erfassen von Daten automatisch ausgefüllt werden, während alle anderen Schema-Feldgruppen mithilfe von [kompatiblen Feldgruppen](#field-groups) hinzugefügt werden müssen:

![](../images/classes/individual-profile.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_repo` | Ein Objekt, das die folgenden [!UICONTROL DateTime]-Felder enthält: <ul><li>`createDate`: Datum und Uhrzeit der Erstellung der Ressource im Datenspeicher, z. B. wann die Daten zum ersten Mal erfasst wurden.</li><li>`modifyDate`: Datum und Uhrzeit der letzten Änderung der Ressource.</li></ul> |
| `_id` | Eine eindeutige ID für den Datensatz. Dieses Feld dient zur Verfolgung der Einzigartigkeit eines einzelnen Datensatzes, zur Vermeidung von Datenduplizierungen und zur Nachforschung dieses Datensatzes in nachgelagerten Diensten.<br><br>Es ist wichtig zu unterscheiden, dass dieses Feld  **keine Identität** darstellt, die sich auf eine Person bezieht, sondern vielmehr die Aufzeichnung der Daten selbst. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen in [Identitätsfelder](../schema/composition.md#identity) umbenannt werden. |
| `createdByBatchID` | Die ID des erfassten Stapels, die zur Erstellung des Datensatzes geführt hat. |
| `modifiedByBatchID` | Die ID des letzten erfassten Stapels, der zur Aktualisierung des Datensatzes geführt hat. |
| `personID` | Eine eindeutige Kennung für die einzelne Person, auf die sich dieser Datensatz bezieht. Dieses Feld stellt nicht unbedingt eine Identität dar, die mit der Person in Verbindung steht, es sei denn, es ist auch als [Identitätsfeld](../schema/composition.md#identity) gekennzeichnet. |
| `repositoryCreatedBy` | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. |

## Kompatible Feldgruppen {#field-groups}

>[!NOTE]
>
>Die Namen mehrerer Feldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../field-groups/name-updates.md).

Adobe bietet mehrere Standardfeldgruppen zur Verwendung mit der [!DNL XDM Individual Profile]-Klasse. Im Folgenden finden Sie eine Liste einiger häufig verwendeter Feldgruppen für die Klasse:

* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Demografische Details]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL Persönliche Kontaktangaben]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Kontaktangaben bearbeiten]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL Details zur Segmentmitgliedschaft]](../field-groups/profile/segmentation.md)

Eine vollständige Liste aller kompatiblen Feldgruppen für [!DNL XDM Individual Profile] finden Sie im [XDM GitHub Repo](https://github.com/adobe/xdm/tree/master/components/mixins/profile).
