---
keywords: Experience Platform;Home;beliebte Themen;Amazon Redshift;amazon Rotverschiebung;Redshift;Rotverschiebung
solution: Experience Platform
title: Erstellen einer Amazon Redshift-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine Amazon Redshift-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 9%

---

# Erstellen einer [!DNL Amazon Redshift]-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
>Der [!DNL Amazon Redshift]-Anschluss befindet sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines [!DNL Amazon Redshift]-Quellconnectors (nachstehend &quot;a1/>&quot;genannt) mithilfe der [!DNL Platform]-Benutzeroberfläche beschrieben.[!DNL Redshift]

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Redshift]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial [Konfigurieren eines Datenniedrig](../../dataflow/databases.md) fortfahren.

### Erforderliche Anmeldedaten sammeln

Um auf Ihr [!DNL Redshift]-Konto bei [!DNL Platform] zuzugreifen, müssen Sie die folgenden Werte angeben:

| **Berechtigung** | **Beschreibung** |
| -------------- | --------------- |
| `server` | Der mit Ihrem [!DNL Redshift]-Konto verknüpfte Server. |
| `username` | Der mit Ihrem [!DNL Redshift]-Konto verknüpfte Benutzername. |
| `password` | Das Ihrem [!DNL Redshift]-Konto zugeordnete Kennwort. |
| `database` | Die [!DNL Redshift]-Datenbank, auf die Sie zugreifen. |

Weitere Informationen zum Einstieg finden Sie unter [this [!DNL Redshift] Dokument](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

## Verbinden Sie Ihr [!DNL Redshift]-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Redshift]-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Reihe von Quellen an, für die Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** **[!UICONTROL Amazon Redshift]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen [!DNL Redshift]-Connector zu erstellen.

![](../../../../images/tutorials/create/redshift/catalog.png)

Die Seite **[!UICONTROL Mit Amazon Redshift]** verbinden wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre [!DNL Redshift]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![](../../../../images/tutorials/create/redshift/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Redshift]-Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![](../../../../images/tutorials/create/redshift/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Redshift]-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und [einen Datendurchlauf konfigurieren, um Daten in [!DNL Platform]](../../dataflow/databases.md) zu übertragen.
