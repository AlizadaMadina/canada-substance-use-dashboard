# Project Documentation: Canadian Substance Use Dashboard
### Written by Madina Alizada | May 2026

---

## Why I Built This

I want to be honest about why I chose this topic. It was not because it looked impressive on a resume or because someone told me to. It was because something about it genuinely bothered me.

Substance use has become so normalized in our society that people are forgetting about the real effects it has on human beings. I am not saying this as a statistic or a fact from a textbook. I am saying this as someone who pays attention to the world around her and feels something when she sees people hurting themselves without even realizing it. I wanted to look at the actual data behind this and understand, are these patterns as widespread as they seem? Which age groups are most affected? And can I turn that data into something visual that makes people stop and actually think?

This project is not going to change the world on its own. But I believe that when you show someone a clear, simple visualization of something difficult, and they suddenly understand it, that matters. That is why I built this.

---

## What This Project Is

This is an interactive data dashboard that explores how alcohol, cannabis, and opioid use varies across different age groups in Canada. The data comes directly from Health Canada's Canadian Substance Use Survey (CSUS) 2023, which surveyed over 36,000 Canadians aged 15 and older across all provinces.

The dashboard answers one central question: does substance use really differ across generations in Canada, and if so, how dramatically?

The short answer is yes, and the patterns are more surprising than most people would expect.

---

## Where the Data Came From

The data comes from Health Canada's official website at [health-infobase.canada.ca/substance-use/csus](https://health-infobase.canada.ca/substance-use/csus/). This is a survey that Health Canada runs every two years to understand trends in alcohol and drug use across the Canadian population. It is one of the most comprehensive public health datasets available in Canada.

I downloaded 3 CSV files covering alcohol, cannabis, and opioids. Each file contained hundreds of rows breaking down substance use by age group, province, gender, income level, and many other categories. In total, the raw data covered 97 different indicators or survey questions across all three substances.

---

## How I Started: Opening the Data for the First Time

When I first opened the CSV files in Microsoft Excel, I did not see the full picture right away. There were hundreds of rows and columns and it took time to understand what I was actually looking at. But as I started reading through the rows, something caught my attention immediately. The age groups showing the most activity in the data were people my age, people in their late teens and early twenties. That made it feel personal. This was not abstract data about strangers. This was data about people I could relate to.

That is when I knew I had picked the right dataset.

---

## Planning the Dashboard Before Touching Any Tool

Before I wrote a single line of code or opened Tableau, I spent time planning exactly what I wanted to build. This is something I learned is really important because jumping straight into building without a plan leads to wasted hours and confused decisions later.

I wrote a user story document, which is basically a formal description of what the dashboard should do, who it is for, and what questions it should answer. I decided my dashboard would be for any Canadian citizen who is curious about substance use patterns in their country, with no technical background required.

I also sketched a mockup showing where each chart would live on the dashboard, and I chose my color palette before touching Tableau. Blue for alcohol, yellow for cannabis, and mint green for opioids. Consistent colors across all charts so anyone looking at the dashboard immediately understands what each color means without reading a legend every time.

---

## The Technical Part: Cleaning the Data

This is where things got interesting and honestly a little frustrating at first.

My original plan was to use SQL and MySQL Workbench to clean and combine the three CSV files into one master table. SQL is the standard tool for this kind of work and I wanted to use it properly. But MySQL Workbench kept throwing errors when I tried to import the CSV files. The files contained French characters from the bilingual Health Canada data, and MySQL could not handle the encoding.

I spent time troubleshooting this and eventually decided to switch to Python. Looking back, I think this was the right call. I learned that in data work, the goal is to solve the problem, not to stick with a tool just because it sounds more impressive. Python handled the encoding issue instantly and let me move forward.

I built my data pipeline in a Jupyter Notebook, which is a tool that lets you write code and explain what you are doing in plain English right next to each other. This made my notebook both a working script and a piece of documentation at the same time.

Here is what the pipeline did, explained simply:

**Step 1: Load the raw data.** I opened the three CSV files, one for alcohol, one for cannabis, and one for opioids.

**Step 2: Filter for age group rows only.** Each file contained breakdowns by many different categories like province, gender, and income. I only kept the rows that showed data broken down by age group, because that was the central question of my dashboard. Think of it like having a huge spreadsheet and highlighting only the rows you care about.

**Step 3: Label each row with its substance.** When I combined the three files into one, I needed a way to tell which row came from which file. So I added a new column called "substance" and labeled every alcohol row as "Alcohol", every cannabis row as "Cannabis", and every opioid row as "Opioids".

**Step 4: Keep only the columns Tableau needs.** The original files had 22 columns each, many of which were in French or contained technical notes I did not need. I kept only 6 columns: substance, indicator, age group, percentage, sample count, and total surveyed.

**Step 5: Stack all three tables into one.** This is the equivalent of SQL's UNION ALL command. I piled the three filtered tables on top of each other into one single clean master table. Think of it like having three separate stacks of paper and combining them into one organized pile.

**Step 6: Handle missing values.** Some percentage values were blank. This was not a mistake in my code. Health Canada intentionally leaves certain values blank when the sample size for a specific group was too small to report a reliable percentage. Reporting a percentage based on very few people would be misleading, so they leave it empty. I removed those 35 rows safely because none of them affected the charts I was building.

