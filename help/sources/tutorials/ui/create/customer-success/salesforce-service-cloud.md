---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Quell-Connectors für Salesforce Service Cloud über die Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 16%

---


# Create a [!DNL Salesforce Service Cloud] source connector in the UI

>[!NOTE]
>Der [!DNL Salesforce Service Cloud] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. This tutorial provides steps for creating a [!DNL Salesforce Service Cloud] (hereinafter referred to as &quot;SSC&quot;) source connector using the [!DNL Platform] user interface.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema Editor tutorial](../../../../../xdm/tutorials/create-schema-ui.md): Learn how to create custom schemas using the Schema Editor UI.
* [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

If you already have a valid SSC connection, you may skip the remainder of this document and proceed to the tutorial on [configuring a dataflow](../../dataflow/customer-success.md)

### Erforderliche Anmeldedaten sammeln

Für den Zugriff auf Ihr SSC-Konto auf [!DNL Platform]müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `username` | Der Benutzername für das Benutzerkonto. |
| `password` | Das Kennwort für das Benutzerkonto. |
| `securityToken` | Das Sicherheits-Token für das Benutzerkonto. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Salesforce Service Cloud-Dokument](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## Verbinden Sie Ihr [!DNL Salesforce Service Cloud] Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues SSC-Konto für die Verbindung zu erstellen [!DNL Platform].

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden eine Reihe von Quellen angezeigt, für die Sie ein Inbound-Konto erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse, die ihnen zugeordnet sind.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie *[!UICONTROL Customer Success]* die Option **[!UICONTROL Salesforce Service Cloud]** , um eine Informationsleiste auf der rechten Seite Ihres Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelle oder Ansicht der zugehörigen Dokumentation. Um eine neue eingehende Verbindung zu erstellen, wählen Sie **[!UICONTROL Hinzufügen Daten]**.

![catalog](../../../../images/tutorials/create/ssc/catalog.png)

Die Seite *[!UICONTROL Verbindung mit der Salesforce Service Cloud]* herstellen wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

If you are using new credentials, select **[!UICONTROL New account]**. Geben Sie im eingeblendeten Eingabebild einen Namen, eine optionale Beschreibung und Ihre SSC-Anmeldeinformationen für die Verbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis das neue Konto eingerichtet ist.

![connect](../../../../images/tutorials/create/ssc/connect.png)

### Vorhandenes Konto

To connect an existing account, select the SSC account you want to connect with, then select **[!UICONTROL Next]** to proceed.

![existing](../../../../images/tutorials/create/ssc/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem SSC-Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Kundenerfolgdaten in die Plattform](../../dataflow/customer-success.md)zu übertragen.