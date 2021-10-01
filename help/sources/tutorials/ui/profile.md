---
keywords: Experience Platform;Startseite;beliebte Themen;eingehende Daten aktivieren;Profil ausfüllen;rtcp ausfüllen;Einheitliches Profil ausfüllen
solution: Experience Platform
title: Aktivieren von eingehenden Quelldaten zum Ausfüllen von Kundenprofilen in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Eingehende Daten aus Ihrem Quell-Connector können zur Anreicherung und zum Ausfüllen Ihrer Echtzeit-Kundenprofildaten verwendet werden.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 16%

---

# Aktivieren von eingehenden Quelldaten zum Ausfüllen von Kundenprofilen

Eingehende Daten aus Ihrem Quell-Connector können zur Anreicherung und zum Ausfüllen Ihrer [!DNL Real-time Customer Profile] -Daten verwendet werden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md) zum Schema Editor: Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Außerdem müssen Sie für dieses Tutorial bereits einen Quell-Connector erstellt und konfiguriert haben.  Eine Liste der Tutorials zum Erstellen verschiedener Connectoren in der Benutzeroberfläche finden Sie in der [Übersicht über Quell-Connectoren](../../home.md).

## Füllen Sie Ihre [!DNL Real-time Customer Profile]-Daten

Um Kundenprofile anzureichern, muss das Quellschema des Zieldatensatzes für die Verwendung in [!DNL Real-time Customer Profile] kompatibel sein. Ein kompatibles Schema erfüllt folgende Anforderungen:

- Das Schema weist mindestens ein Attribut auf, das als Identitätseigenschaft definiert wurde.
- Das Schema verfügt über eine Identitätseigenschaft, die als primäre Identität definiert wurde.
- Eine Zuordnung innerhalb des Datenflusses ist vorhanden, wobei die primäre Identität ein Zielattribut ist.

Klicken Sie im Arbeitsbereich &quot;Quellen&quot;auf die Registerkarte **[!UICONTROL Durchsuchen]** , um Ihre Basisverbindungen aufzulisten. Suchen Sie in der angezeigten Liste die Verbindung, die den Datenfluss enthält, mit dem Profile gefüllt werden sollen. Klicken Sie auf den Namen der Verbindung, um auf deren Details zuzugreifen.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Der Bildschirm **[!UICONTROL Quellaktivität]** der Verbindung wird mit den Datensätzen angezeigt, in die die Verbindung Quelldaten aufnimmt. Klicken Sie auf den Namen des Datensatzes, den Sie für [!DNL Profile] aktivieren möchten.

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Der Bildschirm **[!UICONTROL Datensatzaktivität]** wird angezeigt. Die Spalte **[!UICONTROL Eigenschaften]** auf der rechten Seite des Bildschirms zeigt die Details des Datensatzes an. Sie enthält einen **[!UICONTROL Profil]**-Switch und einen Link zum Schema, dem der Datensatz entspricht. Klicken Sie auf den Namen des Schemas, um dessen Komposition anzuzeigen.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

Der **[!UICONTROL Schema-Editor]** wird angezeigt und zeigt die Struktur des Schemas in der mittleren Arbeitsfläche an. Wählen Sie auf der Arbeitsfläche das Feld aus, das als primäre Identität festgelegt werden soll. Wählen Sie unter der angezeigten Registerkarte **[!UICONTROL Feldeigenschaften]** das Kontrollkästchen **[!UICONTROL Identität]** und dann **[!UICONTROL Primäre Identität]**. Wählen Sie abschließend einen geeigneten **[!UICONTROL Identitäts-Namespace]** und klicken Sie dann auf **[!UICONTROL Anwenden]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Klicken Sie auf das Objekt der obersten Ebene der Schemastruktur und die Spalte **[!UICONTROL Schemaeigenschaften]** wird angezeigt. Aktivieren Sie das Schema für [!DNL Profile], indem Sie den Umschalter **[!UICONTROL Profil]** aktivieren. Klicken Sie auf **[!UICONTROL Speichern]** , um die Änderungen abzuschließen.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Nachdem das Schema für [!DNL Profile] aktiviert wurde, kehren Sie zum Bildschirm **[!UICONTROL Datensatzaktivität]** zurück und aktivieren Sie den Datensatz für [!DNL Profile], indem Sie auf den Umschalter **[!UICONTROL Profil]** in der Spalte **[!UICONTROL Eigenschaften]** klicken.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Wenn sowohl das Schema als auch der Datensatz für [!DNL Profile] aktiviert sind, füllen die in diesen Datensatz erfassten Daten jetzt auch Kundenprofile aus.

>[!NOTE]
>
>Vorhandene Daten in einem kürzlich aktivierten Datensatz werden von [!DNL Profile] nicht verwendet.

## Nächste Schritte

In diesem Tutorial haben Sie eingehende Daten für [!DNL Profile] Population erfolgreich aktiviert. Weitere Informationen finden Sie unter [[!DNL Real-time Customer Profile] overview](../../../profile/home.md).
