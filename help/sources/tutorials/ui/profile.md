---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aktivieren Sie eingehende Quelldaten, um Kundendaten zu füllen.
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---


# Aktivieren Sie eingehende Quelldaten, um Kundendaten zu füllen.

Eingehende Daten aus Ihrem Quellanschluss können zur Anreicherung und zum Ausfüllen Ihrer [!DNL Real-time Customer Profile] Daten verwendet werden.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

- [Erlebnis-Datenmodell (XDM)-System](../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Zusammensetzung](../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   - [Schema-Editor-Lernprogramm](../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [Echtzeit-Profil](../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Darüber hinaus erfordert dieses Lernprogramm, dass Sie bereits einen Quellanschluss erstellt und konfiguriert haben.  Eine Liste von Übungen zum Erstellen verschiedener Connectors in der Benutzeroberfläche finden Sie in der Übersicht über die [Quell-Connectors](../../home.md).

## Ihre [!DNL Real-time Customer Profile] Daten ausfüllen

Um die Profile von Kunden zu bereichern, muss das Quell-Schema des Zielgruppe-Datensatzes für die Verwendung in [!DNL Real-time Customer Profile]kompatibel sein. Ein kompatibles Schema erfüllt folgende Anforderungen:

- Das Schema hat mindestens ein Attribut, das als Identitätseigenschaft angegeben wurde.
- Das Schema verfügt über eine Identitätseigenschaft, die als primäre Identität definiert ist.
- Eine Zuordnung innerhalb des Datenflusses ist vorhanden, wobei die primäre Zielgruppe ein Attribut ist.

Klicken Sie im Quellenarbeitsbereich auf die Registerkarte &quot; **[!UICONTROL Durchsuchen]** &quot;, um Ihre Basisverbindungen Liste. Suchen Sie in der angezeigten Liste die Verbindung, die den Datenfluss enthält, mit dem Sie Profil füllen möchten. Klicken Sie auf den Namen der Verbindung, um deren Details anzuzeigen.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Der Bildschirm &quot; *[!UICONTROL Quelldaten]* &quot;der Verbindung wird angezeigt und zeigt die Datensätze an, in die die Verbindung Quelldaten eingibt. Klicken Sie auf den Namen des Datensatzes, für den Sie aktivieren möchten [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Der Bildschirm &quot; *[!UICONTROL Aktivität]* des Datensatzes&quot;wird angezeigt. In der Spalte &quot; *[!UICONTROL Eigenschaften]* &quot;auf der rechten Seite des Bildschirms werden die Details des Datensatzes angezeigt. Sie enthält einen **[!UICONTROL Profil]** -Schalter und einen Link zum Schema, dem der Datensatz entspricht. Klicken Sie auf den Namen des Schemas, um seine Zusammensetzung Ansicht.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

Der *[!UICONTROL Schema-Editor]* wird angezeigt und zeigt die Struktur des Schemas in der mittleren Arbeitsfläche an. Wählen Sie auf der Arbeitsfläche das Feld aus, das als primäre Identität festgelegt werden soll. Aktivieren Sie unter der angezeigten Registerkarte &quot; *[!UICONTROL Feldeigenschaften]* &quot;das Kontrollkästchen &quot; **[!UICONTROL Identität]** &quot;und wählen Sie anschließend die Option &quot; **[!UICONTROL Primär-Identität]**&quot;. Wählen Sie schließlich einen entsprechenden **[!UICONTROL Identitäts-Namensraum]** und klicken Sie dann auf **[!UICONTROL Übernehmen]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Klicken Sie auf das Objekt auf der obersten Ebene der Struktur des Schemas, und die Spalte mit den Eigenschaften des *[!UICONTROL Schemas]* wird angezeigt. Aktivieren Sie das Schema [!DNL Profile] durch Umschalten des **[!UICONTROL Profils]** . Klicken Sie auf **[!UICONTROL Speichern]** , um die Änderungen abzuschließen.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Kehren Sie nach Aktivierung des Schemas zum Bildschirm &quot; [!DNL Profile]DataSet-Aktivität *[!UICONTROL &quot;zurück und aktivieren Sie den Datensatz,]* indem Sie auf den [!DNL Profile] Profil **[!UICONTROL -Umschalter in der Spalte &quot;]** Eigenschaften ** &quot;klicken.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Wenn sowohl das Schema als auch der Datensatz aktiviert sind, [!DNL Profile]füllen die in diesen Datensatz erfassten Daten nun auch die Profil der Kunden aus.

>[!NOTE] Vorhandene Daten in einem kürzlich aktivierten Datensatz werden nicht von [!DNL Profile]

## Nächste Schritte

Indem Sie diesem Tutorial folgen, haben Sie eingehende Daten für die [!DNL Profile] Population erfolgreich aktiviert. Weitere Informationen finden Sie in der Übersicht über das [Echtzeit-Profil](../../../profile/home.md).