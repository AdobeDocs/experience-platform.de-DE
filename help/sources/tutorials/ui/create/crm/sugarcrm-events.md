---
title: Erstellen einer Quellverbindung zu SugarCRM Events in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung mit SugarCRM-Ereignissen erstellen.
exl-id: db346ec0-2c57-4b82-8a39-f15d4cd377d4
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 45%

---

# (Beta) Erstellen Sie eine [!DNL SugarCRM Events] Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL SugarCRM Events]-Quelle befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL SugarCRM Events] Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL SugarCRM]-Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/crm.md) fortfahren.

### Sammeln erforderlicher Anmeldeinformationen

Um eine Verbindung zwischen [!DNL SugarCRM Events] und Platform herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| `Host` | Der SugarCRM-API-Endpunkt, mit dem die Quelle eine Verbindung herstellt. | `developer.salesfusion.com` |
| `Username` | Ihr Benutzername für das SugarCRM-Entwicklerkonto. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | Ihr SugarCRM-Entwicklerkontokennwort. | `123456789` |

### Erstellen eines Platform-Schemas für [!DNL SugarCRM]

Vor der Erstellung [!DNL SugarCRM] -Quellverbindung erstellen, müssen Sie außerdem sicherstellen, dass Sie zunächst ein Platform-Schema erstellen, das für Ihre Quelle verwendet werden soll. Siehe Tutorial zu [Erstellen eines Platform-Schemas](../../../../../xdm/schema/composition.md) für umfassende Schritte zum Erstellen eines Schemas.

![Screenshot der Platform-Benutzeroberfläche mit einem Beispielschema für SugarCRM-Ereignisse](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>Stellen Sie bei der Zuordnung des Schemas sicher, dass Sie auch die obligatorische `event_id` und `timestamp` für Platform erforderliche Felder.

## Verbinden Ihres [!DNL SugarCRM Events]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem *CRM* category, select **[!UICONTROL SugarCRM-Ereignisse]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Screenshot der Platform-Benutzeroberfläche für den Katalog mit der SugarCRM Events-Karte](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

Die **[!UICONTROL Connect SugarCRM Events-Konto]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL SugarCRM Events]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Screenshot der Platform-Benutzeroberfläche für das Connect SugarCRM Events-Konto mit einem vorhandenen Konto](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre -Anmeldedaten an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Screenshot der Platform-Benutzeroberfläche für das Connect SugarCRM Events-Konto mit einem neuen Konto](../../../../images/tutorials/create/sugarcrm-events/new.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL SugarCRM Events]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen [Datenfluss konfigurieren, um Daten in Platform zu importieren](../../dataflow/crm.md).

## Zusätzliche Ressourcen

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei der Verwendung der [!DNL SugarCRM] -Quelle.

### Leitplanken {#guardrails}

Die [!DNL SugarCRM] Die API-Drosselraten betragen 90 Aufrufe pro Minute oder 2000 Aufrufe pro Tag, je nachdem, was zuerst eintritt. Diese Einschränkung wurde jedoch umgangen, indem ein Parameter in die Verbindungsspezifikation eingefügt wurde, der die Anfragezeit verzögert, sodass die Ratenbegrenzung nie erreicht wird.

### Validierung {#validation}

Überprüfen, ob Sie die Quelle richtig eingerichtet haben und [!DNL SugarCRM Events] Daten werden erfasst, führen Sie die folgenden Schritte aus:

* Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Datenflüsse anzeigen]** neben dem [!DNL SugarCRM Events] Kartenmenü im Quellkatalog. Wählen Sie als Nächstes **[!UICONTROL Vorschau des Datensatzes anzeigen]** , um die erfassten Daten zu überprüfen.

* Je nach dem Objekttyp, mit dem Sie arbeiten, können Sie die aggregierten Daten anhand der in der Variablen [!DNL SugarMarket] Ereignisseite unten:

![Screenshot auf der Seite Zuckermarktkonten mit einer Liste von Konten](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>Die [!DNL SugarMarket] -Seiten enthalten nicht die Anzahl der gelöschten Objekte. Daten, die über diese Quelle abgerufen werden, enthalten jedoch auch die gelöschte Anzahl. Diese würden mit einer gelöschten Markierung markiert.
