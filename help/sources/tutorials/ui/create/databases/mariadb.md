---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Quell-Connectors für MariaDB über die Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 17%

---


# Create a [!DNL MariaDB] source connector in the UI

>[!NOTE]
>
> Der [!DNL MariaDB] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines Maria DB-Quell-Connectors mithilfe der [!DNL Platform] Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model] (XDM) System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine [!DNL MariaDB] Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Lernprogramm zur [Konfiguration eines Datenflusses](../../dataflow/databases.md)fortfahren.

### Erforderliche Anmeldedaten sammeln

Um auf Ihr [!DNL MariaDB] Konto zugreifen zu können, müssen Sie [!DNL Platform]den folgenden Wert angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die mit Ihrer MariaDB-Authentifizierung verknüpfte Verbindungszeichenfolge. Das Muster für die [!DNL MariaDB] Verbindungszeichenfolge lautet: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [[!DNL MariaDB] Dokument](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

## Verbinden Sie Ihr [!DNL Maria DB] Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Maria DB] Konto mit [!DNL Platform]zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den **[!UICONTROL Quellarbeitsbereich]** zuzugreifen. Im Anzeigebereich &quot; **[!UICONTROL Katalog]** &quot;werden verschiedene Quellen angezeigt, mit denen Sie ein Konto erstellen können.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** die Option **[!UICONTROL Maria DB]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie &quot; **[!UICONTROL Konfigurieren]**&quot;aus. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen [!DNL Maria DB] Connector zu erstellen.

![](../../../../images/tutorials/create/maria-db/catalog.png)

Die Seite &quot; **[!UICONTROL Verbindung mit Maria DB]** herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im eingeblendeten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre [!DNL MariaDB] Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![](../../../../images/tutorials/create/maria-db/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL MariaDB] Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![](../../../../images/tutorials/create/maria-db/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL MariaDB] Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in dieses Lernprogramm [!DNL Platform]](../../dataflow/databases.md)einzubeziehen.