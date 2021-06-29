---
keywords: Experience Platform; Startseite; beliebte Themen; Veva CRM; VEC
solution: Experience Platform
title: Erstellen einer VEC CRM-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung mit dem VEE CRM erstellen.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 076e0880c9efd1fe1cbfb4c610c5e15093adf460
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 13%

---

# Erstellen einer [!DNL Veeva CRM]-Quellverbindung in der Benutzeroberfläche

Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, externe CRM-Daten planmäßig zu erfassen. Dieses Tutorial enthält Schritte zum Erstellen eines Quell-Connectors [!DNL Veeva CRM] mithilfe der [!DNL Platform]-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) zum Schema Editor: Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL Veeva CRM]-Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses [fortfahren.](../../dataflow/crm.md)

### Erforderliche Anmeldedaten sammeln

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `environmentUrl` | Die URL der Quellinstanz [!DNL Veeva CRM]. |
| `username` | Der Benutzername für das [!DNL Veeva CRM]-Benutzerkonto. |
| `password` | Das Kennwort für das [!DNL Veeva CRM]-Benutzerkonto. |
| `securityToken` | Das Sicherheits-Token für das [!DNL Veeva CRM]-Benutzerkonto. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Veeva CRM-Dokument]

## Ihr [!DNL Veeva CRM]-Konto verbinden

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Veeva CRM]-Konto mit [!DNL Platform] zu verknüpfen.

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Quellen]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Vielzahl von Quellen, für die Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL CRM] die Option **[!UICONTROL Veeva CRM]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/veeva/catalog.png)

Die Seite **[!UICONTROL Connect Veeva CRM-Konto]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Veeva CRM]-Konto aus, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhandene](../../../../images/tutorials/create/veeva/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre [!DNL Veeva CRM]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** aus und lassen Sie dann etwas Zeit für die Einrichtung der neuen Verbindung zu.

![new](../../../../images/tutorials/create/veeva/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Veeva CRM]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in Platform](../../dataflow/crm.md) zu importieren.
