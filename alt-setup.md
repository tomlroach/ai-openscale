---

copyright:
  years: 2018
lastupdated: "2018-12-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Installing a Python module to set up {{site.data.keyword.aios_short}}
{: #module}

To automate the provisioning and configuration of the required {{site.data.keyword.cloud_notm}} services and see an {{site.data.keyword.aios_full}} application, including sample data, you can install a Python module.
{: shortdesc}

## About this module
{: #about}

- The module provides an alternate way for technical users to see an instance of {{site.data.keyword.aios_short}} up and running without needing to provision and configure the services yourself, as described in the [Getting started](/docs/services/ai-openscale/getting-started.html) tutorial.
- The Python module runs through the process of checking the services that you have and creating the ones that are necessary, including {{site.data.keyword.aios_short}}. After the module runs successfully, from the {{site.data.keyword.cloud_notm}} dashboard you can launch {{site.data.keyword.aios_short}} to see how it monitors a model.

## Before you begin
{: #prereqs}

1. [Create an {{site.data.keyword.cloud_notm}} API key and download it ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/iam/userid_keys.html#creating-an-api-key){: new_window} . You will need to enter the API key in a later step.

2. [Install any release of Python 3 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.python.org/downloads/){: new_window}.

   **Note**: Python 3 includes the required pip package management system.

3. Install the `ibm-ai-openscale-cli` package by running the following command:

    ```
    pip install -U ibm-ai-openscale-cli
    ```
    {: codeblock}

4. If you have an existing {{site.data.keyword.pm_short}} service instance, check the [{{site.data.keyword.cloud_notm}} dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/dashboard/apps){: new_window} to ensure that the service is managed by {{site.data.keyword.iamshort}} (IAM), not Cloud Foundry. Services managed by IAM are listed in the **Services** section.

  **Important**: The module checks for an instance of {{site.data.keyword.pm_short}}. If you have an instance, the module uses it. But if your instance is managed by Cloud Foundry, you must first [migrate it to an IAM resource group before running the module ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/resources/instance_migration.html){: new_window}.

## Running the module
{: #run}

Run the following command:

```
ibm-ai-openscale-cli --apikey <Your API key>
```
{: codeblock}

## Viewing results in {{site.data.keyword.aios_short}}
{: #open}

To view insights into the fairness and accuracy of the model, details of data that is monitored, and explainability for an individual transaction, open the [AI OpenScale dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}.

- To understand the scenario for the sample data, read [Use case and the value of AI OpenScale](/docs/services/ai-openscale/getting-started.html#use-case-and-the-value-of-ai-openscale).

### View insights
{: #insights}

From the [AI OpenScale dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, click the **Insights** tab, which shows an overview of metrics for deployed models: ![Insights](images/insight-dash-tab.png)

- At a glance, the Insights page shows any issues with fairness and accuracy, as determined by the thresholds that are configured.

- Each deployment is shown as a tile. The module configured a deployment called `DrugSelectionModel`, as shown in the following screen capture:

  ![Insight overview](images/setup01.png)

### View monitoring data
{: #monitoring}

1. From the Insights page, click the `DrugSelectionModel` tile to view details about the monitored data.
2. Slide the marker across the chart to view a day and time period that show data and then click the **View details** link.

   - For example, the following screen shows data for a specific date and time. The dates and times vary, depending on when you run the module.

   - For information about interpreting the time series chart, see [Monitoring Fairness, Average Requests per Minute, and Accuracy](/docs/services/ai-openscale/insight-timechart.html).

    ![Monitor data](images/setup02.png)

3. From the **Feature** menu, ensure that `AGE` is selected to see details about  `AGE` data monitoring.

  - Notice that in the following screen capture, the source of the bias is for the age group `36 to 44`.

  - The next section describes how to view the factors that contribute to bias.

  - For information about interpreting the visualization of the data points at a specific hour, see [Monitoring Fairness, Average Requests per Minute, and Accuracy](/docs/services/ai-openscale/insight-timechart.html#insight-data-visual).

    ![Age details](images/setup03-19dec.png)

### View explainability
{: #explain}

1. To understand the factors that contribute when bias is present for a given time period, from the visualization screen shown in the previous section, select the **View transactions** button.

  Transaction IDs for the past hour are listed.

1. Copy one of the transaction IDs.

  ![Transaction list](images/setup04.png)

1. Click the **Explainability** tab: ![Explainability](images/explainability.png)

  The "Explain a transaction" page is shown.

2. Paste the copied transaction ID into the search box and press the Enter key on your keyboard.

  - The page shows how the model arrived at its conclusion, including how confident the model is, the factors that contribute to the confidence level, and the attributes that were fed to the model.

  - For information about interpreting transaction explainability, see [Monitoring Explainability](/docs/services/ai-openscale/insight-explain.html).

    ![Explain a transaction](images/setup05.png)

## Related information
{: #info}

- To learn about biases, see [Fairness](/docs/services/ai-openscale/monitor-fairness.html).
- To learn about how well your model predicts outcomes, see [Accuracy](/docs/services/ai-openscale/monitor-accuracy.html).
- To learn about interpreting charts and data, see [Monitoring Fairness, Average Requests per Minute, and Accuracy](/docs/services/ai-openscale/insight-timechart.html).
- To learn how underlying factors influence outcomes, see [Monitoring explainability](/docs/services/ai-openscale/insight-explain.html).
