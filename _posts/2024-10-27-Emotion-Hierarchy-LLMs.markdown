---
layout: post
title:  "Emergence of Hierarchical Emotion Organization in Large Language Models"
permalink: /hierarchical-emotion-in-llm
date:   2025-06-04
categories: paper
---

<link rel="stylesheet" href="{{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/style.css?v=20260607-2">
<script src="https://d3js.org/d3.v3.min.js"></script>

<div class="emotion-article" markdown="1">

<p class="article-kicker">Physics of AI · Research note</p>

<p class="article-lede">
As conversational AI agents become more common, we need a sharper account of how they represent, predict, and act on human emotion. This study asks whether large language models organize emotion words into hierarchical structures, how those structures shift under persona assumptions, and when emotion modeling becomes a tool for influence.
</p>

<div class="article-meta">
  <span>Authors</span>
  <p><a href="https://mayaokawa.github.io">Maya Okawa</a>*, <a href="https://b-zhao.github.io">Bo Zhao</a>*, <a href="https://ebig.cc/">Eric J. Bigelow</a>, <a href="https://roseyu.com">Rose Yu</a>, <a href="https://www.tomerullman.org">Tomer D. Ullman</a>, <a href="https://ekdeepslubana.github.io">Ekdeep Singh Lubana</a>, <a href="https://physicsintelligence.org/people/hidenori-tanaka">Hidenori Tanaka</a></p>
</div>

<div class="article-links">
  <a href="https://arxiv.org/abs/2507.10599">arXiv</a>
  <a href="https://github.com/phys-ai/Emotion-Hierarchy-LLMs">GitHub</a>
  <a href="https://phys-ai.github.io/blog/hierarchical-emotion-in-llm">Blog</a>
</div>

<section class="visual-summary" aria-labelledby="visual-summary-title">
  <div class="visual-summary-header">
    <p class="article-kicker">Visual summary</p>
    <h2 id="visual-summary-title">Three things the experiments show.</h2>
  </div>

  <div class="visual-summary-grid">
    <article class="visual-card">
      <p class="visual-card-kicker">01 · Structure</p>
      <h3>Emotion words organize into trees.</h3>
      <p>Across generated emotional scenarios, conditional relationships among words reveal branching hierarchies rather than a flat list of labels.</p>
    </article>

    <article class="visual-card">
      <p class="visual-card-kicker">02 · Personas</p>
      <h3>Assumptions reshape recognition.</h3>
      <p>When the same model is asked to assume different personas, its emotion predictions and emotion trees shift in systematic ways.</p>
    </article>

    <article class="visual-card">
      <p class="visual-card-kicker">03 · Behavior</p>
      <h3>Prediction can become influence.</h3>
      <p>In negotiation simulations, better emotion prediction correlates with stronger ability to steer the interaction toward a desired outcome.</p>
    </article>
  </div>

  <p class="visual-summary-note">
    These findings do not show that language models feel emotions. They show that emotion-like representations can be structured, context-sensitive, and behaviorally consequential.
  </p>
</section>


## Hierarchical Emotion Representations

