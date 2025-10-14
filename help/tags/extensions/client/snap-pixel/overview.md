---
title: Snap Pixel Extension - Übersicht
description: Erfahren Sie, wie Sie mit der Tag-Erweiterung „Snap Pixel“ wertvolle Benutzerinteraktionen in Adobe Experience Platform erfassen können.
last-substantial-update: 2025-09-17T00:00:00Z
source-git-commit: d846bd5dee5ce0ee8836dc25e20d9fd070714114
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

---

# [!DNL Snap Pixel] - Übersicht

[[!DNL Snap Pixel]](https://businesshelp.snapchat.com/s/article/snap-pixel-about) ist ein JavaScript-basiertes Analysetool, mit dem Sie wertvolle Benutzerinteraktionen auf Ihrer Website erfassen können. Wichtige Besucheraktionen wie Käufe, Anmeldungen oder andere Konversionen werden automatisch an Ihren [Ads Manager](http://ads.snapchat.com/) gesendet, sodass Sie die Leistung Ihrer Anzeigen, Kampagnen, Konversionspfade und mehr messen und optimieren können.

Mit der [!DNL Snap Pixel] Tag-Erweiterung können Sie [!DNL Snap Pixel] Funktionen direkt in Ihre Client-seitigen Tag-Bibliotheken integrieren. In dieser Dokumentation wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in Ihren Tag-Management-Regeln implementieren.

Die [!DNL Snap Pixel] Tag-Erweiterung optimiert die Integration [!DNL Snap Pixel] Funktionen in Ihre vorhandenen Client-seitigen Tag-Bibliotheken. In dieser Dokumentation wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in Ihrem Tag-Management ([) &#x200B;](../../../ui/managing-resources/rules.md).

## Voraussetzungen {#prerequisites}

Um die Erweiterung verwenden zu können, benötigen Sie ein gültiges [!DNL Snap]-Konto mit Zugriff auf [!DNL Ads Manager]. Sie müssen [einen neuen erstellen [!DNL Snap Pixel]](https://forbusiness.snapchat.com/advertising/snap-pixel#about) und dessen Pixel-ID kopieren, um die Erweiterung für Ihr Konto zu konfigurieren. Wenn Sie über eine vorhandene [!DNL Snap Pixel] verfügen, können Sie einfach deren ID verwenden.

Es wird empfohlen, [!DNL Snap Pixel] zusammen mit dem [!DNL Snap Conversions API] zu verwenden, um dieselben Ereignisse sowohl Client- als auch Server-seitig zu senden. Dieser Ansatz kann dabei helfen, Ereignisse wiederherzustellen, die möglicherweise nicht nur von der [!DNL Snap Pixel] erfasst werden. Unter der [[!DNL Snap] Konversions-API-Erweiterung für die &#x200B;](../../server/snap/overview.md)) finden Sie Anweisungen zur Integration in Ihre Server-seitigen Implementierungen. Beachten Sie, dass Ihre Organisation Zugriff auf [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) haben muss, um die Server-seitige Erweiterung verwenden zu können.

## Installieren der Erweiterung {#install}

Um die [!DNL Snap Pixel]-Erweiterung zu installieren, navigieren Sie zur Datenerfassungs-Benutzeroberfläche oder zur Experience Platform-Benutzeroberfläche und wählen **[!UICONTROL Tags]** in der linken Navigationsleiste aus. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, klicken Sie im linken **[!UICONTROL auf]** Erweiterungen und wählen Sie dann die Registerkarte **[!UICONTROL Katalog]** aus. Suchen Sie nach der Karte [!UICONTROL Snap Pixel] und wählen Sie dann **[!UICONTROL Installieren]** aus.

![Die ausgewählte Schaltfläche [!UICONTROL Installieren] für die Erweiterung [!UICONTROL Snap Pixel] in der Datenerfassungs-Benutzeroberfläche.](./images/install.png)

In der angezeigten Konfigurationsansicht müssen Sie die zuvor kopierte Pixel-ID angeben, um die Erweiterung mit Ihrem Konto zu verknüpfen. Sie können die ID direkt in die Eingabe einfügen oder stattdessen ein vorhandenes Datenelement auswählen.

Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![Die [!DNL Pixel]-ID, die als Datenelement in der Erweiterungskonfigurationsansicht bereitgestellt wird.](./images/configure.png)

Die Erweiterung ist installiert und Sie können jetzt ihre verschiedenen Aktionen in Ihren Tag-Regeln verwenden.

## Konfigurieren einer Tag-Regel {#rule}

[!DNL Snap Pixel] unterstützt eine Reihe vordefinierter Standardereignisse mit jeweils spezifischen Kontexten und akzeptierten Parametern. Die in der [!DNL Snap Pixel]-Erweiterung verfügbaren Regelaktionen werden diesen Ereignistypen zugeordnet, sodass Ereignisse, die an [!DNL Snap] gesendet werden, einfach anhand ihres Typs kategorisiert und konfiguriert werden können.

Zu Demonstrationszwecken wird in diesem Abschnitt gezeigt, wie Sie eine Regel erstellen, die Kaufereignisse an [!DNL Snap] sendet.

Erstellen Sie zunächst eine neue Tag-Regel und definieren Sie die Bedingungen nach Bedarf. Wählen Sie beim Einrichten der Regelaktionen [!DNL Snap Pixel] als Erweiterung und wählen Sie dann **[!UICONTROL Kaufereignis senden]** als Aktionstyp aus.

Nachdem Sie die Konfiguration der Aktion [!UICONTROL Kaufereignis senden] abgeschlossen haben, wählen Sie **[!UICONTROL Änderungen beibehalten]** aus, um sie Ihrer Regeleinrichtung hinzuzufügen.

![Der [!UICONTROL Kaufereignis senden] Aktionstyp, der für eine Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt wurde.](./images/action-type.png)

Wenn Sie mit der allgemeinen Regelkonfiguration zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]**.

Um Ihre Aktualisierungen anzuwenden, veröffentlichen Sie ein neues Tag [build](../../../ui/publishing/builds.md), um die Änderungen an der Bibliothek zu aktivieren.

## Vergewissern Sie sich, dass [!DNL Snap] Daten erhält {#confirm}

Nachdem Ihr aktualisierter Build auf Ihrer Website bereitgestellt wurde, können Sie überprüfen, ob die Daten wie erwartet gesendet werden, indem Sie Konversionsereignisse in Ihrem Browser auslösen und überprüfen, ob sie in [[!DNL Snap Events Manager]](https://businesshelp.snapchat.com/s/article/events-manager) angezeigt werden.

## Nächste Schritte {#next-steps}

In diesem Handbuch wird beschrieben, wie Sie Daten mithilfe der [!DNL Snap]-Tag-Erweiterung an [!DNL Snap Pixel] senden. Wenn Sie auch serverseitige Ereignisse an [!DNL Snap] senden möchten, können Sie mit der Installation und Konfiguration der [[!DNL Snap Conversions API event forwarding extension]](../../server/snap/overview.md) fortfahren.
