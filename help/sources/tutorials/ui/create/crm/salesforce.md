---
keywords: Experience Platform;home;popular topics;Salesforce;salesforce
solution: Experience Platform
title: Erstellen eines Salesforce-Quellconnectors in der Benutzeroberfläche
topic: overview
type: Tutorial
description: In diesem Lernprogramm werden Schritte zum Erstellen eines Salesforce-Quell-Connectors mithilfe der Plattform-Benutzeroberfläche beschrieben.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 10%

---


# Create a [!DNL Salesforce] source connector in the UI

Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte CRM-Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines [!DNL Salesforce] Quell-Connectors mithilfe der [!DNL Platform] Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL Salesforce] Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/crm.md)fortfahren.

### Erforderliche Anmeldedaten sammeln

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `environmentUrl` | The URL of the [!DNL Salesforce] source instance. |
| `username` | Der Benutzername für das [!DNL Salesforce] Benutzerkonto. |
| `password` | Das Kennwort für das [!DNL Salesforce] Benutzerkonto. |
| `securityToken` | Das Sicherheits-Token für das [!DNL Salesforce] Benutzerkonto. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Salesforce-Dokument](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

## Verbinden Sie Ihr [!DNL Salesforce] Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Salesforce] Konto mit [!DNL Platform]zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den **[!UICONTROL Quellarbeitsbereich]** zuzugreifen. Im Anzeigebereich &quot; **[!UICONTROL Katalog]** &quot;werden verschiedene Quellen angezeigt, mit denen Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** die Option **[!UICONTROL Salesforce]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie &quot; **[!UICONTROL Konfigurieren]**&quot;aus. Wählen Sie andernfalls **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen Salesforce-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/salesforce/catalog.png)

Die Seite **[!UICONTROL Verbindung mit Salesforce]** herstellen wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im eingeblendeten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre [!DNL Salesforce] Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/salesforce/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verknüpfen, wählen Sie das [!DNL Salesforce] Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann in der rechten oberen Ecke die Option **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/salesforce/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Salesforce] Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in dieses Lernprogramm [!DNL Platform]](../../dataflow/crm.md)einzubringen.