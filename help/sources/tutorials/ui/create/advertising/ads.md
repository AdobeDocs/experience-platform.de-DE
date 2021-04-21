---
keywords: Experience Platform;Home;beliebte Themen;Google AdWords;Google AdWords-Quellanschluss;Google Adwords-Connector
solution: Experience Platform
title: Erstellen einer Google AdWords-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Google AdWords-Quellverbindung erstellen.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 9%

---

# Erstellen einer [!DNL Google AdWords]-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
>Der [!DNL Google AdWords]-Anschluss befindet sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines [!DNL Google AdWords]-Quellconnectors mithilfe der [!DNL Platform]-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Google AdWords]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial [Konfigurieren eines Datenflusses](../../dataflow/payments.md) fortfahren

### Erforderliche Anmeldedaten sammeln

Um auf Ihr [!DNL Google AdWords]-Konto [!DNL Platform] zuzugreifen, müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `clientCustomerId` | Die Client-Kunden-ID des [!DNL AdWords]-Kontos. |
| `developerToken` | Das mit dem Managerkonto verknüpfte Entwicklertoken. |
| `refreshToken` | Das Aktualisierungstoken, das von [!DNL Google] zum Autorisieren des Zugriffs auf [!DNL AdWords] erhalten wurde. |
| `clientId` | Die Client-ID der Anwendung [!DNL Google], die zum Abrufen des Aktualisierungstokens verwendet wird. |
| `clientSecret` | Das Clientgeheimnis der [!DNL Google]-Anwendung, mit der das Aktualisierungstoken erfasst wird. |

Weitere Informationen zum Einstieg finden Sie in diesem [[!DNL Google AdWords] Dokument](https://developers.google.com/adwords/api/docs/guides/authentication).

## Verbinden Sie Ihr [!DNL Google AdWords]-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Google AdWords]-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Reihe von Quellen an, für die Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Werbung]** **[!UICONTROL Google AdWords]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen [!DNL Google AdWords]-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/ads/catalog.png)

Die Seite **[!UICONTROL Verbindung mit Google AdWords]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre [!DNL Google AdWords]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Google AdWords]-Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![existing](../../../../images/tutorials/create/ads/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Google AdWords]-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und [einen Datendurchlauf konfigurieren, um Anzeigendaten in [!DNL Platform]](../../dataflow/advertising.md) zu übertragen.
