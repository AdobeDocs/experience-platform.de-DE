---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines GreenPlum-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: ec2d0a33e0ae92a3153b7bdcad29734e487a0439
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 9%

---


# Create a [!DNL GreenPlum] source connector in the UI

>[!NOTE]
> Der [!DNL GreenPlum] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines [!DNL GreenPlum] Quell-Connectors mithilfe der [!DNL Platform] Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model] (XDM) System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Echtzeit-Profil]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL GreenPlum] Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Lernprogramm zur [Konfiguration eines Datenflusses](../../dataflow/databases.md)fortfahren.

### Erforderliche Anmeldedaten sammeln

The following sections provide additional information that you will need to know in order to successfully connect to [!DNL GreenPlum] using the [!DNL Flow Service] API.

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, mit der eine Verbindung zu Ihrer [!DNL GreenPlum] Instanz hergestellt wird. Das Verbindungszeichenfolgen-Muster für [!DNL GreenPlum] ist `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem GreenPlum-Dokument](https://gpdb.docs.pivotal.io/580/security-guide/topics/Authenticate.html#topic_fzv_wb2_jr__config_ssl_client_conn).

## Verbinden Sie Ihr [!DNL GreenPlum] Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL GreenPlum] Konto mit [!DNL Platform]zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den **[!UICONTROL Quellarbeitsbereich]** zuzugreifen. Im Anzeigebereich &quot; **[!UICONTROL Katalog]** &quot;werden verschiedene Quellen angezeigt, mit denen Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** die Option **[!UICONTROL GreenPlum]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie &quot; **[!UICONTROL Konfigurieren]**&quot;aus. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen [!DNL GreenPlum] Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/greenplum/catalog.png)

Die Seite &quot; **[!UICONTROL Verbindung zu GreenPlum]** herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im eingeblendeten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre [!DNL GreenPlum] Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/greenplum/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verknüpfen, wählen Sie das [!DNL GreenPlum] Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann in der rechten oberen Ecke die Option **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/greenplum/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL GreenPlum] Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in dieses Lernprogramm [!DNL Platform]](../../dataflow/databases.md)einzubeziehen.