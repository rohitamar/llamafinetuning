# Finetuning LLMs for Sentiment Analysis

This repo contains several notebooks, documenting my explorations in running and finetuning large language models. To get a feel for these models, first, I finetuned GPT2 on the Stanford Sentiment Treebank dataset. Then, the goal was to use a more recently made LLM and finetune it on either a personal dataset or publicly available dataset. I didn't really have any good, concrete ideas for a personal dataset, and so I resorted to trying different datasets on Huggingface. 

I tried ministral/mistral-3b-instruct, Llama2-3b-hf, and Qwen3-7b on datasets: [tatsu-lab/alpaca](https://huggingface.co/datasets/tatsu-lab/alpaca) and [domenicrosati/TruthfulQA](https://huggingface.co/datasets/domenicrosati/TruthfulQA) Training these two datasets (separately) on all three of those models didn't do much. It slightly reduced hallucinations, but for the most part, responses were not coherent and accurate. Hence, I just used SST2 again and used Qwen2-0.5B-Instruct. 

I trained GPT2 on a GCP VM. Unfortunately, I couldn't use the VM for any of the other models that I mentioned (including Qwen2-0.5B-Instruct) due to an [version incompatibility issue between PyTorch and HuggingFace](https://github.com/huggingface/transformers/pull/38328). Hence, for Qwen2-0.5B-Instruct, I only used 2000 samples to train the model. It still beat GPT2 by 1% on the validation dataset even though GPT2 was trained on nearly 32 times more data. 

Here's the Qwen's training loss curve:<br>
![Qwen training loss curve](https://github.com/rohitamar/llamafinetuning/blob/main/images/graph.png)
