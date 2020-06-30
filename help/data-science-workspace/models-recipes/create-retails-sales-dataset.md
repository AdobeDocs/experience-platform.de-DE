---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Schema und Dataset für den Einzelhandel erstellen
topic: Tutorial
translation-type: tm+mt
source-git-commit: 4b0f0dda97f044590f55eaf75a220f631f3313ee
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Schema und Dataset für den Einzelhandel erstellen

Dieses Tutorial bietet Ihnen die Voraussetzungen und Elemente, die für alle anderen [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] Tutorials erforderlich sind. Nach Fertigstellung stehen Ihnen und Ihren Mitarbeitern das Retail Sales Schema und die Datensätze zur Verfügung [!DNL Experience Platform].

## Erste Schritte

Bevor Sie dieses Lernprogramm starten, müssen Sie über die folgenden Voraussetzungen verfügen:
- Zugriff auf [!DNL Adobe Experience Platform]. Wenn Sie keinen Zugriff auf eine IMS-Organisation in haben, wenden Sie sich an Ihren Systemadministrator, [!DNL Experience Platform]bevor Sie fortfahren.
- Autorisierung zum Durchführen von [!DNL Experience Platform] API-Aufrufen. Führen Sie das Lernprogramm [zum Authentifizieren und Zugreifen auf Adobe Experience Platformen-APIs](../../tutorials/authentication.md) durch, um die folgenden Werte abzurufen, damit dieses Lernprogramm erfolgreich abgeschlossen werden kann:
   - Genehmigung: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Kundengeheimnis: `{CLIENT_SECRET}`
   - Client-Zertifikat: `{PRIVATE_KEY}`
- Beispieldaten und Quelldateien für das [Einzelhandelsverkaufsrezept](../pre-built-recipes/retail-sales.md). Laden Sie die für diese und andere [!DNL Data Science Workspace] Übungen erforderlichen Elemente aus dem öffentlichen [Adobe-Git-Repository](https://github.com/adobe/experience-platform-dsw-reference/)herunter.
- [Python >= 2.7](https://www.python.org/downloads/) und die folgenden [!DNL Python] Pakete:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Ein funktionierendes Verständnis der folgenden in diesem Lernprogramm verwendeten Konzepte:
   - [!DNL Experience Data Model (XDM)](../../xdm/home.md)
   - [Grundlagen der Schema-Komposition](../../xdm/schema/field-dictionary.md)

## Schema und Dataset für den Einzelhandel erstellen

Das Retail Sales-Schema und die Datensätze werden automatisch mithilfe des bereitgestellten Bootstrap-Skripts erstellt. Gehen Sie wie folgt vor, um die Reihenfolge zu ändern:

### Dateien konfigurieren

1. Navigieren Sie im [!DNL Experience Platform] Tutorial-Ressourcenpaket zum Ordner `bootstrap`und öffnen Sie es mit einem entsprechenden Texteditor `config.yaml` .
2. Geben Sie unter dem `Enterprise` Abschnitt die folgenden Werte ein:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Bearbeiten Sie die Werte unter dem `Platform` Abschnitt, Beispiel unten:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` : Der Basispfad für API-Aufrufe. Ändern Sie diesen Wert nicht.
   - `ims_token` : Du `{ACCESS_TOKEN}` gehst hierher.
   - `ingest_data` : Legen Sie für diese Übung den Wert `"True"` fest, um die Schema und Datensätze für den Einzelhandel zu erstellen. Der Wert `"False"` &quot;von&quot;erstellt nur die Schema.
   - `build_recipe_artifacts` : Legen Sie für die Zwecke dieses Lernprogramms diesen Wert so fest, dass das Skript kein Rezept-Artefakt generieren `"False"` kann.
   - `kernel_type` : Der Ausführungstyp des Recipe-Artefakts. Lassen Sie diesen Wert unverändert, `Python` wenn er als `build_recipe_artifacts` Ausführungsart festgelegt `"False"`ist.

4. Geben Sie unter dem `Titles` Abschnitt die folgenden Informationen entsprechend für die Musterdaten für den Einzelhandel ein, speichern und schließen Sie die Datei, nachdem die Änderungen vorgenommen wurden. Beispiel:

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### Bootstrap-Skript ausführen

1. Öffnen Sie die Terminalanwendung und navigieren Sie zum Ordner für [!DNL Experience Platform] Übungsressourcen.
2. Legen Sie den `bootstrap` Ordner als aktuellen Arbeitspfad fest und führen Sie das `bootstrap.py` [!DNL Python] Skript durch Eingabe des folgenden Befehls aus:

   ```bash
   python bootstrap.py
   ```

   > [!NOTE] Das Skript kann mehrere Minuten dauern.

## Nächste Schritte

Nach erfolgreichem Abschluss des Bootstrap-Skripts können die Retail Sales-Eingabe- und -Ausgabe-Schema und -Datensätze angezeigt werden [!DNL Experience Platform]. Weitere Informationen finden Sie im Tutorial [zu Schema-Daten zur](./preview-schema-data.md)Vorschau.

Sie haben außerdem erfolgreich Musterdaten für Einzelhandelsverkäufe mit dem bereitgestellten Bootstrap-Skript erfasst. [!DNL Experience Platform]

So arbeiten Sie weiter mit den erfassten Daten:
- [Analysieren Ihrer Daten mit Jupyter-Notebooks](../jupyterlab/analyze-your-data.md)
   - Verwenden Sie Jupyter-Notebooks in Data Science Workspace, um auf Ihre Daten zuzugreifen, sie zu untersuchen, sie zu visualisieren und zu verstehen.
- [Verpacken von Quelldateien in einem Rezept](./package-source-files-recipe.md)
   - In diesem Tutorial erfahren Sie, wie Sie Ihr eigenes Modell in eine [!DNL Data Science Workspace] Datei mit einer wichtigen Rezept-Datei packen können.