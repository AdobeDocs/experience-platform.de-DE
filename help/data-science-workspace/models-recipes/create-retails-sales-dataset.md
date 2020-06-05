---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Schema und Dataset für den Einzelhandel erstellen
topic: Tutorial
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# Schema und Dataset für den Einzelhandel erstellen

Dieses Tutorial bietet Ihnen die Voraussetzungen und Elemente, die für alle anderen Lernprogramme des Arbeitsbereichs [!DNL Adobe Experience Platform] für Datenwissenschaften erforderlich sind. Nach Abschluss des Projekts stehen Ihnen und Mitgliedern Ihrer IMS-Organisation auf Experience Platform das Schema und die Datensätze für den Einzelhandel zur Verfügung.

## Erste Schritte

Bevor Sie dieses Lernprogramm starten, müssen Sie über die folgenden Voraussetzungen verfügen:
- Zugriff auf [!DNL Adobe Experience Platform]. Wenn Sie keinen Zugriff auf eine IMS-Organisation in Experience Platform haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.
- Autorisierung zum Durchführen von Experience Platform-API-Aufrufen. Führen Sie das Lernprogramm zum [Authentifizieren und Zugreifen auf Adobe Experience Platform-APIs](../../tutorials/authentication.md) durch, um die folgenden Werte abzurufen, damit dieses Lernprogramm erfolgreich abgeschlossen werden kann:
   - Genehmigung: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Kundengeheimnis: `{CLIENT_SECRET}`
   - Client-Zertifikat: `{PRIVATE_KEY}`
- Beispieldaten und Quelldateien für das [Einzelhandelsverkaufsrezept](../pre-built-recipes/retail-sales.md). Laden Sie die für diese und andere Data Science Workspace-Tutorials erforderlichen Assets aus dem öffentlichen Git-Repository von [Adobe herunter](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) und die folgenden Python-Pakete:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Ein funktionierendes Verständnis der folgenden in diesem Lernprogramm verwendeten Konzepte:
   - [Erlebnisdatenmodell (XDM)](../../xdm/home.md)
   - [Grundlagen der Schema-Komposition](../../xdm/schema/field-dictionary.md)

## Schema und Dataset für den Einzelhandel erstellen

Das Retail Sales-Schema und die Datensätze werden automatisch mithilfe des bereitgestellten Bootstrap-Skripts erstellt. Gehen Sie wie folgt vor, um die Reihenfolge zu ändern:

### Dateien konfigurieren

1. Navigieren Sie im Experience Platform-Lernprogramm-Ressourcenpaket zum Ordner `bootstrap`und öffnen Sie `config.yaml` es mit einem entsprechenden Texteditor.
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

1. Öffnen Sie die Terminalanwendung und navigieren Sie zum Ordner für die Experience Platform-Lernhilfe.
2. Legen Sie den `bootstrap` Ordner als aktuellen Arbeitspfad fest und führen Sie das `bootstrap.py` Python-Skript aus, indem Sie den folgenden Befehl eingeben:

   ```bash
   python bootstrap.py
   ```

   > [!NOTE] Das Skript kann mehrere Minuten dauern.

## Nächste Schritte

Nach erfolgreichem Abschluss des Bootstrap-Skripts können die Retail Sales-Input- und -Output-Schema und -Datensätze auf Experience Platform angezeigt werden. Weitere Informationen finden Sie im Tutorial [zu Schema-Daten zur](./preview-schema-data.md)Vorschau.

Sie haben außerdem erfolgreich Musterdaten für Einzelhandelsverkäufe in Experience Platform mit dem bereitgestellten Bootstrap-Skript erfasst.

So arbeiten Sie weiter mit den erfassten Daten:
- [Analysieren Ihrer Daten mit Jupyter-Notebooks](../jupyterlab/analyze-your-data.md)
   - Verwenden Sie Jupyter-Notebooks in Data Science Workspace, um auf Ihre Daten zuzugreifen, sie zu untersuchen, sie zu visualisieren und zu verstehen.
- [Verpacken von Quelldateien in einem Rezept](./package-source-files-recipe.md)
   - In diesem Lernprogramm erfahren Sie, wie Sie Ihr eigenes Modell in den Data Science Workspace bringen, indem Sie Quelldateien in einer wichtigen Recipe-Datei verpacken.