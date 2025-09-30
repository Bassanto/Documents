# Overview
Welcome to my analysis on  data job market , focusing on data analytics roles. The project was created out of desire to navigate and understand the job market more efficiently. It drives into the top-paying and in-demand skills to help find optimal job opportunities for data analysts.

The data sourced from Luke Barousse's Python Course which provides a foundarion of my analysis,containing detailed information on job titles, salaries,locations and essential skills. Through a series of python scripts, I explore key questions such as the most demanded skill, salary trends, and the interaction of the demand and salary in data analytics.
# The Questions

Below are the questions i want to answer in my project:
   1. What arebthe skill most in demand for the top 3 most popular data roles?
   2. How are in-demand skills trending for Data Analysts?
   3. How well do jobs and skills pay for Data Analysts?
   4. What are the optimal skills for data analysts to learn(High Demand AND High Paying)
   
# Tools I used
 For my deep dive into data analyst job market, i harnessed the power of several key tool:

- Python: The backbone of my analysis,allowing me to analyze the data and find critical insights. I also used the following python libraries:
    - Pandas Library: This was used to analyze the data 
    - Matplotblib Library: I used it to visualise the data
    - Seaborn Library: Helped me create more advanced visuals

- Jupyter Notebooks: The tool I used to run my python scripts which help me easily include my notes and analysis.
- Visual Studio Code: My go-to for executing Python scripts.
- Git & Github: Essential for version control and sharing my Python code and analysis, ensuring collaboration among my teammates.

# Data Preparation and Cleanup
The section outline the steps taken to prerpare the data for analysis, ensuring accuracy and usability.

## Import  and Cleanup  Data

I used neccesary libraries and loading the dataset, followed by initial data cleaning to ensure the data provides the required result.

## The Analysis 

## 1. What are the most demanded skills for top 3 most popular data roles?

To find the most demanded skilss for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular ,and got the top 5 skills for those top 3 rolwes. This query highlights the most popular job titlesand their top skills I should pay attention to depending on the roles 
I'm targeting .

view my notebook with detailed steps here:
[2_skill_count.ipybn](2_skill_count.ipynb)

### Visualize Data 

~~~python 
fig,ax = plt.subplots(len(job_title),1)

sns.set_theme(style="ticks")

for i, title in enumerate(job_title):
    df_plot = df_skill_perc[df_skill_perc["job_title_short"] == title].head(5)

    #df_plot.plot( kind = "barh", x= "job_skills", y = "skill_percent", ax=ax[i],title = title)
    sns.barplot(data = df_plot, x = "skill_percent",y = "job_skills",ax=ax[i],hue="job_skills",palette="dark:b_r",dodge=False)

    ax[i].set_title(title)
    ax[i].set_xlabel(" ")
    ax[i].set_ylabel(" ")
    ax[i].set_xlim(0,78)
    #ax[i].legend().set_visible(False)
     
    for n,v in enumerate(df_plot["skill_percent"]):
       ax[i].text(v +1 , n, f'{int(v)}%',va= "center")

    if i != len(job_title) -1:
        ax[1].set_xticks([])

fig.suptitle("Likelihood of Skills Requested in US Job Postings",fontsize=16)
fig.tight_layout(h_pad=0.1)    
fig.subplots_adjust(top=0.88)

plt.show()
~~~

## Results
<img width="706" height="497" alt="Screenshot 2025-09-30 190750" src="https://github.com/user-attachments/assets/fb103650-f6df-4e61-892a-4a916a74ca15" />



### Insight


- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists(72%) and Data Engineers (65%).
- SQL is the most requested skill for Data Analyst and Data Scientists, with it in over half the job postings for both roles. For Data Engineer, Python is the most sought-after skill, appearing in 68% of the job postings
-   Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau)


## 2. How are in-demand trending for Data Analysts?

### Visualize Data

~~~python

df_plot = df_DA_US_percent.iloc[:, :5]

sns.lineplot(data = df_plot ,dashes = False , palette = "tab10")
sns.set_theme(style = "ticks")
sns.despine()

plt.title("Trending Top Skills for Data Analysts in the US")
plt.ylabel("Liklihood of Job Posting")
plt.xlabel("2023")
plt.ylim(0,80)

from matplotlib.ticker import PercentFormatter
ax= plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter())
plt.show()
~~~
### Result
<img width="580" height="455" alt="Screenshot 2025-09-30 190852" src="https://github.com/user-attachments/assets/fc7aeada-7168-4c00-b692-0c394aec31f6" />
 

### Insights

- SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand.
- Excel is the most demanded skill of Data Analyst after SQL. Although there were slight fall in demand during the year .
- Tablue and Python has been on competition. there demand are relatively consistent throughtout the year.
- SAS on the other hand has improved ;surpassing other notable skills like Power bi. 


## How well do jobs and skills pay for Data Analysts?

### Salary Analysis for Data Nerds 

~~~python
sns.boxplot(data=df_US_top6,x="salary_year_avg",y="job_title_short",order =job_order)

ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}K'))
plt.show()
~~~

### Result
<img width="712" height="445" alt="Screenshot 2025-09-30 190659" src="https://github.com/user-attachments/assets/17a8543e-9c79-4b5a-8388-05f8fc85e347" />

