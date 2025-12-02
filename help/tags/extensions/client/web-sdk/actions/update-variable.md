---
title: Variable aktualisieren
description: Ändert den Inhalt eines variablen Datenelements.
source-git-commit: f87e6a0e969aa0924656cdb2ea56aa79d2d7c841
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Variable aktualisieren

Mit der **[!UICONTROL Update variable]** Aktion können Sie partielle oder inkrementelle Änderungen an einem [variablen Datenelement“ &#x200B;](../data-element-types.md#variable). Mit dieser Aktion können Sie ein Objekt erstellen, auf das später in einer [[!UICONTROL Send event]](send-event.md)-Aktion verwiesen werden kann. Das Füllen von Datenelementen und das Zuweisen zu Eigenschaften in einem XDM-Objekt ist für die meisten Anwendungsfälle geeignet. Diese Aktion bietet mehr Flexibilität, damit Sie auf der Grundlage von Regelbedingungen Eigenschaften bedingt auf verschiedene Datenelemente festlegen können.

Bevor Sie diese Aktion verwenden, muss bereits ein variables Datenelement erstellt worden sein. Nachdem Sie ein variables Datenelement zum Ändern ausgewählt haben, wird ein Editor angezeigt, in dem Sie alle gewünschten Felder für diese Aktion festlegen können.

![Screenshot der Aktion „Variable aktualisieren“ in der Aktionskonfigurations-Benutzeroberfläche](../assets/update-variable.png)

Das im Editor verwendete XDM-Schema entspricht dem Schema, das im Datenelement „Variable“ ausgewählt wurde. Sie können eine oder mehrere Eigenschaften des Objekts festlegen, indem Sie Objekte erweitern und gewünschte Eigenschaften auswählen. Im folgenden Screenshot ist beispielsweise die Eigenschaft `producedBy` auf das Datenelement `%Produced by data element%` festgelegt.

![Screenshot der Aktionskonfigurations-Benutzeroberfläche mit einer aktualisierten Eigenschaft](../assets/update-variable-set-property.png)

Wenn Sie ein variables Datenelement auswählen, das ein Datenobjekt anstelle eines XDM-Objekts verwendet, hängen die verfügbaren Felder von den Produkten ab, die beim Konfigurieren des Datenelements ausgewählt wurden. Wenn Sie beispielsweise ein Datenobjekt erstellen, das Adobe Analytics-Felder enthält, stellt die Auswahl des Datenelements „Variable“ in dieser Benutzeroberfläche Felder bereit, die Sie für Adobe Analytics spezifisch ausfüllen können.

![Screenshot der Aktionskonfigurations-Benutzeroberfläche mit einem auf einem Datenobjekt basierenden variablen Datenelement](../assets/variable-data-element-data.png)
