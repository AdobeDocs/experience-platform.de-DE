---
title: Übersicht über Kapillarstreaming-Ereignisse
description: Erfahren Sie, wie Sie Daten von Capillary zu Experience Platform streamen.
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: 428aed259343f56a2bf493b40ff2388340fffb7b
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 2%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>Die [!DNL Capillary Streaming Events]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie &#x200B;](../../home.md#terms-and-conditions) den „Nutzungsbedingungen“ in der Quellenübersicht .

[!DNL Capillary Technologies] ist eine führende Treue- und Interaktionsplattform, der über 300 Marken auf der ganzen Welt vertrauen. Verwenden Sie die [!DNL Capillary Streaming Events], damit Ihr Unternehmen Kundenprofile, Treuedaten und Transaktionsereignisse nahtlos von [!DNL Capillary] in Adobe Experience Platform streamen kann. Verbinden Sie Ihre [!DNL Capillary], um Personalisierung in Echtzeit, erweiterte Zielgruppensegmentierung und Omni-Channel-Kampagnenorchestrierung zu ermöglichen.

Durch die Integration von [!DNL Capillary] mit Experience Platform können Sie:

* Synchronisieren **Treuepunkte, -stufen und -belohnungen** in Echtzeit
* Senden Sie **Transaktionsdaten** zur Analyse und Aktivierung an Experience Platform.
* Nutzen Sie Real-Time CDP, Experience Platform und Adobe Journey Optimizer für die Segmentierung, Journey-Orchestrierung und Personalisierung.

## Voraussetzungen

Bevor Sie [!DNL Capillary] mit Adobe Experience Platform verbinden, stellen Sie Folgendes sicher:

* Eine gültige **Adobe-Organisations-** und Zugriff auf eine aktivierte Experience Platform-Sandbox.
* Sie müssen sowohl **[!UICONTROL Quellen anzeigen]** als auch **[!UICONTROL Quellen verwalten]** für Ihr Konto aktiviert haben, um Ihr [!DNL Capillary]-Konto mit Experience Platform zu verbinden. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche der Zugriffssteuerung](../../../access-control/ui/overview.md).

### Erstellen eines Schemas

Sie müssen ein Experience-Datenmodell (XDM)-Schema erstellen, um einen Datensatz zu beschreiben, in dem die möglichen Felder und Datentypen gespeichert werden können, die von [!DNL Capillary] gesendet werden.

1. Melden Sie sich bei Adobe Experience Platform an und greifen Sie über die Anmeldung Ihres Unternehmens auf die Experience Platform zu.
2. Wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Schemata]** aus, um den Arbeitsbereich [!UICONTROL Schemata] zu öffnen.
3. Wählen **[!UICONTROL oben]** rechts Schema erstellen aus.
4. Wählen Sie im Dialogfeld „Schema erstellen“ zwischen **[!UICONTROL Manuelle Erstellung]** (Felder und Feldergruppen selbst hinzufügen) oder **[!UICONTROL ML-unterstützte Erstellung]** (CSV-Datei hochladen und maschinelles Lernen verwenden, um ein empfohlenes Schema zu generieren).
5. Wählen Sie eine Basisklasse für Ihr Schema aus (z. B. Einzelnes XDM-Profil, XDM ExperienceEvent oder Sonstiges). Wenn Sie **[!UICONTROL Sonstige]** auswählen, können Sie aus verfügbaren benutzerdefinierten oder Standardklassen auswählen.
6. Geben Sie einen benutzerfreundlichen Namen und eine Beschreibung für Ihr Schema ein.
7. Verwenden Sie den Schema-Editor, um: Feldergruppen (wiederverwendbare Blöcke von Feldern) hinzuzufügen, einzelne Felder zu definieren (Namen, Datentypen und Optionen anzupassen) und optional benutzerdefinierte Datentypen oder Feldergruppen zu erstellen, wenn die vorhandenen nicht Ihren Anforderungen entsprechen.
8. Überprüfen Sie die Schemastruktur auf der Arbeitsfläche. Wählen Sie **[!UICONTROL Beenden]** aus, um das Schema zu erstellen.
9. (Optional) Bearbeiten Sie Felder, fügen Sie Beschreibungen hinzu und passen Sie die Feldergruppen im Schema-Editor nach Bedarf an.

Detaillierte Anweisungen zum Erstellen eines XDM-Schemas finden Sie im Handbuch unter [Erstellen eines Schemas mithilfe des Schema-Editors](../../../xdm/tutorials/create-schema-ui.md).

### Erstellen eines Datensatzes

Als Nächstes müssen Sie einen Datensatz erstellen, der auf das soeben erstellte Schema verweist.

1. Wählen Sie in der Experience Platform-Benutzeroberfläche [!UICONTROL Datensätze] im linken Navigationsbereich aus, um den Arbeitsbereich [!UICONTROL Datensätze] zu öffnen.
2. Wählen **[!UICONTROL oben]** „Datensatz erstellen“ aus.
3. Wählen Sie in den Erstellungsoptionen **[!UICONTROL Datensatz aus Schema erstellen]** aus.
4. Suchen Sie in der Liste nach dem zuvor erstellten XDM-Schema und wählen Sie es aus. Nachdem Sie Ihr Schema gefunden haben, klicken Sie auf **[!UICONTROL Weiter]**.
5. Geben Sie einen eindeutigen, beschreibenden Namen für Ihren Datensatz ein.
6. Fügen Sie optional eine Beschreibung hinzu, die künftigen Benutzenden hilft, den Datensatz zu identifizieren.
7. Wählen Sie **[!UICONTROL Beenden]** aus, um den Datensatz zu erstellen.

Detaillierte Anweisungen zum Erstellen eines Datensatzes finden Sie im [Handbuch zur Datensatzbenutzeroberfläche](../../../catalog/datasets/user-guide.md).

## Verbinden von [!DNL Capillary Streaming Events] mit Experience Platform

Nachdem Sie die erforderliche Einrichtung für [!DNL Capillary] abgeschlossen haben, lesen Sie das [[!DNL Capillary Streaming Events] UI-Tutorial](../../tutorials/ui/create/loyalty/capillary.md), um zu erfahren, wie Sie Ihr -Konto verbinden und Daten von [!DNL Capillary] an Experience Platform streamen können.
