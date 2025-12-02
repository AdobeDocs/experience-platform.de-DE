---
title: Regelsätze auswerten
description: Manueller Trigger einer Regelsatzauswertung.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---

# Regelsätze auswerten

Mit dem Aktionstyp **[!UICONTROL Evaluate rulesets]** können Sie Trigger für Regelsatzauswertungen manuell durchführen. Regelsätze werden von Adobe Journey Optimizer zurückgegeben, um Funktionen wie In-Browser-Nachrichten zu unterstützen.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Rules]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Actions] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das Dropdown-Feld [!UICONTROL Extension] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und dann den [!UICONTROL Action type] auf **[!UICONTROL Evaluate rulesets]** fest.

![Abbildung der Experience Platform-Benutzeroberfläche mit dem Aktionstyp „Regelsätze auswerten“.](../assets/evaluate-rulesets.png)

## Verfügbare Felder

Dieser Aktionstyp unterstützt die folgenden Optionen:

* **[!UICONTROL Render visual personalization decisions]**: Ein Kontrollkästchen, das nach der Aktivierung visuelle Personalisierungsentscheidungen für die übereinstimmenden Regelsatzelemente rendert.
* **[!UICONTROL Decision context]**: Eine Schlüssel-Wert-Zuordnung, die bei der Auswertung von Adobe Journey Optimizer-Regelsätzen für die geräteinterne Entscheidungsfindung verwendet wird. Sie können den Entscheidungskontext manuell oder über ein Datenelement bereitstellen.
