---
keywords: Experience Platform;Startseite;beliebte Themen;Apache HDFS;HDFS;HDFS
solution: Experience Platform
title: Erstellen einer Apache HDFS-Source-Verbindung über die Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Apache Hadoop-Quellverbindung für das verteilte Dateisystem erstellen.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 35%

---

# Erstellen einer [!DNL Apache] HDFS-Quellverbindung über die Benutzeroberfläche

>[!NOTE]
>
>Der [!DNL Apache] HDFS-Connector befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Connectoren finden Sie ](../../../../home.md#terms-and-conditions) „Quellen - Übersicht“ .

Source-Connectoren in [!DNL Adobe Experience Platform] bieten die Möglichkeit, Daten aus externen Quellen nach einem bestimmten Zeitplan aufzunehmen. In diesem Tutorial werden Schritte zum Authentifizieren eines [!DNL Apache Hadoop Distributed File System]-Quell-Connectors (im Folgenden als „HDFS“ bezeichnet) über die [!DNL Platform]-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von [!DNL Platform] voraus.

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige HDFS-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [ eines Datenflusses ](../../dataflow/batch/cloud-storage.md).

### Sammeln erforderlicher Anmeldedaten

Um Ihren HDFS-Quell-Connector zu authentifizieren, müssen Sie Werte für die folgende Verbindungseigenschaft angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `url` | Die URL definiert Authentifizierungsparameter, die für die anonyme Verbindung mit HDFS erforderlich sind. Weitere Informationen zum Abrufen dieses Werts finden Sie im folgenden Dokument unter [HTTPS-Authentifizierung für HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## HDFS-Konto verbinden

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr HDFS-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Cloud]** die Option **[!UICONTROL Apache HDFS]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]** aus. Wählen Sie andernfalls **[!UICONTROL Daten hinzufügen]**, um einen neuen HDFS-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/hdfs/catalog.png)

Die **[!UICONTROL Verbinden mit HDFS]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre HDFS-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Verbinden](../../../../images/tutorials/create/hdfs/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das HDFS-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/hdfs/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem HDFS-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in zu importieren [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
