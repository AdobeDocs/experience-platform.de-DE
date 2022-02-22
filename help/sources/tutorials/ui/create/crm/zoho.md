---
keywords: Experience Platform; Startseite; beliebte Themen; Zoho CRM; Zoho crm; Zoho; Zoho
solution: Experience Platform
title: Erstellen einer Zoho CRM-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Zoho CRM-Quellverbindung erstellen.
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: 46b2fd6bc715bf1d8ccfeed576a2a2d193f92edd
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 11%

---

# Erstellen Sie eine [!DNL Zoho CRM] Quellverbindung in der Benutzeroberfläche

Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, externe CRM-Daten planmäßig zu erfassen. In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Zoho CRM] Quell-Connector mit [!DNL Platform] -Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Der standardisierte Rahmen, durch den [!DNL Experience Platform] organisiert Kundenerlebnisdaten.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial zum Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Zoho CRM] -Konto verwenden, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Datenfluss konfigurieren](../../dataflow/crm.md).

### Erforderliche Anmeldedaten sammeln

Um eine Verbindung herzustellen [!DNL Zoho CRM] in Platform angeben, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| --- | --- |
| Endpunkt | Der Endpunkt der [!DNL Zoho CRM] -Server, an den Sie Ihre Anforderung senden. |
| Konto-URL | Die Konto-URL wird verwendet, um Ihre Zugriffs- und Aktualisierungstoken zu generieren. Die URL muss domänenspezifisch sein. |
| Client-ID | Die Client-ID, die Ihrer [!DNL Zoho CRM] Benutzerkonto. |
| Client Secret (Client-Geheimnis) | Das Client-Geheimnis, das Ihrem [!DNL Zoho CRM] Benutzerkonto. |
| Zugriffstoken | Das Zugriffstoken autorisiert Ihren sicheren und temporären Zugriff auf Ihre [!DNL Zoho CRM] -Konto. |
| Token aktualisieren | Ein Aktualisierungstoken ist ein Token, mit dem ein neues Zugriffstoken generiert wird, sobald Ihr Zugriffstoken abgelaufen ist. |

Weitere Informationen zu diesen Anmeldedaten finden Sie in der Dokumentation unter [[!DNL Zoho CRM] Authentifizierung](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Verbinden Sie Ihre [!DNL Zoho CRM] account

Nachdem Sie die erforderlichen Anmeldedaten erfasst haben, können Sie die folgenden Schritte ausführen, um Ihre [!DNL Zoho CRM] Konto [!DNL Platform].

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über die linke Navigationsleiste, um auf die [!UICONTROL Quellen] Arbeitsbereich. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem [!UICONTROL CRM] category, select **[!UICONTROL Zoho CRM]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/zoho/catalog.png)

Die **[!UICONTROL CRM-Konto für Zoho verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie die [!DNL Zoho CRM] Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, wählen Sie **[!UICONTROL Nächste]** um fortzufahren.

![vorhandene](../../../../images/tutorials/create/zoho/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre [!DNL Zoho CRM] Anmeldedaten. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbindung mit Quelle herstellen]** und dann etwas Zeit für die Einrichtung der neuen Verbindung.

>[!TIP]
>
>Ihre Konto-URL-Domäne muss mit Ihrem entsprechenden Domänen-Speicherort übereinstimmen. Im Folgenden finden Sie die verschiedenen Domänen und die zugehörigen Konto-URLs:<ul><li>Vereinigte Staaten: https://accounts.zoho.com</li><li>Australien: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>Indien: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

![new](../../../../images/tutorials/create/zoho/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrer [!DNL Zoho CRM] -Konto. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Datenfluss konfigurieren, um Daten in Platform zu importieren](../../dataflow/crm.md).
