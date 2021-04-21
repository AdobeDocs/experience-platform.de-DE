---
keywords: Experience Platform;Home;beliebte Themen;Azurblauer Data Explorer;Azure Data Explorer;Data Explorer;Data Explorer
solution: Experience Platform
title: Erstellen einer Azurblauen Data Explorer-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine Azurblase-Quellverbindung mit der Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 561bf948-fc92-4401-8631-e2a408667507
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 8%

---

# Erstellen einer [!DNL Azure Data Explorer]-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
> Der [!DNL Azure Data Explorer]-Anschluss befindet sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines [!DNL Azure Data Explorer]-Quellconnectors (nachstehend &quot;a1/>&quot;genannt) mithilfe der [!DNL Platform]-Benutzeroberfläche beschrieben.[!DNL Data Explorer]

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Data Explorer]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial [Konfigurieren eines Datenniedrig](../../dataflow/databases.md) fortfahren.

### Erforderliche Anmeldedaten sammeln

Um auf Ihr [!DNL Data Explorer]-Konto bei [!DNL Platform] zuzugreifen, müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `endpoint` | Der Endpunkt des [!DNL Data Explorer]-Servers. |
| `database` | Der Name der [!DNL Data Explorer]-Datenbank. |
| `tenant` | Die eindeutige Mandanten-ID, mit der eine Verbindung zur [!DNL Data Explorer]-Datenbank hergestellt wird. |
| `servicePrincipalId` | Die Prinzipal-ID des Unique Service, mit der eine Verbindung zur [!DNL Data Explorer]-Datenbank hergestellt wird. |
| `servicePrincipalKey` | Der Hauptschlüssel für den eindeutigen Dienst, mit dem eine Verbindung zur [!DNL Data Explorer]-Datenbank hergestellt wird. |

Weitere Informationen zum Einstieg finden Sie unter [this [!DNL Data Explorer] Dokument](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Verbinden Sie Ihr [!DNL Azure Data Explorer]-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Data Explorer]-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Reihe von Quellen an, für die Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** **[!UICONTROL Azurblauer Data Explorer]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen Data Explorer-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/data-explorer/catalog.png)

Die Seite **[!UICONTROL Verbindung mit dem Azurblauen Data Explorer]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre [!DNL Data Explorer]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/data-explorer/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Data Explorer]-Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![existing](../../../../images/tutorials/create/data-explorer/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Data Explorer]-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und [einen Datendurchlauf konfigurieren, um Daten in [!DNL Platform]](../../dataflow/databases.md) zu übertragen.
