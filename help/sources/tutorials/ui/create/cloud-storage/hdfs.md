---
keywords: Experience Platform; Startseite; beliebte Themen; Apache HDFS; HDFS; Hdfs
solution: Experience Platform
title: Erstellen einer Apache HDFS-Quellverbindung in der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung des Apache Hadoop Distributed File System erstellen.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 35%

---

# Erstellen Sie eine [!DNL Apache] HDFS-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Apache] Der HDFS-Connector befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../../../home.md#terms-and-conditions) Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren.

Quell-Connectoren in [!DNL Adobe Experience Platform] ermöglichen die Erfassung von extern bezogenen Daten auf geplanter Basis. In diesem Tutorial werden Schritte zum Authentifizieren eines [!DNL Apache Hadoop Distributed File System] (nachstehend &quot;HDFS&quot; genannt) Quell-Connector, der den [!DNL Platform] -Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von [!DNL Platform] voraus.

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige HDFS-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zu [Datenfluss konfigurieren](../../dataflow/batch/cloud-storage.md).

### Sammeln erforderlicher Anmeldeinformationen

Um Ihren HDFS-Quell-Connector zu authentifizieren, müssen Sie Werte für die folgende Verbindungseigenschaft angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `url` | Die URL definiert Authentifizierungsparameter, die für die anonyme Verbindung mit HDFS erforderlich sind. Weitere Informationen zum Abrufen dieses Werts finden Sie im folgenden Dokument unter [HTTPS-Authentifizierung für HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Verbinden Sie Ihr HDFS-Konto.

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr HDFS-Konto mit [!DNL Platform].

Anmelden bei [Adobe Experience Platform](https://platform.adobe.com) und wählen Sie **[!UICONTROL Quellen]** über die linke Navigationsleiste, um auf die **[!UICONTROL Quellen]** Arbeitsbereich. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem **[!UICONTROL Cloud-Speicher]** category, select **[!UICONTROL Apache HDFS]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Daten hinzufügen]** um einen neuen HDFS-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/hdfs/catalog.png)

Die **[!UICONTROL Verbinden mit HDFS]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre HDFS-Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/hdfs/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das HDFS-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Nächste]** um fortzufahren.

![vorhanden](../../../../images/tutorials/create/hdfs/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem HDFS-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
