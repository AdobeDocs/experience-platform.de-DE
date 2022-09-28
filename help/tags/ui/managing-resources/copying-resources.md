---
title: Kopieren von Ressourcen
description: Erfahren Sie, wie Sie in Adobe Experience Platform eine neue Tag-Ressource mit den Einstellungen einer schon vorhandenen Tag-Ressource erstellen.
exl-id: 7e52ceae-97df-4c64-aba3-4f5ba6018a47
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 96%

---

# Kopieren von Ressourcen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Manchmal ist es praktisch, eine neue Ressource mithilfe der Einstellungen einer vorhandenen Ressource zu erstellen. In diesen Fällen können Sie eine Kopie erstellen.

Eigenschaften, Erweiterungen, Regeln und Datenelemente können kopiert werden.

Das Kopieren einer Ressource erstellt ein Duplikat dieser Ressource im angegebenen Ziel. Dies ist eine einmalige Aktion. Es besteht keine dauerhafte Beziehung zwischen der ursprünglichen Ressource und den vorhandenen Kopien.

## Kopieren einer Erweiterung

Sie können eine Erweiterung kopieren, indem Sie Ihre installierten Erweiterungen anzeigen, auf den Dropdown-Pfeil auf der Schaltfläche **[!UICONTROL Konfigurieren]** klicken und **[!UICONTROL Kopieren]** auswählen.

![Kopieren der Analytics-Erweiterung](../../images/copy-initiate-extension.png)

Wählen Sie für Eigenschaften, Regeln und Datenelemente einfach die zu kopierende Ressource aus und klicken Sie dann im Menü „Aktionen“ auf **[!UICONTROL Kopieren]**.

![Kopieren der Analytics-Regel](../../images/copy-initiate-rule.png)

Wenn Sie eine Regel oder ein Datenelement kopieren, können Sie im Dialogfeld „Kopieren“ über das Dropdown-Menü eine Ziel-Eigenschaft auswählen, in die Sie kopieren möchten (Standardeinstellung ist die aktuelle Eigenschaft). Erweiterungen können nicht in dieselbe Eigenschaft kopiert werden. Daher bieten sie diese Option nicht.

>[!NOTE]
>
>Es ist nicht möglich, Ressourcen in eine andere Eigenschaft zu kopieren, wenn eine Eigenschaft für die Erweiterungsentwicklung konfiguriert ist und die andere Eigenschaft nicht.

Nachdem Sie das gewünschte Verhalten konfiguriert haben, klicken Sie auf **[!UICONTROL Kopieren]**.

## Kopieren von Eigenschaften

Wenn Sie eine Kopie einer vollständigen Eigenschaft erstellen, sollten Sie einige Dinge über den Prozess wissen.

* Die Eigenschaften-Einstellungen werden genau so kopiert, wie sie sind (Domains, erweiterte Einstellungen usw.).
* Regeln, Datenelemente und Erweiterungen aus der Ursprungs-Eigenschaft werden in die neue Ziel-Eigenschaft kopiert. Adapter, Umgebungen und Bibliotheken werden nicht kopiert.
* Erforderliche Erweiterungen (Erweiterungen, die für vorhandene Datenelemente oder Regelkomponenten benötigt werden) werden auch dann in die Ziel-Eigenschaft kopiert, wenn sie in der Ursprungs-Eigenschaft deinstalliert wurden.
* Das Kopieren einer Eigenschaft kann eine Weile dauern. Dieser Vorgang läuft im Hintergrund ab. Sie können den Fortschritt des Kopiervorgangs überwachen oder währenddessen andere Aufgaben erledigen.
* Wenn Sie eine einzelne Ressource ändern, nachdem sie bereits in die Ziel-Eigenschaft kopiert wurde (jedoch bevor die Kopie abgeschlossen wurde), werden die neuen Änderungen nicht kopiert.

## Kopieren von Erweiterungen

Wenn Sie eine Erweiterung in eine andere Eigenschaft kopieren, müssen Sie Folgendes beachten.

* Wenn die Erweiterung nicht in der Ziel-Eigenschaft installiert ist, wird sie mit denselben Einstellungen wie die Ursprungs-Eigenschaft installiert.
* Wenn die Ziel-Eigenschaft bereits installiert ist, werden nur die Einstellungen kopiert.
* Wenn die Ziel-Eigenschaft eine niedrigere Version der installierten Erweiterung aufweist, erhalten Sie einen Hinweis, dass Sie die Erweiterung in der Ziel-Eigenschaft aktualisieren müssen, bevor Sie die Kopie durchführen können. Erweiterungsentwickler können ihren Erweiterungen im Laufe der Zeit Einstellungen hinzufügen. Daher können Einstellungen aus einer neueren Erweiterung nicht zuverlässig auf ältere Versionen angewendet werden.
* Wenn die Ziel-Eigenschaft eine höhere Version der installierten Erweiterung aufweist, werden die Einstellungen kopiert, es wird aber kein Downgrade durchgeführt. Die Ziel-Eigenschaft behält weiterhin die aktuelle Versionsnummer bei.

## Kopieren von Regeln und Datenelementen

Alle Regeln und Datenelemente werden von einer Erweiterung bereitgestellt. Wenn Sie also Eigenschaften-übergreifend kopieren, muss die Platform zugrunde liegende Erweiterungen berücksichtigen.

![Kopieren einer Regel in meine Demo-Property](../../images/copy-rules-dialog1.png)

Das Dialogfeld „Kopieren“ enthält eine Erläuterung dessen, was genau vor dem Kopieren ausgeführt wird. Das Dialogfeld oben ist für eine Regel vorgesehen. Dasselbe gilt jedoch für Datenelemente.

1. **Die für diese Regeln erforderlichen Erweiterungen werden kopiert.** Auf diese Weise wissen Sie, dass die erforderlichen Erweiterungen mit der Regel übereinstimmen. Diese Kopien folgen denselben Regeln wie die oben beschriebene normale Erweiterungskopie.
1. **Die Erweiterungseinstellungen werden NICHT kopiert, wenn die Erweiterung bereits installiert ist.** Wenn die erforderlichen Erweiterungen bereits in der Ziel-Eigenschaft vorhanden sind, bleibt die Erweiterung unverändert. Wenn Sie die Erweiterungseinstellungen ebenfalls kopieren möchten, können Sie die Schaltfläche **Erweiterungseinstellungen in Ziel-Eigenschaft ersetzen** verwenden. Die Erklärung wird daraufhin entsprechend aktualisiert.
1. **Datenelemente, die für diese Regeln erforderlich sind, werden NICHT kopiert.** Diese Erklärung gilt nur für Regeln. Regeln sind häufig auf Datenelemente angewiesen, um ordnungsgemäß zu funktionieren. Wenn Sie eine Regel in eine neue Eigenschaft kopieren, müssen Sie im Rahmen einer separaten Aktion auch die erforderlichen Datenelemente kopieren.
