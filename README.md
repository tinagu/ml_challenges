### Model development / Training:
The script is to tune Liquidai/lfm2-1.2B(https://huggingface.co/LiquidAI/LFM2-1.2B) with given input
- the model size is relative small
- good performance benchmark in knowledge, mathematics, instruction following 
- suited for agentic tasks, RAG & multi-turn conversations.

The assumptions are
- model inputs are only text. There will be no image, audio, video or structured data. 
- the question is similar with the given input in that domain, not programming / knowledge-intensive task.

#### Model performance
- Bleu score:

|          | score    | precisions |
| :------- | :------: | -------: |
| After  | 22.986217   | [54.16894104803494, 35.706271609461226, 29.588731615104432, 26.950305224798644]  |
| Before  | 3.345871  | [23.253925284244723, 5.706521739130435, 1.7730496453900708, 0.6571741511500547]  |

- Rogue score:

|           | rouge1 | rouge2 | rougeL | rougeLsum |
| :------- | :------: | :-------: | :-------:| ------: |
| After    | 0.450514  | 0.291543  | 0.36179 | 0.369014 |
| Before  | 0.245440  | 0.046938  | 0.12602 | 0.153559 |

* Model Strength: The model accuracy/bleu/rogue scores increase after 3 epochs.
* Model Weakness: 
  - As the model card stated, the model might not perform good in knowledge-extensive or programming tasks.
  - I chunk the input length to be 2048 because the training is run in constrained computing resources, therefore, the model might not perform well when the answer is long.
* Potential improvement: 
  - identify reward functions & train with RL; 
  - several questions are same but they come with different answers; if that's expected, the next step can be investigation on how to train multiple answers to the same questions.