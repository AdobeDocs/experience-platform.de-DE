---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Erstellen eines Microsoft Dynamics-Quellconnectors in der Benutzeroberfläche
topic: overview
type: Tutorial
description: In diesem Lernprogramm werden Schritte zum Erstellen eines Microsoft Dynamics-Quellconnectors (nachfolgend "Dynamics") mithilfe der Plattform-Benutzeroberfläche beschrieben.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 10%

---


# Create a [!DNL Microsoft Dynamics] source connector in the UI

Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte CRM-Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines [!DNL Microsoft Dynamics] (im Folgenden &quot;[!DNL Dynamics]&quot;) Quell-Connectors mithilfe der [!DNL Platform] Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model] (XDM) System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Echtzeit-Profil]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL Dynamics] Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/crm.md)fortfahren.

### Erforderliche Anmeldedaten sammeln

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `serviceUri` | Die Dienst-URL Ihrer [!DNL Dynamics] Instanz. |
| `username` | Der Benutzername für Ihr [!DNL Dynamics] Benutzerkonto. |
| `password` | Das Kennwort für Ihr [!DNL Dynamics] Konto. |

Weitere Informationen zum Einstieg finden Sie in [ [!DNL Dynamics] diesem Dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Verbinden Sie Ihr [!DNL Dynamics] Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Dynamics] Konto mit [!DNL Platform]zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den **[!UICONTROL Quellarbeitsbereich]** zuzugreifen. Im Anzeigebereich &quot; **[!UICONTROL Katalog]** &quot;werden verschiedene Quellen angezeigt, mit denen Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** die Option **[!UICONTROL Dynamik]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie &quot; **[!UICONTROL Konfigurieren]**&quot;aus. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen [!DNL Dynamics] Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Die Seite &quot; **[!UICONTROL Verbindung mit Dynamik]** herstellen&quot;wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im eingeblendeten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre [!DNL Dynamics] Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/ms-dynamics/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verknüpfen, wählen Sie das [!DNL Dynamics] Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann in der rechten oberen Ecke die Option **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Dynamics] Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in dieses Lernprogramm [!DNL Platform]](../../dataflow/crm.md)einzubringen.