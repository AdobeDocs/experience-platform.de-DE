---
keywords: Experience Platform;home;popular topics;DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: Erstellen einer IBM DB2-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine IBM DB2-Quellverbindung mithilfe der Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 34%

---

# Erstellen einer IBM DB2-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
> Der IBM DB2-Connector befindet sich in der Betaphase. Siehe [Quellen – Übersicht](../../../../home.md#terms-and-conditions), um weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren zu erhalten.

Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. In diesem Tutorial werden die Schritte zum Erstellen eines Quell-Connectors für IBM DB2 (im Folgenden &quot;DB2&quot; genannt) mithilfe des [!DNL Platform] -Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige DB2-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zu [Datenfluss konfigurieren](../../dataflow/databases.md).

### Sammeln erforderlicher Anmeldeinformationen

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service] API.

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `server` | Der Name des DB2-Servers. Sie können die Anschlussnummer angeben, die auf den Servernamen folgt, der durch einen Doppelpunkt getrennt ist. Beispiel: server:port. |
| `database` | Der Name der DB2-Datenbank. |
| `username` | Der Benutzername, der für die Verbindung mit der DB2-Datenbank verwendet wird. |
| `password` | Das Kennwort für das Benutzerkonto, das Sie für den Benutzernamen angegeben haben. |

Weitere Informationen zu den ersten Schritten finden Sie unter [Dieses DB2-Dokument](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## Verbinden Ihres IBM DB2-Kontos

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr DB2-Konto mit [!DNL Platform].

Anmelden bei [Adobe Experience Platform](https://platform.adobe.com) und wählen Sie **[!UICONTROL Quellen]** über die linke Navigationsleiste, um auf die **[!UICONTROL Quellen]** Arbeitsbereich. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem **[!UICONTROL Datenbanken]** category, select **[!UICONTROL IBM DB2]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Daten hinzufügen]** , um einen neuen DB2-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/ibm-db2/catalog.png)

Die **[!UICONTROL Verbindung zu IBM DB2 herstellen]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre DB2-Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und dann etwas Zeit für die Einrichtung der neuen Verbindung.

![connect](../../../../images/tutorials/create/ibm-db2/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das DB2-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Nächste]** um fortzufahren.

![vorhanden](../../../../images/tutorials/create/ibm-db2/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem DB2-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen [Datenfluss konfigurieren, um Daten in zu importieren [!DNL Platform]](../../dataflow/databases.md).
