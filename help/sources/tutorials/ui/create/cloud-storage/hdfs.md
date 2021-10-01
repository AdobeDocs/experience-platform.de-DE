---
keywords: Experience Platform; Startseite; beliebte Themen; Apache HDFS; HDFS; Hdfs
solution: Experience Platform
title: Erstellen einer Apache HDFS-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung des Apache Hadoop Distributed File System erstellen.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 9%

---

# Erstellen einer [!DNL Apache] HDFS-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
>Der [!DNL Apache] HDFS-Connector befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie unter [Quellen - Übersicht](../../../../home.md#terms-and-conditions) .

Quell-Connectoren in [!DNL Adobe Experience Platform] bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. Dieses Tutorial enthält Schritte zum Authentifizieren eines Quell-Connectors für [!DNL Apache Hadoop Distributed File System] (im Folgenden &quot;HDFS&quot; genannt) mithilfe der [!DNL Platform]-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Verständnis der folgenden Komponenten von [!DNL Platform] voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) zum Schema Editor: Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige HDFS-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses [fortfahren.](../../dataflow/batch/cloud-storage.md)

### Erforderliche Anmeldedaten sammeln

Um Ihren HDFS-Quell-Connector zu authentifizieren, müssen Sie Werte für die folgende Verbindungseigenschaft angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `url` | Die URL definiert Authentifizierungsparameter, die für die anonyme Verbindung mit HDFS erforderlich sind. Weitere Informationen zum Abrufen dieses Werts finden Sie im folgenden Dokument unter [HTTPS-Authentifizierung für HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Verbinden Sie Ihr HDFS-Konto.

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr HDFS-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** enthält eine Vielzahl von Quellen, für die Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Cloud-Speicher]** die Option **[!UICONTROL Apache HDFS]** aus. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]** aus. Klicken Sie andernfalls auf **[!UICONTROL Daten hinzufügen]** , um einen neuen HDFS-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/hdfs/catalog.png)

Die Seite **[!UICONTROL Verbindung zu HDFS]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre HDFS-Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** aus und lassen Sie dann etwas Zeit für die Einrichtung der neuen Verbindung zu.

![connect](../../../../images/tutorials/create/hdfs/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das HDFS-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhandene](../../../../images/tutorials/create/hdfs/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem HDFS-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in [!DNL Platform]](../../dataflow/batch/cloud-storage.md) zu übertragen.
