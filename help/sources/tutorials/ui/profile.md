---
keywords: Experience Platform; home; beliebte Themen; eingehende Daten aktivieren; Profil ausfüllen; rtcp ausfüllen; einheitliches Profil ausfüllen
solution: Experience Platform
title: Aktivieren von eingehenden Source-Daten zum Ausfüllen von Kundenprofilen in der Benutzeroberfläche
type: Tutorial
description: Eingehende Daten aus Ihrem Quell-Connector können zur Anreicherung und zum Ausfüllen Ihrer Echtzeit-Kundenprofildaten verwendet werden.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 22%

---

# Aktivieren von eingehenden Quelldaten zum Ausfüllen von Kundenprofilen

Eingehende Daten aus Ihrem Quell-Connector können zur Anreicherung und zum Ausfüllen Ihrer [!DNL Real-Time Customer Profile] -Daten verwendet werden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Darüber hinaus erfordert dieses Tutorial, dass Sie bereits einen Quell-Connector erstellt und konfiguriert haben.  Eine Liste der Tutorials zum Erstellen verschiedener Connectoren in der Benutzeroberfläche finden Sie in der [Übersicht über Quell-Connectoren](../../home.md) .

## [!DNL Real-Time Customer Profile]-Daten ausfüllen

Um Kundenprofile anzureichern, muss das Quellschema des Zieldatensatzes für die Verwendung in [!DNL Real-Time Customer Profile] kompatibel sein. Ein kompatibles Schema erfüllt folgende Anforderungen:

- Das Schema weist mindestens ein Attribut auf, das als Identitätseigenschaft definiert wurde.
- Das Schema verfügt über eine Identitätseigenschaft, die als primäre Identität definiert wurde.
- Eine Zuordnung innerhalb des Datenflusses ist vorhanden, wobei die primäre Identität ein Zielattribut ist.

Klicken Sie im Arbeitsbereich &quot;Quellen&quot;auf die Registerkarte **[!UICONTROL Durchsuchen]** , um Ihre Basisverbindungen aufzulisten. Suchen Sie in der angezeigten Liste die Verbindung, die den Datenfluss enthält, mit dem Profile gefüllt werden sollen. Klicken Sie auf den Namen der Verbindung, um auf deren Details zuzugreifen.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Der Bildschirm **[!UICONTROL Source-Aktivität]** der Verbindung wird mit den Datensätzen angezeigt, in die die Verbindung Quelldaten aufnimmt. Klicken Sie auf den Namen des Datensatzes, den Sie für [!DNL Profile] aktivieren möchten.

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Der Bildschirm **[!UICONTROL Datensatzaktivität]** wird angezeigt. Die Spalte **[!UICONTROL Eigenschaften]** auf der rechten Seite des Bildschirms zeigt die Details des Datensatzes an und enthält einen Schalter **[!UICONTROL Profil]** sowie einen Link zum Schema, dem der Datensatz entspricht. Klicken Sie auf den Namen des Schemas, um dessen Komposition anzuzeigen.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

Der **[!UICONTROL Schema-Editor]** wird angezeigt und zeigt die Struktur des Schemas in der mittleren Arbeitsfläche an. Wählen Sie auf der Arbeitsfläche das Feld aus, das als primäre Identität festgelegt werden soll. Aktivieren Sie auf der angezeigten Registerkarte **[!UICONTROL Feldeigenschaften]** das Kontrollkästchen **[!UICONTROL Identität]** und dann **[!UICONTROL Primäre Identität]**. Wählen Sie abschließend einen entsprechenden **[!UICONTROL Identitäts-Namespace]** aus und klicken Sie dann auf **[!UICONTROL Anwenden]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Klicken Sie auf das Objekt der obersten Ebene der Schemastruktur und die Spalte **[!UICONTROL Schemaeigenschaften]** wird angezeigt. Aktivieren Sie das Schema für [!DNL Profile], indem Sie den Schalter **[!UICONTROL Profil]** umschalten. Klicken Sie auf **[!UICONTROL Speichern]** , um die Änderungen abzuschließen.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Nachdem das Schema für [!DNL Profile] aktiviert wurde, kehren Sie zum Bildschirm **[!UICONTROL Datensatzaktivität]** zurück und aktivieren Sie den Datensatz für [!DNL Profile], indem Sie auf den Umschalter **[!UICONTROL Profil]** in der Spalte **[!UICONTROL Eigenschaften]** klicken.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Wenn sowohl das Schema als auch der Datensatz für [!DNL Profile] aktiviert sind, werden jetzt auch die in diesen Datensatz erfassten Daten mit Kundenprofilen gefüllt.

>[!NOTE]
>
>Vorhandene Daten in einem kürzlich aktivierten Datensatz werden von [!DNL Profile] nicht genutzt.

## Nächste Schritte

In diesem Tutorial haben Sie eingehende Daten für [!DNL Profile] Population erfolgreich aktiviert. Weiterführende Informationen finden Sie in der [[!DNL Real-Time Customer Profile] Übersicht](../../../profile/home.md).
