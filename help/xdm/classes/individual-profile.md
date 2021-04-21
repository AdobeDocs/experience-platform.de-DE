---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemas;Identitätskarte;Identitätskarte;Schema-Design;Map;Vereinigung Schema;Vereinigung
solution: Experience Platform
title: XDM Individuelle Profil-Klasse
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die XDM Individual Profil-Klasse.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] ist eine Standard-XDM-Klasse, die eine Singular-Darstellung (oder &quot;Profil&quot;) der Attribute und Interessen von identifizierten und teilweise identifizierten Personen bildet.

Profil können von anonymen Verhaltenssignalen (z. B. Browser-Cookies) bis hin zu eindeutig identifizierten Profilen mit detaillierten Informationen wie Name, Geburtsdatum, Ort und E-Mail-Adresse reichen. Mit zunehmendem Profil wird es zu einem robusten Archiv mit persönlichen Informationen, Identitäten, Kontaktdaten und Kommunikationsvorlieben für eine Einzelperson. Weitere Informationen zur Verwendung dieser Klasse im Plattform-Ökosystem finden Sie in der [XDM-Übersicht](../home.md#data-behaviors).

Die [!DNL XDM Individual Profile]-Klasse selbst stellt mehrere systemgenerierte Werte bereit, die beim Erfassen von Daten automatisch gefüllt werden, während alle anderen Felder durch die Verwendung von [kompatiblen Mixins](#mixins) hinzugefügt werden müssen:

![](../images/classes/individual-profile.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_repo` | Ein Objekt, das die folgenden [!UICONTROL DateTime]-Felder enthält: <ul><li>`createDate`: Datum und Uhrzeit der Erstellung der Ressource im Datenspeicher, z. B. wann die Daten zum ersten Mal erfasst wurden.</li><li>`modifyDate`: Datum und Uhrzeit der letzten Änderung der Ressource.</li></ul> |
| `_id` | Ein eindeutiger, vom System generierter Zeichenfolgenbezeichner für den Datensatz. Dieses Feld dient zur Verfolgung der Einzigartigkeit eines einzelnen Datensatzes, zur Vermeidung von Datenduplizierungen und zur Nachforschung dieses Datensatzes in nachgelagerten Diensten. Da dieses Feld vom System generiert wird, sollte es bei der Datenerfassung nicht als expliziter Wert angegeben werden.<br><br>Es ist wichtig zu unterscheiden, dass dieses Feld  **keine Identität** darstellt, die sich auf eine Person bezieht, sondern vielmehr die Aufzeichnung der Daten selbst. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen in [Identitätsfelder](../schema/composition.md#identity) umbenannt werden. |
| `createdByBatchID` | Die ID des erfassten Stapels, die zur Erstellung des Datensatzes geführt hat. |
| `modifiedByBatchID` | Die ID des letzten erfassten Stapels, der zur Aktualisierung des Datensatzes geführt hat. |
| `repositoryCreatedBy` | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. |

## Kompatible Mixins {#mixins}

>[!NOTE]
>
>Die Namen mehrerer Mixins haben sich geändert. Weitere Informationen finden Sie im Dokument [mixin name updates](../mixins/name-updates.md).

Adobe bietet mehrere Standardmixins zur Verwendung mit der [!DNL XDM Individual Profile]-Klasse. Im Folgenden finden Sie eine Liste der am häufigsten verwendeten Mixins für die Klasse:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Demografische Details]](../mixins/profile/person-details.md)
* [[!UICONTROL Persönliche Kontaktangaben]](../mixins/profile/personal-details.md)
* [[!UICONTROL Kontaktangaben bearbeiten]](../mixins/profile/work-details.md)
* [[!UICONTROL Details zur Segmentmitgliedschaft]](../mixins/profile/segmentation.md)