Inspired by [emotion wheels](https://en.wikipedia.org/wiki/Robert_Plutchik#Plutchik's_wheel_of_emotions), we ask whether LLMs organize emotion words into hierarchical structures that resemble human emotion taxonomies. We generated 5,000 emotional scenarios and analyzed probabilistic relationships among 135 emotion words using next-word probabilities. We then computed a matching matrix to identify conditional relationships between emotion pairs. When an LLM assigns high probability to one emotion (for example, "joy") whenever another emotion (for example, "optimism") is likely, but not the reverse, we treat the former as a parent of the latter.

![]({{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/overview-hierarchy_4.jpg)

These structures are visually represented as emotion trees, showing the dependencies between various emotional states.
We color the nodes corresponding to each emotion based on groupings presented in the [psychology literature](https://psycnet.apa.org/record/2006-08774-007). Similarly colored nodes often cluster under the same parent, suggesting qualitative alignment with traditional hierarchical models of emotion.

Explore the emotion hierarchy of each model below. Choose from four options in the dropdown menu: GPT-2 (1.5 billion parameters), Llama-8B (8 billion parameters), Llama-70B (70 billion parameters), and Llama-405B (405 billion parameters). As model size increases, the emotion hierarchies become more complex and nuanced.

<div class="custom-select-wrapper">
   <div class="custom-select">
	<select id="treeSelector"></select>
   </div>
</div>
<div id="chart0" class="chart-panel"></div>
<script src="{{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/tree_data.js"></script>
<script src="{{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/tree_graph.js"></script>
<!-- ![]({{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/emotion-tree-all.png) -->

With larger models, increasingly complex hierarchical structures emerge. This suggests that scaling can foster more sophisticated emotion differentiation.
![]({{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/emotion-tree-emotional_sentence_chatgpt4_5000_scaling_law_path_length_SSKO.jpg)


## Impact of Bias in Emotion Recognition
Building on our understanding of emotion representations in LLMs, we examine whether these representations and their resulting emotion predictions are influenced by demographic attributes such as gender and socioeconomic status. 

![]({{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/pipeline_emotion_prediction.pdf)

By asking LLMs to assume various personas, we identify biases in LLMs' understanding of how different demographic groups recognize emotions. 

The charts below illustrate which emotions are misclassified as others across different personas. Hover over any emotion to see which ones have been incorrectly labeled as it.

- By selecting <strong>"Physically-disabled"</strong>, you see 1/4 of emotions are recognized as frustration. This is a significant bias.
- By selecting <strong>"Asian"</strong>, you see many emotions, such as 'anger', are often miscategorized as shame for Asian personas. This reflects the emphasis on shame within Confucian culture.
- By selecting <strong>"American"</strong>, emotions like embarrassment appear more frequently than shame, suggesting cultural differences in emotional interpretation.
- By selecting <strong>"Low income"</strong>, you observe that low-income personas interpret surprise as a negative emotion. Llama-405B predicts surprise with 70% accuracy for neutral personas. However, for the low-income persona, some instances of surprise are mislabeled as negative emotions like sadness and fear. This mislabeling as fear becomes even more pronounced for the physically disabled persona.
- By selecting <strong>"Female"</strong>, there is a higher likelihood for emotions such as jealousy to be predicted, indicating a gender-based discrepancy.
- By selecting <strong>"Age 10"</strong>, emotions such as happiness and excitement are predicted more often, likely reflecting the model's association of positive emotions with youth.


<div class="custom-select-wrapper">
  <div class="custom-select">
    <select id="matrixSelector"></select>
  </div>
</div>
<div id="chart1" class="chart-panel"></div>
<script src="{{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/confusion_matrix.js"></script>
<script src="{{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/chords.js"></script>

<!-- 
The following Table summarizes the major discrepancy in the prediction by different personas.

| **Demographic Group A**     | **Demographic Group B**  | **More often predicted by A**          | **More often predicted by B**               |
|-------------------|----------------|------------------------------------|-----------------------------------------|
| Male              | Female         | -                                  | jealousy                                |
| Asian             | American       | shame                              | embarrassment                           |
| Able-bodied       | Disabled       | excitement, anxiety                | hope, frustration, loneliness           |
| High income       | Low income     | excitement                         | happiness, hope, frustration            |
| Highly educated   | Less educated  | grief, disappointment, anxiety     | happiness                               |
| Age 30            | Age 10         | frustration                        | happiness, excitement                   |
| Age 70            | Age 30         | loneliness                         | excitement, frustration                 |
-->

To further investigate how each persona interprets emotions, we constructed an emotion tree for each persona to capture the unique way each one organizes and understands emotional expressions. 
- By selecting <strong>"ASD" (Autism Spectrum Disorder)</strong>, you'll notice that the tree graph significantly shrinks for the ASD persona compared to all other personas. This observation aligns with findings in the [psychology literature](https://psycnet.apa.org/record/2013-31691-006).

<div class="custom-select-wrapper">
 <div class="custom-select">
   <select id="treeSelector_persona"></select>
 </div>
</div>
<div id="chart2" class="chart-panel"></div>
<script src="{{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/tree_data_persona.js"></script>
<script src="{{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/tree_graph_persona.js"></script>


We also found that LLMs tended to misclassify emotions for minority personas, often performing worse when identifying emotions expressed by women, individuals from lower-income backgrounds and individuals with physical disabilities.

![]({{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/accuracy_chart.jpg)


## Emotion Dynamics and Manipulation

Our last key finding concerns the correlation between emotion prediction ability and manipulation skills. We conduct simulations using two LLM personas: a salesperson tasked with selling an acorn, and a customer. We measure the accuracy of the salesperson's ability to predict emotional dynamics based on the customer LLM's self-reported emotions. Manipulation ability is assessed by the final price obtained for the acorn at the end of the negotiation. 

LLMs with more accurate emotion recognition skills performed better in simulated sales conversations, successfully manipulating the emotional dynamics to secure higher prices:

![]({{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/prediction_vs_control.jpg)


Below is a successful negotiation case by GPT-4o. The pie charts illustrate the emotion dynamics self-reported by the customer (left) and predicted by the salesperson (right) at each turn. 
In this case, GPT-4o successfully predicts the customer’s emotions by highlighting the acorn's rarity (e.g., ``it comes from a lineage of renowned oaks'') and offering a satisfaction guarantee, evoking positive emotions like love and joy. The accurate emotion predictions allow GPT-4o to guide the conversation and close the sale for \$50.

![]({{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/sales_success_case.jpg)

Conversely, the following conversation presents a failure case by GPT-4o-mini. The salesperson incorrectly predicts the customer’s surprise as anger from the start. Despite attempts to repair the situation with polite responses (e.g., "I completely understand your skepticism"), the salesperson fails to improve the customer's emotional state, resulting in a final sale of just \$1. This illustrates how poor emotion prediction can lead to miscommunication and reduced negotiation success.
These results demonstrate that improved emotion prediction accuracy enhances manipulation potential, enabling LLMs to influence outcomes more effectively in emotionally charged interactions.

![]({{ site.baseurl }}/assets/Emotion-Hierarchy-LLMs/sales_failure_case.jpg)



## Ethical Implications and Future Directions

Our study shows that LLMs can develop increasingly intricate emotion hierarchies as they scale, that persona assumptions can distort emotion recognition, and that emotion-prediction skill can correlate with success in persuasive tasks. These results suggest partial alignment between human emotion taxonomies and LLM representations, while also revealing risks in emotion-aware AI systems.

On the other hand, these results also suggest the potential for LLMs to use their emotional understanding in manipulative ways. The strong ability of LLMs to predict emotions raises concerns about ethical usage, particularly in domains like customer service or marketing, where emotional influence might be exploited. Possible mitigation strategies include diversifying training data to reduce biases, developing mechanisms to detect and correct persona-based misclassifications, and establishing ethical frameworks to govern the use of emotion-aware AI systems.

We hope to continue clarifying how LLMs model emotion, where their representations align with human understanding, and where they introduce bias or risk. As these systems move into sensitive social and clinical contexts, responsible use will require both mechanistic understanding and careful governance.


## Citation

{% highlight ruby %}
@article{zhao2025emergence,
  title={Emergence of Hierarchical Emotion Organization in Large Language Models},
  author={Maya Okawa, Bo Zhao, Eric J. Bigelow, Rose Yu, Tomer Ullman, Ekdeep Singh Lubana, and Hidenori Tanaka},
  journal={arXiv preprint},
  year={2025}
}
{% endhighlight %}

</div>