### Insights

- Senior Data Scientist has the highest salary amongst other data science jobs with its median salary around 155k. This indicate high value placed on it due to advanced skills and funstions they perform.
- Senior Data Engineer and Senior Data Scientist roles show a considerable high outliers at the high end of salary spectrum suggesting that expectional skills can pay high salary.
- Finally, the median salaries differs from each other with regard to there specific responsibilities. The senior data nerds earns higher as they bore more responsibilites which are actualized with certain expectional skills.

### Highest Paid and most Demanded Skills for Data Analyst

#### Visualize Data 

~~~python
# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data = df_DA_top_pay,x = "median", y = df_DA_top_pay.index, ax =ax[0],hue="median",palette="dark:b")

# Top 10 Most In-Demand skills for Data Analysts
sns.barplot(data = df_DA_skills,x = "median" ,y = df_DA_skills.index, ax =ax[1],hue="median",palette="light:b")
plt.show()
~~~
#### Result
<img width="619" height="472" alt="Screenshot 2025-09-30 190935" src="https://github.com/user-attachments/assets/8698b71d-d96a-4042-b0bb-482d09ac36d8" />


#### Insights:

- The top graph shows that technical skills like 'dplyr'.'Bitbucket', and 'Gitlab' are associated with higher salaries, some are reaching up to $200k, suggesting advanced technical proficiency can incresase earning potential.

- The bottom graph highlights fundamental skills like 'Excel' , 'Powerpoint', and 'Sql' are the most in-demand , even though they do not offer the highest salary.

- There is clear distinction between the skills that are highest paid and thos that are most in-demand. Data analysts aiming to maximise their carrer potential should consider developing diverse skill set that includes both high-paying specialized skills and widely demanded foundational skills.

## 4. What are the most optimal skill to learn for Data Analysts?

#### Visualize Data

~~~python
from adjustText import adjust_text

#df_DA_skills_high_demand.plot(kind = "scatter", x= "skill_percent",y="median_salary")
sns.scatterplot(
    data = df_plot,
      x="skill_percent",
      y="median_salary",
      hue="Technology"
      )

sns.set_theme(style = "ticks")
sns.despine()

texts = []
for i,txt in enumerate(df_DA_skills_high_demand.index):
    texts.append(plt.text(df_DA_skills_high_demand["skill_percent"].iloc[i],df_DA_skills_high_demand["median_salary"].iloc[i],txt))

adjust_text(texts,arrowprops=dict(arrowstyle="<-",color = "gray"),    
    force_text=0.5,    
    expand_text=(2, 2)  ,
  )   
  ~~~
  #### Result
<img width="592" height="443" alt="Screenshot 2025-09-30 190500" src="https://github.com/user-attachments/assets/d5f7ec41-b139-4cd6-85db-7361f63df8ac" />


#### Insights

- The scatter the most of the "programming" skills (coloured with blue) tends to cover higher salary levels compared to other categories, indicating that programming expertise might offer greater salary salary benefit within the data analytics field.
- Analyst tools (coloured green) including Tableau and Power Bi offers the prevalent in job postings and offer competitive salaries. This category does not only have good salary but is also versatile across different type of data tasks.
- The database skills (coloured orange) such as Oracle and SQL Server are associated with a very high salary. This is to indicate the value of data management and manipiulation  expertists in the industry.

# What I Learned 
 Throughout this project, i deepened my understanding of the data analyst job market and enhanced myntechnical skill in Python,espacially in data manipulation and visualization. Here are the few specific things i learned:
- Advanvced Python Usage: Ultilising libries such as Pandas for data manipulation, Seaborn and Matplotlib for visualization,and other libries helped me to perform complex data analysis tasks more efficiently.
- Data Cleaning Importance: I learned that through data cleaning and preparation are crucial before any analysis can be conducted, ensuring the accurancy of insights derived from the data.
- Strategic Skill Analysis: The project emphasized the importance of aligning ones skill with market demand. Understanding the relationship between skill demand, salary,and job availability allows for more strategic career planning in the tech industry.

# Insights
The provided several general insights into the data job market for analysts:
- Skill Demand and Salary Correlation: There is a clear correlation between the demand for specific skills and the salaries these skills command. Advanced and specialized skill like Python and Oracle often lead to higher salaries.
- Marker Trend: There are changing trends in skill demand, highlighting the dynamic nature of the data job market. Keeping up with these trends is essential for career growth in data analytics.
- Economic Value of Skills: Understanding which skill are both in-demand and well-compensated can guide data analysts in prioritizing learning to maximize  their economic return.

# Challenges I Faced
This project was not without its challenges,but it provided good learning oppoturnities:

- Data Inconsistencies: Handling missing data requires careful consideration to ensure intergrity of the anaysis.
- Complex Data Visualization: Visualizing complex dataset was challenging owning to the fact the dataset is ambigious but insights had to be conveyed clearly.

# Conclusion 
The exploration into data  market has been incredibly informative,highlighting the critical skills and trend that shape this evolving field. The insights I got enhanced my understanding and provide actionable guidance for anyone looking to advance there career in data analytics. As the market continues to change, ongoing analysis will be essential to stay ahead in data analytics. This project is a good foundation for future exporations and underscores the importance of continous learning and adaptation in the data field.
