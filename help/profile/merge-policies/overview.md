---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Zusammenführungsrichtlinien; Benutzeroberfläche; Benutzeroberfläche; Zeitstempel geordnet; Datensatzpriorität
title: Zusammenführungsrichtlinien - Überblick
type: Documentation
description: Mit Adobe Experience Platform können Sie Datenfragmente aus mehreren Quellen zusammenführen und kombinieren, um eine vollständige Ansicht Ihrer Kunden zu erhalten. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen Platform bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden, um eine einheitliche Ansicht zu schaffen.
source-git-commit: c2cc1428e3a70cf987adab583e9f9fb5d5140c74
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 11%

---


# Zusammenführungsrichtlinien - Übersicht

Mit Adobe Experience Platform können Sie Datenfragmente aus mehreren Quellen zusammenführen und kombinieren, um eine vollständige Ansicht Ihrer einzelnen Kunden zu erhalten. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen [!DNL Platform] bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden, um eine einheitliche Ansicht zu schaffen.

Über die RESTful APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen einrichten. Dieses Dokument bietet einen Überblick über Zusammenführungsrichtlinien und deren Rolle in der Experience Platform.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis mehrerer wichtiger [!DNL Experience Platform] Funktionen voraus. Bevor Sie dieses Handbuch befolgen und mit Zusammenführungsrichtlinien arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [Echtzeit-Kundenprofil](../home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Adobe Experience Platform Identity-Dienst](../../identity-service/home.md): Ermöglicht das Echtzeit-Kundenprofil durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, die in erfasst werden  [!DNL Platform].
* [Experience-Datenmodell (XDM)](../../xdm/home.md)[!DNL Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.

## Zusammenführungsrichtlinien verstehen

Mit Adobe Experience Platform können Sie Datenfragmente aus mehreren Quellen zusammenführen und kombinieren, um eine vollständige, einheitliche Ansicht Ihrer einzelnen Kunden zu erhalten. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen Platform bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um eine Übersicht zu schaffen.

Wenn ein Kunde beispielsweise über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihr Unternehmen über mehrere Profilfragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen enthalten sind. Wenn diese Fragmente in Platform aufgenommen werden, werden sie zusammengeführt, sodass ein zentrales Profil für diesen Kunden entsteht.

Wenn es zu Konflikten zwischen Daten aus verschiedenen Quellen kommt (z. B. listet ein Fragment den Kunden als &quot;einzeln&quot;auf, während das andere den Kunden als &quot;verheiratet&quot;auflistet), bestimmt die Zusammenführungsrichtlinie, welche Informationen in das Profil für den Kontakt aufgenommen werden sollen.

Zusammenführungsrichtlinien sind privat für Ihre IMS-Organisation, sodass Sie verschiedene Richtlinien erstellen können, um Schemas auf die gewünschte Weise zusammenzuführen. Sie können auch eine standardmäßige Zusammenführungsrichtlinie angeben, die verwendet wird, wenn keine explizite Angabe erfolgt. Weitere Informationen finden Sie im Abschnitt [Standardmäßige Zusammenführungsrichtlinien](#default-merge-policy) weiter unten in diesem Dokument.

## Zusammenführungsmethoden {#merge-methods}

Jedes Profilfragment enthält Informationen für nur eine Identität aus der Gesamtzahl der Identitäten, die für eine Person vorhanden sein könnten. Beim Zusammenführen dieser Daten zu einem Kundenprofil besteht die Möglichkeit, dass diese Informationen miteinander in Konflikt geraten und eine Priorität angegeben werden muss.

Wenn Sie eine Zusammenführungsmethode auswählen, können Sie angeben, welche Datensatzattribute priorisiert werden sollen, wenn ein Zusammenführungskonflikt zwischen Datensätzen auftritt.

Für Zusammenführungsrichtlinien stehen zwei mögliche Zusammenführungsmethoden zur Verfügung. Jede dieser Methoden wird im Folgenden mit zusätzlichen Details in den folgenden Abschnitten zusammengefasst:

* **[!UICONTROL Datensatzpriorität]:** Geben Sie im Fall eines Konflikts Profilfragmenten je nach dem Datensatz, aus dem sie stammen, Priorität. Bei Auswahl dieser Option müssen Sie die zugehörigen Datensätze und deren Prioritätsreihenfolge auswählen. Erfahren Sie mehr über die Zusammenführungsmethode [Datensatzpriorität](#dataset-precedence).
* **[!UICONTROL Zeitstempel geordnet]:** Im Fall eines Konflikts wird dem zuletzt aktualisierten Profilfragment Priorität eingeräumt. Erfahren Sie mehr über die Zusammenführungsmethode [Zeitstempel ordered](#timestamp-ordered) .
   * **Benutzerdefinierte Zeitstempel:**  Die Methode zur sortierten Zeitstempelzusammenführung unterstützt auch benutzerdefinierte Zeitstempel, die beim Zusammenführen von Daten innerhalb desselben Datensatzes (mehrere Identitäten) oder über Datensätze hinweg Vorrang vor Systemzeitstempeln haben. Weitere Informationen finden Sie im Abschnitt [Verwenden benutzerdefinierter Zeitstempel](#custom-timestamps).

### Datensatzpriorität {#dataset-precedence}

Wenn **[!UICONTROL Datensatzpriorität]** als Zusammenführungsmethode für eine Zusammenführungsrichtlinie ausgewählt ist, können Sie Profilfragmenten je nach dem Datensatz, aus dem sie stammen, Priorität einräumen. Ein Beispiel bestünde darin, wenn es in Ihrer Organisation Daten in einem Datensatz gibt, die bevorzugt werden oder vertrauenswürdiger sind als Daten in einem anderen Datensatz.

Um eine Zusammenführungsrichtlinie mit **[!UICONTROL Datensatzpriorität]** zu erstellen, müssen Sie die eingeschlossenen Profil- und ExperienceEvent-Datensätze auswählen und dann die Profildatensätze manuell für die Rangfolge sortieren. Sobald die Datensätze ausgewählt und sortiert wurden, erhält der oberste Datensatz die höchste Priorität, der zweite Datensatz wird an zweiter Stelle stehen usw.

### Zeitstempel geordnet {#timestamp-ordered}

Da Profildatensätze in Experience Platform erfasst werden, wird zum Zeitpunkt der Erfassung ein Systemzeitstempel abgerufen und zum Datensatz hinzugefügt. Wenn **[!UICONTROL Zeitstempel ordered]** als Zusammenführungsmethode für eine Zusammenführungsrichtlinie ausgewählt ist, werden Profile basierend auf dem Systemzeitstempel zusammengeführt. Das heißt, das Zusammenführen erfolgt auf der Grundlage des Zeitstempels für den Zeitpunkt, zu dem der Datensatz in Platform aufgenommen wurde.

#### Verwenden benutzerdefinierter Zeitstempel {#custom-timestamps}

Gelegentlich kann es zu Anwendungsfällen kommen, in denen es erforderlich ist, einen benutzerdefinierten Zeitstempel anzugeben und die Zusammenführungsrichtlinie den benutzerdefinierten Zeitstempel und nicht den Systemzeitstempel berücksichtigen zu lassen. Beispiele dafür sind das Aufstocken von Daten oder die Sicherstellung der richtigen Reihenfolge von Ereignissen, wenn Datensätze nicht in der richtigen Reihenfolge erfasst werden.

Um einen benutzerdefinierten Zeitstempel zu verwenden, muss die Schemafeldgruppe **[!UICONTROL Externe Quellsystem-Prüfungsdetails]** zum Profilschema hinzugefügt werden. Nach dem Hinzufügen kann der benutzerdefinierte Zeitstempel mithilfe des Felds `lastUpdatedDate` aufgefüllt werden. Wenn ein Datensatz erfasst wird und das Feld `lastUpdatedDate` ausgefüllt ist, verwendet Experience Platform dieses Feld, um Datensätze über Datensätze hinweg zusammenzuführen. Wenn `lastUpdatedDate` nicht vorhanden oder nicht ausgefüllt ist, verwendet Platform weiterhin den Systemzeitstempel.

>[!NOTE]
>
>Sie müssen sicherstellen, dass der Zeitstempel `lastUpdatedDate` beim Erfassen einer Aktualisierung für denselben Datensatz gefüllt wird.

Im folgenden Screenshot werden die Felder in der Feldergruppe [!UICONTROL Audit-Details des externen Quellsystems] angezeigt. Eine schrittweise Anleitung zum Arbeiten mit Schemas unter Verwendung der Platform-Benutzeroberfläche, einschließlich des Hinzufügens von Feldergruppen zu Schemas, finden Sie im [Tutorial zum Erstellen eines Schemas mithilfe der Benutzeroberfläche](../../xdm/tutorials/create-schema-ui.md).

![](../images/merge-policies/custom-timestamp-field-group.png)

Informationen zum Arbeiten mit benutzerdefinierten Zeitstempeln mithilfe der API finden Sie im Abschnitt [Endpunkt-Handbuch zu Zusammenführungsrichtlinien zur Verwendung benutzerdefinierter Zeitstempel](../api/merge-policies.md#custom-timestamps).

## Identitätszusammenfügung {#id-stitching}

Identitätszusammenfügung ([!UICONTROL ID-Zuordnung]) ist der Prozess der Identifikation von Datenfragmenten und ihrer Kombination zu einem vollständigen Profildatensatz. Zur Veranschaulichung der unterschiedlichen Stitching-Verhaltensweisen sollten Sie einen einzelnen Kunden berücksichtigen, der mit einer Marke über zwei verschiedene E-Mail-Adressen interagiert.

* **[!UICONTROL Keine]:** Wenn diese Option ausgewählt ist, werden IDs nicht zugeordnet. Wenn die Segmentierung erfolgt, werden Identitäten, die zu derselben Person gehören können, nicht zugeordnet. Bei der Segmentierung werden nur die mit jeder einzelnen ID verknüpften Attribute berücksichtigt, wenn festgestellt wird, ob ein Kunde für die Segmentzugehörigkeit qualifiziert ist. Dies könnte dazu führen, dass ein einzelner Kunde über mehrere Profile verfügt und jedes Profil für verschiedene Segmente qualifiziert ist, sodass mehrere Marketing-Nachrichten an denselben Kunden gesendet werden.
* **[!UICONTROL Privates Diagramm]:** Wenn das private Diagramm ausgewählt ist, werden mehrere Identitäten, die sich auf dieselbe Person beziehen, zugeordnet. Dies führt dazu, dass der Kunde über ein einzelnes Profil verfügt, und ermöglicht die Segmentierung, bei der Bestimmung der Segmentqualifizierung mehrere Attribute aus mehreren verwandten Identitäten zu berücksichtigen. In diesem Szenario weist der Kunde wahrscheinlich ein einzelnes Profil auf, qualifiziert sich für ein Segment basierend auf der Kombination von Attributen über Identitäten hinweg und erhält nur eine Marketing-Nachricht.

Um mehr über Identitäten und ihre Rolle beim Generieren von Profilen und Segmenten zu erfahren, lesen Sie zunächst die [Übersicht über den Identity Service](../../identity-service/home.md).

## Standardmäßige Zusammenführungsrichtlinie {#default-merge-policy}

Eine Organisation kann eine standardmäßige Zusammenführungsrichtlinie für ihre Organisation erstellen, die beim Zusammenführen von Profilfragmenten verwendet wird. Auf diese Weise können Benutzer bei Aktionen in Experience Platformen wie der Anzeige von Kundenprofilen oder der Erstellung von Segmenten einfach die Standardrichtlinie auswählen. In den meisten Fällen wird die standardmäßige Zusammenführungsrichtlinie verwendet, sofern keine andere Zusammenführungsrichtlinie angegeben ist.

Jede Organisation kann mehrere Zusammenführungsrichtlinien erstellen, die sich auf eine einzelne XDM-Schemaklasse beziehen, jedoch kann für jede Klasse nur eine standardmäßige Zusammenführungsrichtlinie deklariert werden. Ihre Organisation könnte beispielsweise über eine standardmäßige Zusammenführungsrichtlinie für die [!DNL XDM Individual Profile]-Klasse und eine andere standardmäßige Zusammenführungsrichtlinie für eine benutzerdefinierte Produktinventarklasse verfügen.

Wenn Sie eine neue Zusammenführungsrichtlinie erstellen und sie als Standard festlegen, wird die vorherige standardmäßige Zusammenführungsrichtlinie automatisch vom System aktualisiert, sodass sie nicht mehr der Standard ist.

>[!WARNING]
>
>Profilzählungen und Segmente mit einer vorhandenen standardmäßigen Zusammenführungsrichtlinie können betroffen sein. Jedes Segment, für das eine standardmäßige Zusammenführungsrichtlinie angewendet wurde, wird auf die neue standardmäßige Zusammenführungsrichtlinie aktualisiert.

## Nächste Schritte

Nach dem Lesen dieses Handbuchs wissen Sie jetzt, welche Zusammenführungsrichtlinien gelten und welche Rolle sie in der Experience Platform spielen. Informationen zum Einstieg in die Arbeit mit Zusammenführungsrichtlinien in der Experience Platform-Benutzeroberfläche finden Sie im [UI-Handbuch für Zusammenführungsrichtlinien](ui-guide.md). Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der API finden Sie im [API-Endpunkthandbuch für Zusammenführungsrichtlinien](../api/merge-policies.md).