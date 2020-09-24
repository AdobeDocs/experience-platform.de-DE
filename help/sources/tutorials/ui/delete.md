---
keywords: Experience Platform;home;popular topics; delete dataflows
description: Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Löschen von Datenflüssen aus dem Quellarbeitsbereich.
solution: Experience Platform
title: Datenflüsse löschen
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 10%

---


# Datenflüsse löschen

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Löschen von Datenflüssen aus dem [!UICONTROL Quellarbeitsbereich] .

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model] (XDM) System](../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [[!DNL Echtzeit-Profil]](../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

## Löschen von Datenflüssen mithilfe der Benutzeroberfläche

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den **[!UICONTROL Quellarbeitsbereich]** zuzugreifen. Im Anzeigebereich &quot; **[!UICONTROL Katalog]** &quot;werden verschiedene Quellen angezeigt, für die Sie Konten und Datenflüsse erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse, die ihnen zugeordnet sind.

Wählen Sie &quot; **[!UICONTROL Datenflüsse]** &quot;, um auf die Seite &quot; **[!UICONTROL Datenflüsse]** &quot;zuzugreifen.

![dataset-flow-Aktivität](../../images/tutorials/delete/dataflows.png)

Eine Liste der vorhandenen Datenflüsse wird angezeigt. Auf dieser Seite finden Sie eine Liste sortierbarer Informationen zu vorhandenen Datenflüssen wie Quelle, Benutzername, Ausführungsstatus und Datum der letzten Ausführung. Wählen Sie das **Trichtersymbol** oben links, das sortiert werden soll.

![dataflows-Liste](../../images/tutorials/delete/dataflows-list.png)

Das Sortierungsbedienfeld wird auf der linken Seite des Bildschirms mit einer Liste der verfügbaren Quellen angezeigt.
Mit der Sortierfunktion können Sie mehrere Quellen auswählen.

Wählen Sie die Quelle aus, auf die Sie zugreifen möchten, und suchen Sie den Datenfluss, den Sie löschen möchten, aus der Liste der Datenflüsse in der Hauptschnittstelle. In diesem Beispiel ist die ausgewählte Quelle **[!DNL Azure Blob Storage]** und der Dataflow-Name der Datenfluss für **[!UICONTROL Kundendaten]**. Wenn Sie mehrere Quellen aus dem Sortierfeld auswählen, werden die zuletzt erstellten Datenflüsse zuerst angezeigt, da die Liste nach dem erstellten Datum sortiert wird.

Wählen Sie den zu löschenden Datenfluss aus.

![dataflows-sort](../../images/tutorials/delete/dataflows-sort.png)

Das Bedienfeld &quot; **[!UICONTROL Eigenschaften]** &quot;wird auf der rechten Seite des Bildschirms angezeigt und enthält Informationen zum ausgewählten Datenpfad sowie eine Option zum **[!UICONTROL Bearbeiten des Zeitplans]**.

Zum Löschen des Datenflusses wählen Sie &quot; **[!UICONTROL Löschen&quot;]**.

![dataflows-sort](../../images/tutorials/delete/dataflows-properties.png)

Ein abschließendes Bestätigungsdialogfeld wird angezeigt. Wählen Sie **[!UICONTROL Löschen]** , um den Vorgang abzuschließen.

![Löschen Sie](../../images/tutorials/delete/delete.png)

Nach einigen Augenblicken wird am unteren Bildschirmrand ein grünes Bestätigungsfeld angezeigt, um eine erfolgreiche Löschung zu bestätigen.

![bestätigt](../../images/tutorials/delete/confirmed.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich auf vorhandene Konten und Datenflüsse im **[!UICONTROL Sources]** -Arbeitsbereich zugegriffen. Eingehende Daten können nun von nachgelagerten [!DNL Platform] Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace]genutzt werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [[!DNL Real-time Customer Profile] Übersicht](../../../profile/home.md)
- [[!DNL Data Science Workspace] Übersicht](../../../data-science-workspace/home.md)