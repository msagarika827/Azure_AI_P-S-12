# Custom Skill for Azure AI Search - Margie's Travel

This repository demonstrates how to create a custom skill for Azure AI Search using a word frequency analysis on documents. The skill is added to an AI search solution for **Margie's Travel**, a fictitious travel agency. The custom skill analyzes documents, counts the frequency of words, and returns the top 5 most frequently used words, enriching the search experience.

## Prerequisites

Before proceeding, ensure you have the following setup:

- **Azure Subscription**: Ensure that your Azure subscription is active and you have the necessary permissions to create resources.
- **Visual Studio Code**: You will be developing the solution using Visual Studio Code.
- **Azure CLI**: The Azure CLI will be used to interact with Azure resources.
- **Git**: To clone this repository and manage the project files.

## Setting Up the Development Environment

### 1. Clone the Repository

Clone the repository to your local machine by running the following command in your terminal:

```bash
git clone https://github.com/MicrosoftLearning/mslearn-knowledge-mining.git
```

Once cloned, open the repository folder in Visual Studio Code.

### 2. Install Dependencies

If prompted, install the required dependencies for C# code in the repository.

### 3. Configure Azure Resources

Before running the code, ensure the required Azure resources are created as per the instructions. These resources include an Azure AI Services multi-service account, a storage account, and an Azure AI Search service. 

#### Create Azure AI Services Account

1. Log in to your Azure portal and create a multi-service account for Azure AI.
2. Use the Azure portal to retrieve the subscription ID, resource group name, and location.

#### Setup Script Configuration

In the `Labfiles/02-search-skill` folder:

1. Open the `setup.cmd` script in Visual Studio Code.
2. Modify the `subscription_id`, `resource_group`, and `location` variables with the appropriate values.
3. Save the script and run it using the terminal:

```powershell
./setup
```

### 4. Create Search Solution

Once the resources are created, proceed with creating a search solution. This includes defining the data source, skillset, index, and indexer through JSON files.

- **data_source.json**: Define the connection to your storage account.
- **skillset.json**: Define the AI skills pipeline, including your custom word frequency skill.
- **index.json**: Define the searchable index structure.
- **indexer.json**: Configure the indexer to apply the skillset.

In the `create-search` folder, replace the placeholders in each of these files with the actual values from your Azure resources (e.g., connection strings, keys).

### 5. Deploy the Search Solution

After configuring the JSON files:

1. Open the `create-search.cmd` file and modify the `YOUR_SEARCH_URL` and `YOUR_ADMIN_KEY` placeholders with your Azure AI Search service details.
2. Save the changes and run the script:

```powershell
./create-search
```

### 6. Search the Index

Once the index has been populated, you can use the Search Explorer in the Azure portal to run queries against the index.

Sample query to search for documents mentioning "London" with a positive sentiment:

```text
search=London&$select=url,sentiment,keyphrases&$filter=metadata_author eq 'Reviewer' and sentiment eq 'positive'
```

## Creating the Custom Word Frequency Skill

In this project, we create a custom skill using an Azure Function in Node.js. The function analyzes the frequency of words in each document and returns the top 5 most frequent words (excluding common stopwords).

### 1. Create a Function App

Create a new **Function App** in the Azure portal with the following settings:

- **Function App name**:
- **Runtime stack**: Node.js (version 18 LTS)
- **Region**: Same as your Azure AI Search resource

### 2. Create a Word Count Function

1. Inside the Function App, create a new function using the HTTP trigger template.
2. Replace the default code with the provided word count function code (available in the repository).
3. Deploy the function.

### 3. Integrate the Custom Skill

Use the custom skill in the AI enrichment pipeline to process documents, extract word frequency data, and add it to the search index. This will improve the search experience by providing insights into frequently used words.

## Contributions

If you would like to contribute to this repository, feel free to submit issues or pull requests. We welcome suggestions, bug fixes, and improvements to this project.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgements

- **Azure AI Services**: For providing the cognitive services needed for the custom skills.
- **GitHub**: For hosting the repository.
- **Microsoft Learning**: For providing the original instructional materials.

---

For further details, refer to the official [Azure AI Search documentation](https://learn.microsoft.com/en-us/azure/search/).
```
