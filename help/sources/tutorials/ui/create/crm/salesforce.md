---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Salesforce-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---


# Erstellen eines [!DNL Salesforce] Quellconnectors in der Benutzeroberfläche

Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte CRM-Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines [!DNL Salesforce] Quell-Connectors mithilfe der [!DNL Platform] Benutzeroberfläche.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL Salesforce] Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/crm.md)fortfahren.

### Erforderliche Berechtigungen erfassen

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `environmentUrl` | Die URL der [!DNL Salesforce] Quellinstanz. |
| `username` | Der Benutzername für das [!DNL Salesforce] Benutzerkonto. |
| `password` | Das Kennwort für das [!DNL Salesforce] Benutzerkonto. |
| `securityToken` | Das Sicherheits-Token für das [!DNL Salesforce] Benutzerkonto. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Salesforce-Dokument](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

## Verbinden Sie Ihr [!DNL Salesforce] Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues [!DNL Salesforce] Konto für die Verbindung zu erstellen [!DNL Platform].

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** , um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden eine Reihe von Quellen angezeigt, mit denen Sie ein eingehendes Konto erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse an, die ihnen zugeordnet sind.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie &quot; *[!UICONTROL Datenbanken]* &quot;die Option **[!UICONTROL Salesforce]** durch Klicken **auf das Pluszeichen (+)** , um einen neuen Salesforce-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/salesforce/catalog.png)

Die Seite *[!UICONTROL Verbindung mit Salesforce]* herstellen wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre [!DNL Salesforce] Anmeldeinformationen für die Verbindung ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis das neue Konto eingerichtet ist.

![connect](../../../../images/tutorials/create/salesforce/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verknüpfen, wählen Sie das [!DNL Salesforce] Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann in der rechten oberen Ecke die Option **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/salesforce/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Salesforce] Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in die Platform](../../dataflow/crm.md)zu bringen.