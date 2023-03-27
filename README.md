<p align="center" width="100%">
<img src="assets/alpaca_sv.png" alt="Swedish Alpaca" style="width: 20%; min-width: 400px; display: block; margin: auto;">
</p>


# Alpaca-LoRA-sv
Code and dataset for training a swedish finetuned instruction LLaMA

This repository contains code for training a swedish Alpaca model and striving to reproduce the [Stanford Alpaca](https://github.com/tatsu-lab/stanford_alpaca) results using [low-rank adaptation (LoRA)](https://arxiv.org/pdf/2106.09685.pdf).

This work is based on the [Alpaca Lora repository](https://github.com/tloen/alpaca-lora) by @tloen 

We translated the [alpaca_data_cleaned.json](https://github.com/tloen/alpaca-lora/blob/main/alpaca_data_cleaned.json) to swedish using ChatGPT. The translated json file is available in the data folder.

### Setup

1. Install dependencies

```
pip install -r requirements.txt
```

2. If bitsandbytes doesn't work, [install it from source.](https://github.com/TimDettmers/bitsandbytes/blob/main/compile_from_source.md). Please see the troubleshooting section below for additional suggestions. 

### Training (`finetune.py`)

Example usage for training on Stanford Alpaca instructions translated to swedish:

```bash
python finetune.py \
    --base_model 'decapoda-research/llama-7b-hf' \
    --data_path 'data/alpaca_sv_data_cleaned.json'
```

Example usage for training on swedish summarization dataset with a total prompt maxlength of 1500 tokens:

python finetune.py \
    --base_model 'decapoda-research/llama-7b-hf' \
    --data_path 'data/sv_data_summaries.json' \
    --cutoff_len=1500

## Example outputs

```
Instruction: "Varför kan det vara bra att vila sig i form före en löpartävling?"

Response: "Att vila sig i form före en löpartävling kan vara avgörande för att 
säkerställa en framgångsrik prestation. Att vila sig i form kan hjälpa till att 
förbättra konditionen, öka energinivåerna och minska risken för skador."
```

```
Instruction: "Skriv en berättelse om en hund som heter Ida"

Response: "Det var en gång en hund som hette Ida. Hon var en liten och vänlig hund 
som älskade att leka med sina vänner. En dag bestämde hon sig för att utforska världen 
utanför sin trädgård och upptäckte att det fanns mycket att upptäcka. 
Hon upptäckte nya platser, möter nya människor och gjorde nya vänner. 
Hon upptäckte att det fanns mycket att upptäcka i världen utanför hennes trädgård."
```



```
Instruction: "Ge 5 tips för hur man återhämtar sig efter en 40-årsfest"

Response: "1. Återgå till din vanliga rutin så snart som möjligt.
2. Ta dig tid att sova och vila ordentligt.
3. Ta dig tid att äta hälsosamma maträtter och dricka vatten.
4. Ta dig tid att göra någon form av fysisk aktivitet.
5. Se till att hålla kontakten med dina vänner och familj."
```

```
Instruction: "Vad krävs för att arbeta som Data Scientist?"

Response: "För att arbeta som Data Scientist krävs vanligtvis en kandidatexamen 
eller masterexamen i datavetenskap, matematik, statistik eller en liknande ämne. 
Dessutom krävs vanligtvis flera års erfarenhet inom datavetenskap och programmering."
```

```
Instruction: "Skriv en text om VMs historia"

Response: "Världsmästerskapet i fotboll är en internationell fotbollsturnering som 
arrangeras av Fifa och spelas vartannat år sedan 1930. Turneringen är en av de mest 
populära sportevenemangen i världen och lockar miljontals tittare från hela världen."
```




### Troubleshooting

#### undefined symbol: cget_col_row_stats / 8-bit not working / libsbitsandbytes_cpu.so not found

cp libbitsandbytes_cuda117.so libbitsandbytes_cpu.so

