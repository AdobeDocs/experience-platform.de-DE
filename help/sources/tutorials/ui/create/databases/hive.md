---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen Sie einen Apache Hive auf einem Azurblauen HDInsights-Quellanschluss in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 14%

---


# Create an [!DNL Apache Hive] on [!DNL Azure HDInsights] source connector in the UI

>[!NOTE]
> The [!DNL Apache Hive] on [!DNL Azure HDInsights] connector is in beta. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines [!DNL Apache Hive] On- [!DNL Azure HDInsights] Source-Connectors mithilfe der [!DNL Platform] Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema Editor tutorial](../../../../../xdm/tutorials/create-schema-ui.md): Learn how to create custom schemas using the Schema Editor UI.
* [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Hive] Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses fortfahren](../../dataflow/databases.md)

### Erforderliche Anmeldedaten sammeln

In order to access your [!DNL Hive] account on [!DNL Platform], you must provide the following values:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Die IP-Adresse oder der Hostname des [!DNL Hive] Servers. |
| `username` | Der Benutzername, mit dem Sie auf den [!DNL Hive] Server zugreifen. |
| `password` | Das dem Benutzer zugeordnete Kennwort. |

For more information about getting started refer to [this Hive document](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted).

## Connect your [!DNL Hive] account

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues [!DNL Hive] Konto für die Verbindung zu erstellen [!DNL Platform].

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. The *[!UICONTROL Catalog]* screen displays a variety of sources for which you can create inbound account, and each source shows the number of existing accounts and dataset flows associated to them.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Under the *[!UICONTROL Databases]* category, select **[!UICONTROL Hive]** to expose an information bar on the right-hand side of your screen. The information bar provides a brief description for the selected source as well as options to connect with the source or view its documentation. To create a new inbound connection, select **[!UICONTROL Connect source]**.

![Katalog](../../../../images/tutorials/create/hive/catalog.png)

The *[!UICONTROL Connect to Hive]* page appears. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### New account

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre [!DNL Hive] Anmeldeinformationen für die Verbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis das neue Konto eingerichtet ist.

![connect](../../../../images/tutorials/create/hive/new.png)

### Vorhandenes Konto

To connect an existing account, select the [!DNL Hive] account you want to connect with, then select **[!UICONTROL Next]** to proceed.

![existing](../../../../images/tutorials/create/hive/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Hive] Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in Plattform](../../dataflow/databases.md)zu übertragen.