**Step 7: Save the clean file.** The final output was a CSV file called master_age_substance.csv containing 638 clean rows, ready to connect directly to Tableau.

All of this is documented step by step with plain English explanations inside my Jupyter Notebook, which you can find in the scripts folder of this repository.

---

## Building the Dashboard in Tableau

This was my first time building a personal project in Tableau. I had watched tutorials before and understood the concepts, but this was the first time I sat down with my own data and built something from scratch.

What I discovered is that Tableau is genuinely incredible for this kind of work. Whatever story you want to tell with your data, you can drag and drop your way to a visualization that communicates it clearly. For someone who cares about making complex information accessible to people who are not technical, Tableau feels like a really powerful tool. Whatever raw data you have, you can transfer it into a dashboard that anyone can understand, even if they have no idea what happened behind the scenes. I find that really meaningful.

I built four charts:

**Chart 1: Substance Use by Age Group (Grouped Bar Chart)**
This is the hero chart at the top of the dashboard. It shows lifetime use rates for alcohol, cannabis, and opioids side by side for each of the four age groups: 15-19, 20-24, 25-54, and 55+. Each age group has three bars, one per substance, color coded consistently throughout the dashboard.

**Chart 2: Binge Drinking by Age Group (Horizontal Bar Chart)**
This chart digs deeper into alcohol specifically, showing which age group binge drinks the most. The finding here was surprising: 20-24 year olds have the highest binge drinking rate in Canada at around 60%, higher than any other age group including teenagers.

**Chart 3: Cannabis Use by Age Group (Horizontal Bar Chart)**
This chart shows past 12 month cannabis use by age group. Again, 20-24 year olds lead at around 52%, followed closely by 15-19 year olds at around 44%. The 55+ age group uses cannabis the least at around 20%, though that number is still significant.

**Chart 4: Opioid Misuse by Age Group (Horizontal Bar Chart)**
This was the most alarming finding in the entire dataset. 15-19 year olds have the highest rate of non-medical opioid use at around 23%, higher than any other age group. Teenagers are misusing opioids more than middle-aged adults or seniors. This is the kind of finding that makes you stop and think.

---

## What the Data Tells Us

Here are the key insights from this dashboard, explained simply:

Alcohol is the most widely used substance across every single age group in Canada. The 55+ age group has the highest lifetime alcohol use at around 93%, meaning almost every older Canadian has tried alcohol at some point in their life.

Cannabis use peaks in young adulthood. The 20-24 age group has the highest rates of both lifetime and recent cannabis use. This is likely connected to cannabis legalization in Canada in 2018, which made it more accessible to young adults.

Opioid misuse is a young person's problem more than people realize. While opioid use overall is low compared to alcohol and cannabis, the fact that teenagers have the highest non-medical opioid use rate is deeply concerning from a public health perspective.

Binge drinking is most common among young adults, not teenagers. Many people assume teenagers are the biggest binge drinkers, but the data shows it is actually the 20-24 age group that drinks most dangerously.

---

## What I Would Add in the Future

If I had more time and resources, here is what I would explore next:

I would love to add provincial breakdowns to see how substance use varies across Canada geographically. Does British Columbia have higher cannabis use than other provinces? Do prairie provinces have different opioid patterns? That would add a whole new dimension to the story.

I would also want to compare data across multiple survey years to show trends over time. Health Canada runs this survey every two years, so there is historical data available. Seeing how cannabis use changed before and after legalization in 2018 would be particularly compelling.

Finally, I would want to add a section on treatment-seeking behavior to see whether people who use substances at high rates are also seeking help at similar rates, or whether there is a gap between need and access to support.

---

## Tools and Technologies Used

**Python and pandas:** Used for data cleaning, filtering, and combining the three CSV files into one master dataset. Chosen because it handled the bilingual CSV encoding issue that blocked the SQL approach, and because it allowed me to document every step clearly inside a Jupyter Notebook.

**Jupyter Notebook:** Used as the environment for writing and running the Python data pipeline. Chosen because it allows code and plain English explanations to live side by side, making the notebook both a working script and a readable document.

**Tableau Public:** Used for building and publishing the interactive dashboard. Chosen because of its flexibility, its ability to create professional visualizations without writing frontend code, and its free publishing platform that makes dashboards accessible to anyone with a browser.

**GitHub:** Used for version control and project storage. The repository is organized into a data folder for raw and cleaned CSV files, a scripts folder for the Jupyter Notebook, a docs folder for documentation and mockups, and a README that links everything together.

---

## A Personal Note

I am a Data Science student at Simon Fraser University and this is one of the projects I am most proud of building. Not because of the technical complexity, but because the data means something to me personally. I genuinely care about people understanding the world around them more clearly, and I think data visualization is one of the most powerful ways to make that happen. Whenever I can turn something complicated into something easy for someone else to understand, that makes me really happy.

If even one person looks at this dashboard and thinks differently about substance use in Canada, that is enough for me.

---

*Data Source: Canadian Substance Use Survey (CSUS) 2023, Health Canada. [health-infobase.canada.ca/substance-use/csus](https://health-infobase.canada.ca/substance-use/csus/)*

*Live Dashboard: https://public.tableau.com/app/profile/madina.alizada/viz/Book1_17787142620000/Dashboard1*

*GitHub Repository: https://github.com/AlizadaMadina/canada-substance-use-dashboard*
