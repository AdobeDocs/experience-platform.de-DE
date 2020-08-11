---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Create a Phoenix source connector in the UI
topic: overview
translation-type: tm+mt
source-git-commit: 598b29f681ac930a4e1781f7f298608c8344d807
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 13%

---


# Create a [!DNL Phoenix] source connector in the UI

>[!NOTE]
> Der [!DNL Phoenix] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines [!DNL Phoenix] Quell-Connectors mithilfe der [!DNL Platform] Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Phoenix] Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses fortfahren](../../dataflow/databases.md)

### Erforderliche Anmeldedaten sammeln

Um auf Ihr [!DNL Phoenix] Konto zugreifen zu können, müssen Sie die folgenden Werte angeben [!DNL Platform]:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Die IP-Adresse oder der Hostname des [!DNL Phoenix] Servers. |
| `port` | Der TCP-Anschluss, den der [!DNL Phoenix] Server verwendet, um auf Clientverbindungen zu warten. Wenn Sie eine Verbindung herstellen, [!DNL Azure HDInsights]geben Sie den Anschluss als 443 an. |
| `httpPath` | Die Teil-URL, die dem [!DNL Phoenix] Server entspricht. Geben Sie /hbasephoenix0 an, wenn Sie den [!DNL Azure HDInsights] Cluster verwenden. |
| `username` | Der Benutzername, mit dem Sie auf den [!DNL Phoenix] Server zugreifen. |
| `password` | Das dem Benutzer zugeordnete Kennwort. |
| `enableSsl` | A toggle that specifies whether he connections to the server are encrypted using SSL. |

Weitere Informationen zum Einstieg finden Sie in [diesem Phoenix-Dokument](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Verbinden Sie Ihr Phoenix-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues [!DNL Phoenix] Konto für die Verbindung zu erstellen [!DNL Platform].

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. The *[!UICONTROL Catalog]* screen displays a variety of sources for which you can create inbound account, and each source shows the number of existing accounts and dataset flows associated to them.

You can select the appropriate category from the catalog on the left-hand side of your screen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie &quot; *[!UICONTROL Datenbanken]* &quot;die Option &quot; **[!UICONTROL Phoenix]** &quot;aus, um eine Informationsleiste auf der rechten Seite des Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelle oder Ansicht der zugehörigen Dokumentation. To create a new inbound connection, select **[!UICONTROL Add data]**.

![Katalog](../../../../images/tutorials/create/phoenix/catalog.png)

The *[!UICONTROL Connect to Phoenix]* page appears. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

If you are using new credentials, select **[!UICONTROL New account]**. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre [!DNL Phoenix] Anmeldeinformationen für die Verbindung ein. When finished, select **[!UICONTROL Connect]** and then allow some time for the new account to establish.

![connect](../../../../images/tutorials/create/phoenix/new.png)

### Existing account

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Phoenix] Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/phoenix/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Phoenix] Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in Plattform](../../dataflow/databases.md)zu übertragen.