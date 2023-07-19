---
keywords: Experience Platform, Profil, Kundenprofil in Echtzeit, Zusammenführungsrichtlinien, Benutzeroberfläche, Benutzeroberfläche, Zeitstempel geordnet, Datensatzpriorität
title: Zusammenführungsrichtlinien – Übersicht
type: Documentation
description: Mit Adobe Experience Platform können Sie Datenfragmente aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich eine vollständige Ansicht über Ihre einzelnen Kunden verschaffen können. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen Platform bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um eine einheitliche Ansicht zu schaffen.
exl-id: a8ef527a-cfee-4129-9973-e8a212a3ad1e
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 81%

---

# Zusammenführungsrichtlinien – Übersicht

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich eine vollständige Ansicht über jeden einzelnen Ihrer Kunden verschaffen können. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen [!DNL Platform] bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um eine einheitliche Ansicht zu schaffen.

Über die RESTful APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen einrichten. Dieses Dokument bietet einen Überblick über Zusammenführungsrichtlinien und deren Rolle in Experience Platform.

## Erste Schritte

Dieses Handbuch setzt ein Grundverständnis für mehrere wichtige [!DNL Experience Platform]-Funktionen voraus. Bevor Sie dieses Handbuch befolgen und mit Zusammenführungsrichtlinien arbeiten, überprüfen Sie bitte die Dokumentation für die folgendenen Services:

