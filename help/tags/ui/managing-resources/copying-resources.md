---
title: Kopieren von Ressourcen
description: Erfahren Sie, wie Sie mit den Einstellungen einer vorhandenen Tag-Ressource in Adobe Experience Platform eine neue Tag-Ressource erstellen.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 86%

---

# Kopieren von Ressourcen

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Manchmal ist es praktisch, eine neue Ressource mithilfe der Einstellungen einer vorhandenen Ressource zu erstellen. In diesen Fällen können Sie eine Kopie erstellen.

Eigenschaften, Erweiterungen, Regeln und Datenelemente können kopiert werden.

Das Kopieren einer Ressource erstellt ein Duplikat dieser Ressource im angegebenen Ziel. Dies ist eine einmalige Aktion. Es besteht keine dauerhafte Beziehung zwischen der ursprünglichen Ressource und den vorhandenen Kopien.

## Kopieren einer Erweiterung

Sie können eine Erweiterung kopieren, indem Sie Ihre installierten Erweiterungen anzeigen, auf den Dropdown-Pfeil auf der Schaltfläche **[!UICONTROL Konfigurieren]** klicken und **[!UICONTROL Kopieren]** auswählen.

![Kopieren der Analytics-Erweiterung](../../images/copy-initiate-extension.png)

Wählen Sie für Eigenschaften, Regeln und Datenelemente einfach die zu kopierende Ressource aus und klicken Sie dann im Menü „Aktionen“ auf **[!UICONTROL Kopieren]**.

![Kopieren der Analytics-Regel](../../images/copy-initiate-rule.png)

Wenn Sie eine Regel oder ein Datenelement kopieren, können Sie im Dialogfeld „Kopieren“ über das Dropdownmenü eine Ziel-Property auswählen, in die Sie kopieren möchten (Standardeinstellung ist die aktuelle Eigenschaft). Erweiterungen können nicht in dieselbe Property kopiert werden. Daher bieten sie diese Option nicht.

>[!NOTE]
>
>In der Datenerfassungs-Benutzeroberfläche ist es nicht möglich, Ressourcen in eine andere Property zu kopieren, wenn eine Property für die Erweiterungsentwicklung konfiguriert ist und die andere Property nicht.

Nachdem Sie das gewünschte Verhalten konfiguriert haben, klicken Sie auf **[!UICONTROL Kopieren]**.

## Kopieren von Propertys

Wenn Sie eine Kopie einer vollständigen Property erstellen, sollten Sie einige Dinge über den Prozess wissen.

* Die Property-Einstellungen werden genau so kopiert, wie sie sind (Domänen, erweiterte Einstellungen usw.).
* Regeln, Datenelemente und Erweiterungen aus der Ursprungs-Property werden in die neue Ziel-Property kopiert. Adapter, Umgebungen und Bibliotheken werden nicht kopiert.
* Erforderliche Erweiterungen (Erweiterungen, die für vorhandene Datenelemente oder Regelkomponenten benötigt werden) werden auch dann in die Ziel-Property kopiert, wenn sie in der Ursprungs-Property deinstalliert wurden.
* Das Kopieren einer Property kann eine Weile dauern. Dieser Vorgang läuft im Hintergrund ab. Sie können den Fortschritt des Kopiervorgangs überwachen oder währenddessen andere Aufgaben erledigen.
* Wenn Sie eine einzelne Ressource ändern, nachdem sie bereits in die Ziel-Property kopiert wurde (jedoch bevor die Kopie abgeschlossen wurde), werden die neuen Änderungen nicht kopiert.

## Kopieren von Erweiterungen

Wenn Sie eine Erweiterung in eine andere Property kopieren, müssen Sie Folgendes beachten.

* Wenn die Erweiterung nicht in der Ziel-Property installiert ist, wird sie mit denselben Einstellungen wie die Ursprungs-Property installiert.
* Wenn die Ziel-Property bereits installiert ist, werden nur die Einstellungen kopiert.
* Wenn die Ziel-Property eine niedrigere Version der installierten Erweiterung aufweist, erhalten Sie einen Hinweis, dass Sie die Erweiterung in der Ziel-Property aktualisieren müssen, bevor Sie die Kopie durchführen können. Erweiterungsentwickler können ihren Erweiterungen im Laufe der Zeit Einstellungen hinzufügen. Daher können Einstellungen aus einer neueren Erweiterung nicht zuverlässig auf ältere Versionen angewendet werden.
* Wenn die Ziel-Property eine höhere Version der installierten Erweiterung aufweist, werden die Einstellungen kopiert, es wird aber kein Downgrade durchgeführt. Die Ziel-Property behält weiterhin die aktuelle Versionsnummer bei.

## Kopieren von Regeln und Datenelementen

Alle Regeln und Datenelemente werden von einer Erweiterung bereitgestellt. Wenn Sie also Eigenschaften-übergreifend kopieren, muss Platform diese zugrunde liegenden Erweiterungen berücksichtigen.

![Kopieren einer Regel in meine Demo-Property](../../images/copy-rules-dialog1.png)

Das Dialogfeld &quot;Kopieren&quot;enthält eine Erläuterung dessen, was genau vor dem Kopieren ausgeführt wird. Das Dialogfeld oben ist für eine Regel vorgesehen. Dasselbe gilt jedoch für Datenelemente.

1. **Die für diese Regeln erforderlichen Erweiterungen werden kopiert.** Auf diese Weise wissen Sie, dass die erforderlichen Erweiterungen mit der Regel übereinstimmen. Diese Kopien folgen denselben Regeln wie die oben beschriebene normale Erweiterungskopie.
1. **Die Erweiterungseinstellungen werden NICHT kopiert, wenn die Erweiterung bereits installiert ist.** Wenn die erforderlichen Erweiterungen bereits in der Ziel-Property vorhanden sind, bleibt die Erweiterung unverändert. Wenn Sie die Erweiterungseinstellungen ebenfalls kopieren möchten, können Sie die Schaltfläche **Erweiterungseinstellungen in Ziel-Property ersetzen** verwenden. Die Erklärung wird daraufhin entsprechend aktualisiert.
1. **Datenelemente, die für diese Regeln erforderlich sind, werden NICHT kopiert.** Diese Erklärung gilt nur für Regeln. Regeln sind häufig auf Datenelemente angewiesen, um ordnungsgemäß zu funktionieren. Wenn Sie eine Regel in eine neue Eigenschaft kopieren, müssen Sie im Rahmen einer separaten Aktion auch die erforderlichen Datenelemente kopieren.
