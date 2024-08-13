
# Table of Contents

1.  [Scripts](#org3a6d305)
    1.  [Talking to LLM through LM-studio](#org897ff9c)
    2.  [Talking to AnythinLLM](#org6bba7f6)
    3.  [Base Prompt for AI topic classification:](#org2d6413f)
    4.  [Prompt + examples for AI topics classification](#orge75e2eb)
    5.  [Template script for generating bar-plot](#orgfa5d984)
        1.  [Figures quality check<code>[0/19]</code>](#orgee528d0)
        2.  [Script](#org3fc4446)


<a id="org3a6d305"></a>

# Scripts


<a id="org897ff9c"></a>

## Talking to LLM through LM-studio

    
    # is used to interact with LM-sdudio to process and extract information from the text belonging to the 'outcomes' section.
    # to use it, you have to have the LLM and LM-studio installed. for more info, refer to the documentation for LM-studio
    # Example: reuse your existing OpenAI setup
    from openai import OpenAI
    
    # Point to the local server
    client = OpenAI(base_url="http://localhost:1234/v1", api_key="lm-studio")
    
    completion = client.chat.completions.create(
      model="lmstudio-community/Meta-Llama-3-8B-Instruct-GGUF",
      messages=[
        {"role": "system", "content": system},
        {"role": "user", "content": user}
      ],
      temperature=0,
    )
    
    print(completion.choices[0].message.content)


<a id="org6bba7f6"></a>

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


<a id="org2d6413f"></a>

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


<a id="orge75e2eb"></a>

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


<a id="orgfa5d984"></a>

## Template script for generating bar-plot


<a id="orgee528d0"></a>

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


<a id="org3fc4446"></a>

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