* [Echtzeit-Kundenprofil](../home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Ermöglicht das Echtzeit-Kundenprofil durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, in die erfasst wird [!DNL Platform].
* [Experience-Datenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

## Zusammenführungsrichtlinien verstehen

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich eine einheitlich Ansicht über Ihre einzelnen Kunden verschaffen können. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen Platform bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um eine Übersicht zu schaffen.

Wenn ein Kunde beispielsweise über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihr Unternehmen über mehrere Profilfragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen enthalten sind. Wenn diese Fragmente in Platform aufgenommen werden, werden sie zusammengeführt, sodass ein zentrales Profil für diesen Kunden entsteht.

Wenn die Daten aus mehreren Quellen in Konflikt stehen (z. B. listet ein Fragment den Kunden als „ledig“ auf, während ein anderes den Kunden als „verheiratet“ auflistet), bestimmt die Zusammenführungsrichtlinie, welche Informationen priorisiert und in das Profil für die Einzelperson aufgenommen werden sollen.

Zusammenführungsrichtlinien sind für Ihre Organisation privat, sodass Sie verschiedene Richtlinien erstellen können, um Schemas auf die gewünschte Weise zusammenzuführen. Sie können auch eine standardmäßige Zusammenführungsrichtlinie angeben, die verwendet wird, wenn keine explizite Angabe erfolgt. Weitere Informationen finden Sie im Abschnitt [Standardmäßige Zusammenführungsrichtlinien](#default-merge-policy) weiter unten in diesem Dokument. Bitte beachten Sie, dass pro Organisation maximal fünf Zusammenführungsrichtlinien zulässig sind.

## Zusammenführungsmethoden {#merge-methods}

Jedes Profilfragment enthält Informationen für nur eine Identität aus der Gesamtzahl der Identitäten, die für eine Einzelperson vorhanden sein könnten. Beim Zusammenführen dieser Daten zu einem Kundenprofil kann es zu Konflikten zwischen diesen Informationen kommen und es muss eine Priorität festgelegt werden.

Wenn Sie eine Zusammenführungsmethode auswählen, können Sie angeben, welche Datensatzattribute priorisiert werden sollen, wenn ein Zusammenführungskonflikt zwischen Datensätzen auftritt.

Für Zusammenführungsrichtlinien stehen zwei mögliche Zusammenführungsmethoden zur Verfügung. Jede dieser Methoden wird im Folgenden mit zusätzlichen Details in den folgenden Abschnitten zusammengefasst:

* **[!UICONTROL Datensatzpriorität]:** Geben Sie im Falle eines Konflikts den Profilfragmenten Priorität, basierend auf dem Datensatz, aus dem sie stammen. Wenn Sie diese Option wählen, müssen Sie die zugehörigen Datensätze und deren Prioritätsreihenfolge auswählen. Weitere Informationen über die Zusammenführungsmethode [Datensatzpriorität](#dataset-precedence).
* **[!UICONTROL Zeitstempel geordnet]:** Im Fall eines Konflikts wird dem zuletzt aktualisierten Profilfragment Priorität eingeräumt. Hier erfahren Sie mehr über die [nach Zeitstempel geordnete](#timestamp-ordered) Zusammenführungsmethode.

### Datensatzpriorität {#dataset-precedence}

Wenn **[!UICONTROL Datensatzpriorität]** als Zusammenführungsmethode für eine Zusammenführungsrichtlinie ausgewählt ist, können Sie Profilfragmenten, basierend auf dem Datensatz, aus dem sie stammen, Priorität einräumen. Ein Beispiel bestünde darin, wenn es in Ihrer Organisation Daten in einem Datensatz gibt, die bevorzugt werden oder vertrauenswürdiger sind als Daten in einem anderen Datensatz.

Um eine Zusammenführungsrichtlinie mit **[!UICONTROL Datensatzpriorität]** zu erstellen, müssen Sie die eingeschlossenen Profil- und ExperienceEvent-Datensätze auswählen und dann die Profildatensätze manuell für die Rangfolge sortieren. Nachdem die Datensätze ausgewählt und geordnet wurden, erhält der oberste Datensatz die höchste Priorität, der zweite Datensatz die zweithöchste u.s.w.

### Zeitstempel geordnet {#timestamp-ordered}

Bei der Aufnahme von Profildatensätzen in Experience Platform wird ein Systemzeitstempel zum Zeitpunkt der Aufnahme ermittelt und dem Datensatz hinzugefügt. Wenn **[!UICONTROL Zeitstempel ordered]** als Zusammenführungsmethode für eine Zusammenführungsrichtlinie ausgewählt ist, werden Profile basierend auf dem Systemzeitstempel zusammengeführt. Das heißt, das Zusammenführen erfolgt auf Basis des Zeitstempels, an dem der Datensatz in Platform aufgenommen wurde.

## Identitätszuordnung {#id-stitching}

Identitätszuordnung ([!UICONTROL ID-Zuordnung]) ist der Prozess der Identifikation von Datenfragmenten und ihrer Kombination zu einem vollständigen Profildatensatz. Zur Veranschaulichung der unterschiedlichen Zuordnungsverhaltensweisen sollten Sie einen einzelnen Kunden berücksichtigen, der mit einer Marke über zwei verschiedene E-Mail-Adressen interagiert.

* **[!UICONTROL Keine]:** Wenn diese Option ausgewählt ist, werden IDs nicht zugeordnet. Wenn die Segmentierung erfolgt, werden Identitäten, die zu derselben Person gehören können, nicht zugeordnet. Bei der Segmentierung werden nur die mit jeder einzelnen ID verknüpften Attribute berücksichtigt, wenn festgestellt wird, ob ein Kunde für die Zielgruppenzugehörigkeit qualifiziert ist. Dies könnte dazu führen, dass ein einzelner Kunde über mehrere Profile verfügt und jedes Profil für verschiedene Zielgruppen qualifiziert ist, sodass mehrere Marketing-Nachrichten an denselben Kunden gesendet werden.
* **[!UICONTROL Privates Diagramm]:** Wenn das private Diagramm ausgewählt ist, werden mehrere Identitäten, die sich auf dieselbe Person beziehen, zugeordnet. Dies führt dazu, dass der Kunde über ein einzelnes Profil verfügt, und ermöglicht der Segmentierung, bei der Bestimmung der Segmentqualifizierung mehrere Attribute aus mehreren verwandten Identitäten zu berücksichtigen. In diesem Szenario weist der Kunde wahrscheinlich ein einzelnes Profil auf, qualifiziert sich für eine Zielgruppe, basierend auf der Kombination von Attributen über Identitäten hinweg, und erhält nur eine Marketing-Nachricht.

Um mehr über Identitäten und ihre Rolle beim Generieren von Profilen und Zielgruppen zu erfahren, lesen Sie zunächst das [Identity Service - Übersicht](../../identity-service/home.md).

## Standardmäßige Zusammenführungsrichtlinie {#default-merge-policy}

Eine Organisation kann eine standardmäßige Zusammenführungsrichtlinie für ihre Organisation erstellen, die beim Zusammenführen von Profilfragmenten verwendet wird. Auf diese Weise können Benutzer bei Aktionen in der Experience Platform einfach die Standardrichtlinie auswählen, z. B. beim Anzeigen von Kundenprofilen oder Erstellen von Zielgruppen. In den meisten Fällen wird die standardmäßige Zusammenführungsrichtlinie verwendet, sofern keine andere Zusammenführungsrichtlinie angegeben ist.

Jede Organisation kann mehrere Zusammenführungsrichtlinien erstellen, die sich auf eine einzelne XDM-Schemaklasse beziehen, jedoch kann für jede Klasse nur eine standardmäßige Zusammenführungsrichtlinie deklariert werden. Ihre Organisation könnte beispielsweise über eine standardmäßige Zusammenführungsrichtlinie für die [!DNL XDM Individual Profile]-Klasse und eine andere standardmäßige Zusammenführungsrichtlinie für eine benutzerdefinierte Produktinventarklasse verfügen.

Wenn Sie eine neue Zusammenführungsrichtlinie erstellen und sie als Standard festlegen, wird die vorherige standardmäßige Zusammenführungsrichtlinie automatisch vom System aktualisiert, sodass sie nicht mehr der Standard ist.

>[!WARNING]
>
>Profilzählungen und Zielgruppen mit einer vorhandenen, zugehörigen standardmäßigen Zusammenführungsrichtlinie können betroffen sein. Alle Zielgruppen, für die eine standardmäßige Zusammenführungsrichtlinie angewendet wurde, werden auf die neue standardmäßige Zusammenführungsrichtlinie aktualisiert.

## Nächste Schritte

Nach dem Lesen dieses Handbuchs wissen Sie jetzt, welche Zusammenführungsrichtlinien gelten und welche Rolle sie in der Experience Platform spielen. Informationen zum Einstieg in die Arbeit mit Zusammenführungsrichtlinien in der Experience Platform-Benutzeroberfläche finden Sie im [UI-Handbuch für Zusammenführungsrichtlinien](ui-guide.md). Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der API finden Sie im [API-Endpunkthandbuch für Zusammenführungsrichtlinien](../api/merge-policies.md).
