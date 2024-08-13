
# Table of Contents

1.  [Scripts](#org0588e2b)
    1.  [Talking to LLM through LM-studio](#orgb1f0264)
    2.  [Talking to AnythinLLM](#org345ed8e)
    3.  [Base Prompt for AI topic classification:](#orgfae4150)
    4.  [Prompt + examples for AI topics classification](#orgdb29a73)
    5.  [Template script for generating bar-plot](#org8cb91b1)
        1.  [Figures quality check<code>[0/19]</code>](#orgef69e38)
        2.  [Script](#org70bd80d)


<a id="org0588e2b"></a>

# Scripts


<a id="orgb1f0264"></a>

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


<a id="org345ed8e"></a>

## Talking to AnythinLLM

import requests
import json

url = &ldquo;<http://localhost:3001/api/v1/workspace/ai_course_syllabus_analysis/chat>&rdquo;
data = {
  &ldquo;message&rdquo;: system4,
  &ldquo;mode&rdquo;: &ldquo;chat&rdquo;
}
api<sub>key</sub> = &ldquo;7FMSR1T-BED4NAK-Q09HTT0-CH87175&rdquo;

headers = {&ldquo;Authorization&rdquo;: f&ldquo;Bearer {api<sub>key</sub>}&rdquo;}

response = requests.post(url, headers=headers, data=data)

print(&ldquo;Status code:&rdquo;, response.status<sub>code</sub>)
print(&ldquo;Response content:&rdquo;, json.loads(response.text)[&rsquo;textResponse&rsquo;])


<a id="orgfae4150"></a>

## Base Prompt for AI topic classification:

&ldquo;&rdquo;&ldquo;you are an expert in AI education and writing AI course syllabi.
return only the following python dictionary without any additional text(not text before or after the dictionary). fill it with a
unique name of topics or algorithms students will learn in the course and the theme/section they belong to
according to the &rdquo;artificial intelligence: a modern approach&ldquo; 4th edition book. choose only one of the following classifications for each topic:

1- Artificial Intelligence Foundations

2- Problem Solving

3- Knowledge, Reasoning, and Planning

4- Uncertain Knowledge and Reasoning

5- Machine Learning

6- Communicating, Perceiving, and Acting

7- Other

.Don’t justify your answers. Don’t give information not mentioned in the CONTEXT INFORMATION. \`\`\`{topic/algorithm:classification}\`\`\`&ldquo;&rdquo;&ldquo;


<a id="orgdb29a73"></a>

## Prompt + examples for AI topics classification

This is another variation of the prompt to classify AI topics but with more information sent to the llm.

&ldquo;&rdquo;&ldquo;

You are an expert in AI education and writing AI course syllabi. return only the
filled following python dictionary without additional text(No text before or after the dictionary) filled with a
name of a topics and their classification(number from 1-7) according to their section in the book &rsquo;artificial intelligence: a modern approach&rsquo;. use the
following inforatoin as reference:

1- Introduction to Artificial Intelligence
Content/Keywords: Definitions of AI, historical development, foundational theories, state-of-the-art technologies,
risks and benefits, philosophical questions (e.g., &ldquo;Can machines think?&rdquo;), ethical considerations.

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

7- other: doesn&rsquo;t belong to any of the above
Content/Keywords: This would include any specialized topics not covered in
the main sections, such as specific interdisciplinary applications,
detailed case studies outside the typical domains, or emerging AI
technologies not detailed in the standard curriculum of the book.

Don’t justify your answers. Don’t give information not mentioned in the CONTEXT INFORMATION.(give No text before or after the dictionary). {topic : number from 1-7}


<a id="org8cb91b1"></a>

## Template script for generating bar-plot


<a id="orgef69e38"></a>

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


<a id="org70bd80d"></a>

### Script

import matplotlib.pyplot as plt

categories = []
values = []
total<sub>syllabi</sub> =  # Total number of syllabi

percentages = []

plt.figure(figsize=(10, 5))
bars = plt.bar(categories, values, color=&rsquo;skyblue&rsquo;, width=0.6)

for bar, val, percentage in zip(bars, values, percentages):
    yval = bar.get<sub>height</sub>()
    plt.text(bar.get<sub>x</sub>() + bar.get<sub>width</sub>()/2, yval + 1, f&rsquo;{val} ({percentage:.1f}%)&rsquo;, va=&rsquo;bottom&rsquo;, ha=&rsquo;center&rsquo;, color=&rsquo;black&rsquo;, fontsize=10)

plt.ylim(0, max(values) + 10)

plt.title(&rsquo;Distribution of Course Syllabi by Year&rsquo;, fontsize=16)
plt.xlabel(&rsquo;Year&rsquo;, fontsize=14)
plt.ylabel(&rsquo;Number of Syllabi (out of {total<sub>syllabi</sub>})&rsquo;, fontsize=14)

plt.xticks(fontsize=10)
plt.yticks(fontsize=10)

plt.savefig(&rsquo;path/to/save/figure.png&rsquo;, dpi=300)

plt.show()

