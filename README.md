# NYC Food Scrap Drop-off Sites Chatbot
## Dataset Selection and Explanation:
- Using the NYC Food Scrap Drop-off Sites dataset
- Explanation of why this dataset is appropriate for a custom chatbot
## Data Wrangling
- Loading the dataset into a pandas dataframe
- Creating a "text" column that contains comprehensive descriptions of each drop-off site
- Each text entry includes site name, borough, location, operating hours, hosting organization, website, and any special notes about acceptable materials
## Custom Query Process:
- Creating functions to generate custom prompts that include the dataset information
- The system prompt positions the AI as an expert in NYC food scrap drop-off sites
- Functions to call the OpenAI API with both custom and basic prompts for comparison
## Performance Demonstration:
- Two specific questions to demonstrate the enhanced performance:
  - "Can I compost meat and dairy at the Astoria Pug drop-off site?"
  - "What are the drop-off sites that are open 24/7 in Manhattan?"
- Each question is answered with both the custom prompt and a basic prompt to show the difference
