---
keywords: Experience Platform;home;popular topics;DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: Erstellen einer IBM DB2-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine IBM DB2-Quellverbindung mithilfe der Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 11%

---

# Erstellen einer IBM DB2-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
> Der IBM DB2-Connector befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie unter [Quellen - Übersicht](../../../../home.md#terms-and-conditions) .

Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. In diesem Tutorial werden die Schritte zum Erstellen eines Quell-Connectors für IBM DB2 (im Folgenden &quot;DB2&quot;) mithilfe der [!DNL Platform]-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) zum Schema Editor: Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige DB2-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses [fortfahren.](../../dataflow/databases.md)

### Erforderliche Anmeldedaten sammeln

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mit der [!DNL Flow Service]-API erfolgreich eine Verbindung zu DB2 herstellen zu können.

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `server` | Der Name des DB2-Servers. Sie können die Anschlussnummer angeben, die auf den Servernamen folgt, der durch einen Doppelpunkt getrennt ist. Beispiel: server:port. |
| `database` | Der Name der DB2-Datenbank. |
| `username` | Der Benutzername, der für die Verbindung mit der DB2-Datenbank verwendet wird. |
| `password` | Das Kennwort für das Benutzerkonto, das Sie für den Benutzernamen angegeben haben. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem DB2-Dokument](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## Verbinden Ihres IBM DB2-Kontos

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr DB2-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** enthält eine Vielzahl von Quellen, für die Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** die Option **[!UICONTROL IBM DB2]** aus. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]** aus. Klicken Sie andernfalls auf **[!UICONTROL Daten hinzufügen]** , um einen neuen DB2-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/ibm-db2/catalog.png)

Die Seite **[!UICONTROL Verbindung zu IBM DB2]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre DB2-Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/ibm-db2/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das DB2-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhandene](../../../../images/tutorials/create/ibm-db2/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem DB2-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in [!DNL Platform]](../../dataflow/databases.md) zu übertragen.
