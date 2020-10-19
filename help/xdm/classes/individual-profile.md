---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: XDM Individuelle Profil-Klasse
topic: overview
description: Dieses Dokument bietet einen Überblick über die XDM Individual Profil-Klasse.
translation-type: tm+mt
source-git-commit: b7b57c0b70b1af3a833f0386bc809bb92c9b50f8
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] ist eine Standard-XDM-Klasse, die eine Singular-Darstellung (oder &quot;Profil&quot;) der Attribute und Interessen von identifizierten und teilweise identifizierten Personen bildet.

Profil können von anonymen Verhaltenssignalen (z. B. Browser-Cookies) bis hin zu eindeutig identifizierten Profilen mit detaillierten Informationen wie Name, Geburtsdatum, Ort und E-Mail-Adresse reichen. Mit zunehmendem Profil wird es zu einem robusten Archiv mit persönlichen Informationen, Identitäten, Kontaktdaten und Kommunikationsvorlieben für eine Einzelperson. Weitere Informationen zur Verwendung dieser Klasse im Plattform-Ökosystem finden Sie in der [XDM-Übersicht](../home.md#data-behaviors).

Die [!DNL XDM Individual Profile] Klasse selbst stellt mehrere systemgenerierte Werte bereit, die beim Erfassen von Daten automatisch gefüllt werden, während alle anderen Felder mithilfe von [kompatiblen Mixins](#mixins)hinzugefügt werden müssen:

![](../images/classes/individual-profile.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_repo` | Ein Objekt, das die folgenden [!UICONTROL DateTime] -Felder enthält: <ul><li>`createDate`: Datum und Uhrzeit der Erstellung der Ressource im Datenspeicher, z. B. wann die Daten zum ersten Mal erfasst wurden.</li><li>`modifyDate`: Datum und Uhrzeit der letzten Änderung der Ressource.</li></ul> |
| `_id` | Ein eindeutiger, vom System generierter Zeichenfolgenbezeichner für den Datensatz. Dieses Feld dient zur Verfolgung der Einzigartigkeit eines einzelnen Datensatzes, zur Vermeidung von Datenduplizierungen und zur Nachforschung dieses Datensatzes in nachgelagerten Diensten. Da dieses Feld vom System generiert wird, sollte es bei der Datenerfassung nicht als expliziter Wert angegeben werden.<br><br>Es ist wichtig zu unterscheiden, dass dieses Feld **nicht** eine Identität darstellt, die mit einer einzelnen Person in Zusammenhang steht, sondern vielmehr die Aufzeichnung der Daten selbst. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen in [Identitätsfelder](../schema/composition.md#identity) unterteilt werden. |
| `createdByBatchID` | Die ID des erfassten Stapels, die zur Erstellung des Datensatzes geführt hat. |
| `modifiedByBatchID` | Die ID des letzten erfassten Stapels, der zur Aktualisierung des Datensatzes geführt hat. |
| `repositoryCreatedBy` | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. |

## Kompatible Mixins {#mixins}

Adobe bietet verschiedene Standard-Mixins zur Verwendung mit der [!DNL XDM Individual Profile] Klasse. Im Folgenden finden Sie eine Liste der am häufigsten verwendeten Mixins für die Klasse:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Angaben zur Person des Profils]](../mixins/profile/person-details.md)
* [[!UICONTROL Persönliche Angaben zum Profil]](../mixins/profile/personal-details.md)
* [[!UICONTROL Profil-Arbeitsdetails]](../mixins/profile/work-details.md)
* [[!UICONTROL Segmentierung von Profilen]](../mixins/profile/segmentation.md)