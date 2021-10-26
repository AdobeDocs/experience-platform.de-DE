---
keywords: Experience Platform;home;beliebte Themen;Zoho CRM;zoho crm;Zoho;Zoho
solution: Experience Platform
title: Erstellen einer Zoho CRM-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine Zoho CRM-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
source-git-commit: 7a15090d8ed2c1016d7dc4d7d3d0656640c4785c
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 11%

---

# Erstellen Sie eine [!DNL Zoho CRM] Quellverbindung in der Benutzeroberfläche

Quellschnittstellen in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte CRM-Daten planmäßig zu erfassen. In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Zoho CRM] Quellanschluss mit [!DNL Platform] Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Der standardisierte Rahmen, nach dem [!DNL Experience Platform] organisiert Kundenerlebnisdaten.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Tutorial](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Zoho CRM] , können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial fortfahren auf [Konfigurieren eines Datenflusses](../../dataflow/crm.md).

### Erforderliche Anmeldedaten sammeln

Zur Verbindung [!DNL Zoho CRM] auf Platform setzen, müssen Sie Werte für die folgenden Verbindungseigenschaften bereitstellen:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Endpunkt | Der Endpunkt des [!DNL Zoho CRM] Server, an den Sie Ihre Anforderung senden. |
| Konto-URL | Die Konto-URL wird verwendet, um Ihren Zugriff zu generieren und Token zu aktualisieren. Die URL muss domänenspezifisch sein. |
| Client-ID | Die Client-ID, die Ihrer [!DNL Zoho CRM] Benutzerkonto. |
| Client Secret (Client-Geheimnis) | Das Client-Geheimnis, das Ihrem [!DNL Zoho CRM] Benutzerkonto. |
| Zugriffstoken | Das Zugriffstoken autorisiert Ihren sicheren und temporären Zugriff auf Ihre [!DNL Zoho CRM] Konto. |
| Token aktualisieren | Ein Aktualisierungstoken ist ein Token, das verwendet wird, um ein neues Zugriffstoken zu generieren, sobald Ihr Zugriffstoken abgelaufen ist. |

Weitere Informationen zu diesen Anmeldedaten finden Sie in der Dokumentation zu [[!DNL Zoho CRM] Authentifizierung](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Verbinden Sie [!DNL Zoho CRM] Konto

Nachdem Sie die erforderlichen Anmeldedaten erhalten haben, können Sie die folgenden Schritte ausführen, um Ihre [!DNL Zoho CRM] Konto für [!DNL Platform].

Wählen Sie in der Plattform-Benutzeroberfläche **[!UICONTROL Quellen]** von der linken Navigationsleiste aus, um auf [!UICONTROL Quellen] Arbeitsbereich. Die [!UICONTROL Katalog] zeigt eine Reihe von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie aus dem Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die spezifische Quelle finden, mit der Sie arbeiten möchten, indem Sie die Suchoption verwenden.

Im Rahmen der [!UICONTROL CRM] Kategorie, auswählen **[!UICONTROL Zoho CRM]**, und wählen Sie dann **[!UICONTROL Daten Hinzufügen]**.

![Katalog](../../../../images/tutorials/create/zoho/catalog.png)

Die **[!UICONTROL Connect Zoo CRM-Konto]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie [!DNL Zoho CRM] Konto, mit dem Sie einen neuen Datenpfad erstellen möchten, wählen Sie **[!UICONTROL Weiter]** um fortzufahren.

![vorhanden](../../../../images/tutorials/create/zoho/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie einen Namen, eine optionale Beschreibung und Ihre [!DNL Zoho CRM] Anmeldedaten. Wählen Sie nach Beendigung **[!UICONTROL Mit Quelle verbinden]** und dann etwas Zeit für die Einrichtung der neuen Verbindung.

>[!TIP]
>
>Die URL-Domäne Ihrer Konten muss Ihrem entsprechenden Domänenstandort entsprechen. Die folgenden Domänen und die zugehörigen Konto-URLs sind angegeben:<ul><li>Vereinigte Staaten: https://accounts.zoho.com</li><li>Australien: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>Indien: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

![new](../../../../images/tutorials/create/zoho/new.png)

## Nächste Schritte

Durch Befolgen dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Zoho CRM] Konto. Sie können nun mit dem nächsten Tutorial fortfahren und [einen Datenpfad konfigurieren, um Daten in die Plattform zu bringen](../../dataflow/crm.md).
