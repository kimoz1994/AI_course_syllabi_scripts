
# Table of Contents

1.  [Scripts](#orgef5d50a)
    1.  [Talking to LLM through LM-studio](#orgb266de5)
    2.  [Talking to AnythinLLM](#org867911f)
    3.  [Base Prompt for AI topic classification:](#org9054e23)
    4.  [Prompt + examples for AI topics classification](#org84ed903)
    5.  [Template script for generating bar-plot](#org9756258)
        1.  [Figures quality check<code>[0/19]</code>](#orgbc4d6ba)
        2.  [Script](#orgc448572)


<a id="orgef5d50a"></a>

# Scripts


<a id="orgb266de5"></a>

## Talking to LLM through LM-studio

    

from openai import OpenAI

client = OpenAI(base<sub>url</sub>=&ldquo;<http://localhost:1234/v1>&rdquo;, api<sub>key</sub>=&ldquo;lm-studio&rdquo;)

completion = client.chat.completions.create(
  model=&ldquo;lmstudio-community/Meta-Llama-3-8B-Instruct-GGUF&rdquo;,
  messages=[
    {&ldquo;role&rdquo;: &ldquo;system&rdquo;, &ldquo;content&rdquo;: system},
    {&ldquo;role&rdquo;: &ldquo;user&rdquo;, &ldquo;content&rdquo;: user}
  ],
  temperature=0,
)

print(completion.choices[0].message.content)

\#+END<sub>SRC</sub>


<a id="org867911f"></a>

## Talking to AnythinLLM

    
    
    # use the following snippet to interact with AnythinLLM. you have to have the LLM, LM-studio and AnythinLLM installed.
    
    import requests
    import json
    
    # Example POST request
    url = "http://localhost:3001/api/v1/workspace/ai_course_syllabus_analysis/chat"
    data = {
      "message": system4,
      "mode": "chat"
    }
    api_key = "7FMSR1T-BED4NAK-Q09HTT0-CH87175"
    
    # Add API key to headers
    headers = {"Authorization": f"Bearer {api_key}"}
    
    response = requests.post(url, headers=headers, data=data)
    
    # Print response status code and content
    print("Status code:", response.status_code)
    print("Response content:", json.loads(response.text)['textResponse'])


<a id="org9054e23"></a>

## Base Prompt for AI topic classification:

    
    
    # use the following prompt along with the a list of AI topics and send them to the LLM
    
    """you are an expert in AI education and writing AI course syllabi.
    return only the following python dictionary without any additional text(not text before or after the dictionary). fill it with a
    unique name of topics or algorithms students will learn in the course and the theme/section they belong to
    according to the "artificial intelligence: a modern approach" 4th edition book. choose only one of the following classifications for each topic:
    
    1- Artificial Intelligence Foundations
    
    2- Problem Solving
    
    3- Knowledge, Reasoning, and Planning
    
    4- Uncertain Knowledge and Reasoning
    
    5- Machine Learning
    
    6- Communicating, Perceiving, and Acting
    
    7- Other
    
    .Don’t justify your answers. Don’t give information not mentioned in the CONTEXT INFORMATION. ```{topic/algorithm:classification}```"""


<a id="org84ed903"></a>

## Prompt + examples for AI topics classification

    
    
    
    This is another variation of the prompt to classify AI topics but with more information sent to the llm.
    
    
    
    """
    
    You are an expert in AI education and writing AI course syllabi. return only the
    filled following python dictionary without additional text(No text before or after the dictionary) filled with a
    name of a topics and their classification(number from 1-7) according to their section in the book 'artificial intelligence: a modern approach'. use the
    following inforatoin as reference:
    
    1- Introduction to Artificial Intelligence
    Content/Keywords: Definitions of AI, historical development, foundational theories, state-of-the-art technologies,
    risks and benefits, philosophical questions (e.g., "Can machines think?"), ethical considerations.
    
    
    2- Problem-solving
    
    Content/Keywords: Search algorithms, problem-solving agents, adversarial search, game theory, heuristic methods,
    constraint satisfaction problems, environments (deterministic, stochastic, episodic, dynamic), agent structures.
    
    
    3- Knowledge and reasoning and planning
    
    Content/Keywords: Logical agents, first-order logic, propositional logic, inference methods, knowledge representation, automated planning,
    reasoning systems, ontological engineering, effective model checking, planning algorithms, knowledge engineering.
    
    
    4- Uncertain knowledge and reasoning
    
    Content/Keywords: Probabilistic reasoning, Bayesian networks, decision-making under uncertainty,
    quantifying uncertainty, inference in temporal models, probabilistic programming,
    utility theory, decision networks, Markov decision processes (MDPs), partially observable MDPs (POMDPs).
    
    
    5- Machine Learning
    
    Content/Keywords: Forms of learning, supervised and unsupervised learning,
    decision trees, model selection, reinforcement learning, deep learning, statistical learning,
    learning probabilistic models, learning algorithms, ensemble learning,
    generalization in machine learning, learning from rewards. This also includes model training and evaluation and all the middle
    steps in that process.
    
    6- Communicating, perceiving, and acting
    
    Content/Keywords: Natural language processing, computer vision, robotics,
    language models, parsing, object detection, robotic perception and control,
    deep learning for NLP, augmented grammars, sequence-to-sequence models, transformer architectures
    
    7- other: doesn't belong to any of the above
    Content/Keywords: This would include any specialized topics not covered in
    the main sections, such as specific interdisciplinary applications,
    detailed case studies outside the typical domains, or emerging AI
    technologies not detailed in the standard curriculum of the book.
    
    
    Don’t justify your answers. Don’t give information not mentioned in the CONTEXT INFORMATION.(give No text before or after the dictionary). {topic : number from 1-7}


<a id="org9756258"></a>

## Template script for generating bar-plot


<a id="orgbc4d6ba"></a>

### Figures quality check<code>[0/19]</code>

-   [ ] title
-   [ ] x-label
-   [ ] y-label
-   [ ] font x-label 14
-   [ ] font y-label 14
-   [ ] font title 16
-   [ ] font values on bars 10
-   [ ] x-ticks font size 10
-   [ ] y-ticks font size 10
-   [ ] x-numbers/items
-   [ ] y-numbers/items
-   [ ] values on bars
-   [ ] percentages on bars
-   [ ] check if percentages correct
-   [ ] height and width of figure (horizontal: 10,5, vertical = 10 , 5 )
-   [ ] width or height of bars (horizontal(height) = 0.5, vertical(width) =0.6)
-   [ ] number of syllabi chart is based on(submissions)
-   [ ] check capitalization for all
-   [ ] y-axis range


<a id="orgc448572"></a>

### Script

    
    
    import matplotlib.pyplot as plt
    
    # Data
    categories = []
    values = []
    total_syllabi =  # Total number of syllabi
    
    # Calculate percentages for each value
    percentages = []
    
    # Creating the bar chart
    plt.figure(figsize=(10, 5))
    bars = plt.bar(categories, values, color='skyblue', width=0.6)
    
    # Adding the value labels on top of each bar for clarity
    for bar, val, percentage in zip(bars, values, percentages):
        yval = bar.get_height()
        plt.text(bar.get_x() + bar.get_width()/2, yval + 1, f'{val} ({percentage:.1f}%)', va='bottom', ha='center', color='black', fontsize=10)
    
    # Adjust the y-axis to fit labels
    plt.ylim(0, max(values) + 10)
    
    # Adding title and labels
    plt.title('Distribution of Course Syllabi by Year', fontsize=16)
    plt.xlabel('Year', fontsize=14)
    plt.ylabel('Number of Syllabi (out of {total_syllabi})', fontsize=14)
    
    plt.xticks(fontsize=10)
    plt.yticks(fontsize=10)
    
    # Save the plot as a PNG file with high quality (300 DPI)
    plt.savefig('path/to/save/figure.png', dpi=300)
    
    # Show the plot
    plt.show()

