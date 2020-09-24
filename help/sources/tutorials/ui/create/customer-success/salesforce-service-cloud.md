---
keywords: Experience Platform;home;popular topics;Salesforce Service Cloud;salesforce service cloud
solution: Experience Platform
title: Erstellen eines Quell-Connectors für Salesforce Service Cloud über die Benutzeroberfläche
topic: overview
type: Tutorial
description: In diesem Lernprogramm werden Schritte zum Erstellen eines Salesforce Service Cloud-Quellconnectors (im Folgenden "SSC") mithilfe der Plattform-Benutzeroberfläche beschrieben.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 11%

---


# Create a [!DNL Salesforce Service Cloud] source connector in the UI

>[!NOTE]
>
>Der [!DNL Salesforce Service Cloud] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines [!DNL Salesforce Service Cloud] (im Folgenden &quot;SSC&quot;) Quellconnectors mithilfe der [!DNL Platform] Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model] (XDM) System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Echtzeit-Profil]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige SSC-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses fortfahren](../../dataflow/customer-success.md)

### Erforderliche Anmeldedaten sammeln

Für den Zugriff auf Ihr SSC-Konto auf [!DNL Platform]müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `username` | Der Benutzername für das Benutzerkonto. |
| `password` | Das Kennwort für das Benutzerkonto. |
| `securityToken` | Das Sicherheits-Token für das Benutzerkonto. |

Weitere Informationen zum Einstieg finden Sie in [ [!DNL Salesforce Service Cloud] diesem Dokument](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## Verbinden Sie Ihr [!DNL Salesforce Service Cloud] Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr SSC-Konto mit [!DNL Platform]zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den **[!UICONTROL Quellarbeitsbereich]** zuzugreifen. Im Anzeigebereich &quot; **[!UICONTROL Katalog]** &quot;werden verschiedene Quellen angezeigt, mit denen Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Customer Success]** die Option **[!UICONTROL Salesforce Service Cloud]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie &quot; **[!UICONTROL Konfigurieren]**&quot;aus. Wählen Sie andernfalls **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen SSC-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/ssc/catalog.png)

Die Seite **[!UICONTROL Verbindung mit der Salesforce Service Cloud]** herstellen wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im eingeblendeten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre SSC-Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/ssc/connect.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das SSC-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/ssc/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem SSC-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Kundenerfolgdaten zu erhalten [!DNL Platform]](../../dataflow/customer-success.md).