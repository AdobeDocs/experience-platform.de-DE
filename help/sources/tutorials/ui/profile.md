---
keywords: Experience Platform;Startseite;beliebte Themen;eingehende Daten aktivieren;Profil ausfüllen;rtcp ausfüllen;Einheitliches Profil ausfüllen
solution: Experience Platform
title: Aktivieren von eingehenden Quelldaten zum Ausfüllen von Kundenprofilen in der Benutzeroberfläche
type: Tutorial
description: Eingehende Daten aus Ihrem Quell-Connector können zur Anreicherung und zum Ausfüllen Ihrer Echtzeit-Kundenprofildaten verwendet werden.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 22%

---

# Aktivieren von eingehenden Quelldaten zum Ausfüllen von Kundenprofilen

Eingehende Daten aus Ihrem Quell-Connector können zur Anreicherung und zum Ausfüllen Ihrer [!DNL Real-Time Customer Profile] Daten.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Außerdem müssen Sie für dieses Tutorial bereits einen Quell-Connector erstellt und konfiguriert haben.  Eine Liste der Tutorials zum Erstellen verschiedener Connectoren in der Benutzeroberfläche finden Sie im [Übersicht über Quell-Connectoren](../../home.md).

## Ihre [!DNL Real-Time Customer Profile] data

Um Kundenprofile anzureichern, muss das Quellschema des Zieldatensatzes für die Verwendung in [!DNL Real-Time Customer Profile]. Ein kompatibles Schema erfüllt folgende Anforderungen:

- Das Schema weist mindestens ein Attribut auf, das als Identitätseigenschaft definiert wurde.
- Das Schema verfügt über eine Identitätseigenschaft, die als primäre Identität definiert wurde.
- Eine Zuordnung innerhalb des Datenflusses ist vorhanden, wobei die primäre Identität ein Zielattribut ist.

Klicken Sie im Arbeitsbereich Quellen auf die **[!UICONTROL Durchsuchen]** -Tab, um Ihre Basisverbindungen aufzulisten. Suchen Sie in der angezeigten Liste die Verbindung, die den Datenfluss enthält, mit dem Profile gefüllt werden sollen. Klicken Sie auf den Namen der Verbindung, um auf deren Details zuzugreifen.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Die Verbindung **[!UICONTROL Quellaktivität]** angezeigt, in dem die Datensätze angezeigt werden, in die die Verbindung Quelldaten aufnimmt. Klicken Sie auf den Namen des Datensatzes, für den Sie die [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Die **[!UICONTROL Datensatzaktivität]** angezeigt. Die **[!UICONTROL Eigenschaften]** -Spalte auf der rechten Seite des Bildschirms zeigt die Details des Datensatzes an und enthält eine **[!UICONTROL Profil]** und einen Link zum Schema, dem der Datensatz entspricht. Klicken Sie auf den Namen des Schemas, um dessen Komposition anzuzeigen.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

Die **[!UICONTROL Schema Editor]** angezeigt, um die Struktur des Schemas in der mittleren Arbeitsfläche anzuzeigen. Wählen Sie auf der Arbeitsfläche das Feld aus, das als primäre Identität festgelegt werden soll. Unter dem **[!UICONTROL Feldeigenschaften]** angezeigt wird, wählen Sie die **[!UICONTROL Identität]** Kontrollkästchen und **[!UICONTROL Primäre Identität]**. Wählen Sie abschließend eine geeignete **[!UICONTROL Identitäts-Namespace]** Klicken Sie auf **[!UICONTROL Anwenden]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Klicken Sie auf das Objekt der obersten Ebene der Schemastruktur und auf die **[!UICONTROL Schemaeigenschaften]** angezeigt. Aktivieren des Schemas für [!DNL Profile] durch Umschalten der **[!UICONTROL Profil]** umschalten. Klicken **[!UICONTROL Speichern]** um Ihre Änderungen abzuschließen.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Jetzt, da das Schema für [!DNL Profile], kehren Sie zu **[!UICONTROL Datensatzaktivität]** Bildschirm anzeigen und Datensatz aktivieren für [!DNL Profile] durch Klicken auf **[!UICONTROL Profil]** innerhalb der **[!UICONTROL Eigenschaften]** Spalte.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Wenn sowohl das Schema als auch der Datensatz für [!DNL Profile], füllen die in diesen Datensatz erfassten Daten jetzt auch Kundenprofile.

>[!NOTE]
>
>Vorhandene Daten in einem kürzlich aktivierten Datensatz werden nicht von [!DNL Profile].

## Nächste Schritte

In diesem Tutorial haben Sie eingehende Daten für [!DNL Profile] Population. Weiterführende Informationen finden Sie in der [[!DNL Real-Time Customer Profile] Übersicht](../../../profile/home.md).
