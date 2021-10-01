---
title: Erweiterungs-Upgrades
description: Erfahren Sie, wie Erweiterungs-Upgrades im Erweiterungskatalog verpackt und dargestellt werden.
exl-id: 4a7e0c5c-4bd1-4fb8-8509-f88a0aa42ac4
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 100%

---

# Erweiterungs-Upgrades

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Erweiterungsentwickler fügen ihren Erweiterungen kontinuierlich neue Funktionen hinzu und beheben regelmäßig Fehler. Diese Aktualisierungen werden in neuen Versionen der jeweiligen Erweiterung zusammengefasst und im Erweiterungskatalog als Upgrade bereitgestellt.

## Erweiterungskatalog

Wenn ein Erweiterungsentwickler eine neue Version der Erweiterung bereitgestellt hat, wird diese neue Version im Erweiterungskatalog verfügbar. Der Katalog zeigt nur die neueste Version der jeweiligen Erweiterung an. Es ist nicht möglich, eine andere Erweiterungsversion als `latest` zu installieren.

Wenn Sie eine Erweiterung in Ihrer Eigenschaft installieren, wird die derzeit verfügbare Version installiert und die Eigenschaft weist ab diesem Zeitpunkt diese Version auf – auch wenn dem Katalog neuere Versionen hinzugefügt werden.

## Upgrade-Benachrichtigungen

Wenn Sie eine Erweiterung in Ihrer Eigenschaft installiert haben und im Katalog eine neue Version verfügbar ist, wird auf der Seite „Installierte Erweiterungen“ auf der Erweiterungskarte die Schaltfläche [!UICONTROL Upgrade] angezeigt.

Außerdem wird ein Hinweis angezeigt, wenn Sie Ressourcen bearbeiten, die von dieser Erweiterung bereitgestellt werden.

## Upgrades sind dauerhaft

Wenn Sie ein Upgrade auf eine neuere Version im Katalog durchführen möchten, müssen Sie dieses Upgrade selbst installieren. Upgrades sind Änderungen, die einer Bibliothek hinzugefügt, getestet und veröffentlicht werden müssen, bevor sie sich auf die bereitgestellten Tags auswirken.

Upgrades müssen sorgfältig geplant werden. Führen Sie keine Upgrades durch, wenn Sie nicht darauf vorbereitet sind, die neue Erweiterung zu testen und bereitzustellen. Nachdem das Upgrade Ihrer Eigenschaft hinzugefügt wurde, muss es in alle Bibliotheken eingefügt werden. Bei allen Bibliotheken, die nicht die aktualisierte Erweiterung enthalten, schlägt die Erstellung fehl.

Es gibt derzeit keine Möglichkeit, Erweiterungen auf eine frühere Version herabzustufen. Nach dem Upgrade der Erweiterung (egal, ob veröffentlicht oder nicht) wird die neue Erweiterungsversion in Ihrer Eigenschaft gespeichert.

## Upgradeprozess

Das Installieren eines Upgrades ähnelt stark der erstmaligen Installation der Erweiterung.

1. Wählen Sie **[!UICONTROL Upgrade]** aus, um zum Bildschirm [!UICONTROL Erweiterungskonfiguration] zu wechseln.
1. Nehmen Sie die gewünschten Konfigurationsänderungen vor.
1. Wählen Sie **[!UICONTROL Speichern]** aus.

Das Upgrade wird erst durchgeführt, wenn Sie auf **[!UICONTROL Speichern]** klicken. Sie können zu jedem Zeitpunkt vor dem Upgrade auf [!UICONTROL Abbrechen] klicken, um die derzeit installierte Version beizubehalten. Nachdem Sie auf **[!UICONTROL Speichern]** geklickt haben, ist dies nicht mehr möglich.

Erweiterungs-Upgrades sind nicht zulässig, wenn Sie eine Bibliothek im Status `Approved` oder `Submitted` haben. Dies liegt daran, dass der nächste Build die neue Erweiterungsversion enthalten muss. Bei einer Bibliothek im Status `Approved` oder `Submitted` ist der nächste Build der Produktions-Build. Dieser Build würde fehlschlagen, da er nicht die aktuelle Version enthält. Daher muss der Workflow Bibliotheken im Status `Approved` oder `Submitted` veröffentlichen oder ablehnen, _bevor_ die Erweiterung aktualisiert wird.

## Veröffentlichen eines Upgrades

Nach der Installation der aktualisierten Erweiterung auf Ihrer Eigenschaft müssen Sie sie fortan in alle Bibliotheken einfügen. Für alle Bibliotheken, in der sie nicht enthalten ist, wird eine Fehlermeldung angezeigt.

Davon abgesehen ähnelt das Hinzufügen der aktualisierten Erweiterung zu Ihrer Bibliothek dem [Hinzufügen anderer Änderungen](../../publishing/libraries.md) zu einer Bibliothek.

Im Bildschirm [!UICONTROL Bibliothek bearbeiten] können Sie die Schaltfläche [!UICONTROL Alle geänderten Ressourcen hinzufügen] verwenden, oder Sie verwenden die Schaltfläche [!UICONTROL Ressource hinzufügen] und wählen die aktualisierte Erweiterung eigenständig aus.

>[!TIP]
>
>Es ist möglich, dass Erweiterungsentwickler neue Konfigurationselemente zu ihren Erweiterungsansichten hinzufügen, um neue Funktionen zu aktivieren. Wenn Sie nach dem Upgrade auf eine neue Erweiterungsversion einen Buildfehler feststellen, der eindeutig auf diese Erweiterung zurückzuführen ist, öffnen Sie die Konfigurationsseite der Erweiterung und klicken Sie auf „Speichern“ (auch wenn Sie nichts geändert haben). Fügen Sie dann die neue Änderung Ihrer Bibliothek hinzu und versuchen Sie erneut, den Build zu erstellen.

Nachdem Sie Ihrer Bibliothek das Erweiterungs-Upgrade hinzugefügt haben, können Sie sie anhand der im [Publishing-Workflow](../../publishing/publishing-flow.md) beschriebenen Schritte in der Produktion veröffentlichen.
