---
keywords: Experience Platform;Startseite;beliebte Themen;Eingehende Daten aktivieren;Profil ausfüllen;rtcp ausfüllen;Einheitliches Profil ausfüllen
solution: Experience Platform
title: Aktivieren Sie Eingangsquellendaten, um die Profil der Kunden in der Benutzeroberfläche zu füllen.
topic-legacy: overview
type: Tutorial
description: Eingehende Daten aus Ihrem Quell-Connector können zur Bereicherung und zum Ausfüllen Ihrer Echtzeit-Kundendaten verwendet werden.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 13%

---

# Aktivieren Sie eingehende Quelldaten, um Kundendaten zu füllen.

Eingehende Daten aus Ihrem Quellanschluss können zur Anreicherung und zum Ausfüllen Ihrer [!DNL Real-time Customer Profile]-Daten verwendet werden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Darüber hinaus erfordert dieses Lernprogramm, dass Sie bereits einen Quellanschluss erstellt und konfiguriert haben.  Eine Liste von Übungen zum Erstellen verschiedener Connectors in der Benutzeroberfläche finden Sie im [Übersicht über die Quellschnittstellen](../../home.md).

## Ihre [!DNL Real-time Customer Profile]-Daten füllen

Um die Profil der Zielgruppe zu bereichern, muss das Quell-Schema des Datasets für die Verwendung in [!DNL Real-time Customer Profile] kompatibel sein. Ein kompatibles Schema erfüllt folgende Anforderungen:

- Das Schema weist mindestens ein Attribut auf, das als Identitätseigenschaft definiert wurde.
- Das Schema verfügt über eine Identitätseigenschaft, die als primäre Identität definiert wurde.
- Eine Zuordnung innerhalb des Datenflusses ist vorhanden, wobei die primäre Zielgruppe ein Attribut ist.

Klicken Sie im Arbeitsbereich &quot;Quellen&quot;auf die Registerkarte **[!UICONTROL Durchsuchen]**, um Ihre Basisverbindungen Liste. Suchen Sie in der angezeigten Liste die Verbindung, die den Datenfluss enthält, mit dem Sie Profil füllen möchten. Klicken Sie auf den Namen der Verbindung, um deren Details anzuzeigen.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Der Bildschirm **[!UICONTROL Aktivität der Quelle]** der Verbindung wird angezeigt und zeigt die Datensätze an, in die die Verbindung Quelldaten einfügt. Klicken Sie auf den Namen des Datensatzes, den Sie für [!DNL Profile] aktivieren möchten.

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Der Bildschirm **[!UICONTROL Aktivität des Datensatzes]** wird angezeigt. Die Spalte **[!UICONTROL Properties]** auf der rechten Seite des Bildschirms zeigt die Details des Datensatzes an. Sie enthält einen Umschalter **[!UICONTROL Profil]** und einen Link zum Schema, dem der Datensatz entspricht. Klicken Sie auf den Namen des Schemas, um seine Zusammensetzung Ansicht.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

Der **[!UICONTROL Schema-Editor]** wird angezeigt und zeigt die Struktur des Schemas in der mittleren Arbeitsfläche an. Wählen Sie auf der Arbeitsfläche das Feld aus, das als primäre Identität festgelegt werden soll. Aktivieren Sie unter der angezeigten Registerkarte **[!UICONTROL Feldeigenschaften]** das Kontrollkästchen **[!UICONTROL Identität]** und **[!UICONTROL Primär identity]**. Wählen Sie abschließend einen geeigneten **[!UICONTROL Identity Namensraum]** und klicken Sie dann auf **[!UICONTROL Apply]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Klicken Sie auf das Objekt der obersten Ebene der Struktur des Schemas und die Spalte **[!UICONTROL Eigenschaften des Schemas]** wird angezeigt. Aktivieren Sie das Schema für [!DNL Profile], indem Sie den Umschalter **[!UICONTROL Profil]** umschalten. Klicken Sie auf **[!UICONTROL Speichern]**, um die Änderungen abzuschließen.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Nachdem das Schema für [!DNL Profile] aktiviert wurde, kehren Sie zum Bildschirm **[!UICONTROL Dataset-Aktivität]** zurück und aktivieren Sie den Datensatz für [!DNL Profile], indem Sie auf den Umschalter **[!UICONTROL Profil]** in der Spalte **[!UICONTROL Eigenschaften]** klicken.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Wenn sowohl das Schema als auch der Datensatz für [!DNL Profile] aktiviert sind, füllen die in diesen Datensatz erfassten Daten nun auch die Profil der Kunden aus.

>[!NOTE]
>
>Vorhandene Daten in einem kürzlich aktivierten Datensatz werden von [!DNL Profile] nicht genutzt.

## Nächste Schritte

In diesem Lernprogramm haben Sie eingehende Daten für [!DNL Profile] Population erfolgreich aktiviert. Weitere Informationen finden Sie unter [[!DNL Real-time Customer Profile] overview](../../../profile/home.md).
