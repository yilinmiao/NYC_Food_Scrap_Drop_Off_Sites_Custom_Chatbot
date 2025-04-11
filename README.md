# NYC Food Scrap Drop-Off Sites Custom Chatbot

## Overview

This project demonstrates the creation of a custom chatbot using OpenAI's API, specifically tailored to answer questions about NYC Food Scrap Drop-off Sites. By leveraging a specific dataset and custom prompt engineering, the chatbot provides more accurate and context-aware responses compared to a generic prompt.

## Features

* Loads and processes data from the NYC Food Scrap Drop-off Sites dataset.
* Generates structured text descriptions for each drop-off site based on dataset columns.
* Employs custom system prompts that integrate site-specific data to guide the OpenAI API.
* Compares the performance of custom prompts against basic prompts using specific example questions.
* Utilizes the `gpt-3.5-turbo` model via the OpenAI API for response generation.

## Dataset

* **Source:** The primary data source is the `nyc_food_scrap_drop_off_sites.csv` file, originating from NYC Open Data (specifically, the Food Scrap Drop-off Sites dataset).
* **Relevance:** This dataset is highly suitable due to its comprehensive and structured information about composting locations throughout NYC. Key details captured include:
    * Borough and Neighborhood (NTA Name)
    * Site Name and Address
    * Operating Hours and Months
    * Hosting Organization
    * Website Information
    * Specific instructions or notes (like accepted materials)

    This allows for the creation of a knowledgeable chatbot capable of providing specific, actionable information to users looking for composting options.

## Methodology

The project follows these main steps:

1.  **Data Wrangling:**
    * The dataset (`.csv` file) is loaded using the `pandas` library into a DataFrame.
    * A function processes each row of the DataFrame. It selects relevant fields (like name, location, hours, notes, etc.) and concatenates them into a single, descriptive string.
    * This string, containing a summary of each site, is stored in a new column named `text` within the DataFrame. This `text` column serves as the knowledge base for the custom prompt.

2.  **Custom Prompt Engineering:**
    * A carefully crafted "system prompt" is created. This prompt sets the context for the AI, defining its role as an expert on NYC food scrap sites.
    * The core of the custom prompt involves dynamically inserting the text descriptions (from the `text` column of the DataFrame) for multiple sites directly into the system prompt. This effectively "teaches" the AI about specific site details before it answers the user's question.
    * The system prompt also includes instructions on *how* the AI should answer, directing it to use the provided site information and be accurate.

3.  **OpenAI API Integration:**
    * The `openai` Python library connects to the OpenAI API.
    * Two functions are defined to handle API calls:
        * One function (`get_completion_with_custom_prompt`) sends the user's query along with the data-rich system prompt to the `gpt-3.5-turbo` model.
        * A second function (`get_completion_with_basic_prompt`) sends the same user query but uses a generic system prompt (e.g., "You are a helpful assistant") for comparison purposes.

## Setup and Installation

1.  **Prerequisites:** Ensure you have Python 3.x and `pip` installed.
2.  **Clone Repository:** If this project is in a Git repository, clone it to your local machine.
3.  **Install Dependencies:** Open your terminal or command prompt, navigate to the project directory, and run:
    `pip install pandas numpy openai python-dotenv`
4.  **API Key:**
    * Create a file named `.env` in the root directory of the project.
    * Inside `.env`, add the line: `OPENAI_API_KEY='YOUR_OPENAI_API_KEY_HERE'`, replacing the placeholder with your actual key.
    * The Python script uses the `python-dotenv` library to load this key automatically.

## Usage

1.  Place the `nyc_food_scrap_drop_off_sites.csv` dataset file in the same directory as the main Python script, or adjust the file path within the script accordingly.
2.  Ensure the `.env` file is correctly set up with your OpenAI API key.
3.  Execute the Python script from your terminal:
    `python your_script_name.py`
    (Replace `your_script_name.py` with the actual filename).

The script will perform the data processing and then query the OpenAI API using both the custom and basic prompts for the pre-defined demonstration questions. The responses for both approaches will be printed to the console.

## Performance Demonstration

The effectiveness of injecting dataset knowledge via the custom prompt is shown through two examples:

1.  **Question:** "Can I compost meat and dairy at the Astoria Pug drop-off site?"
    * **Custom Prompt Result:** The AI correctly uses the information fed to it (from the data subset) to state that this specific site *does not* accept meat/dairy, and provides other relevant site details (hours, location).
    * **Basic Prompt Result:** The AI provides generic advice about composting meat/dairy, failing to reference the specific site or its rules, leading to potentially incorrect guidance for the user.

2.  **Question:** "What are the drop-off sites that are open 24/7 in Manhattan?"
    * **Custom Prompt Result:** The AI successfully lists specific Manhattan drop-off sites from the provided dataset context that operate 24/7, including their names and details.
    * **Basic Prompt Result:** The AI misunderstands the context, suggesting generic 24/7 locations like courier services or convenience stores, completely missing the "food scrap drop-off" requirement.

**Conclusion:** The demonstration clearly shows that the custom prompt, enriched with specific dataset information, enables the chatbot to provide significantly more accurate, relevant, and useful responses compared to relying on the model's general knowledge alone.

## Dependencies

* pandas
* numpy
* openai
* python-dotenv
