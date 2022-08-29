# Portuguese T5 for Abstractive Summarization (PTT5 Summ)

The code will be released soon.

## Introduction
PTT5 Summ is a fine-tuned [PTT5](https://github.com/unicamp-dl/PTT5) model to perform Abstractive Summarization in Brazilian Portuguese texts. This model was fine-tuned on the datasets: [WikiLingua](https://github.com/esdurmus/Wikilingua), [XL-Sum](https://github.com/csebuetnlp/xl-sum), [TeMário](http://www.nilc.icmc.usp.br/nilc/download/NILCTR0706-MazieroEtAl(2).pdf) and [CSTNews](http://nilc.icmc.usp.br/CSTNews/login/?next=/CSTNews/).

For further information, please go to [PTT5 Summ repository](https://github.com/pedropaiola/ptt5-summ).

## Available models
| Model                                                                                                | Dataset used in fine-tuning| 
| :-:                                                                                                  | :-:                        | 
| [phpaiola/ptt5-base-summ-wikilingua](https://huggingface.co/phpaiola/ptt5-base-summ-wikilingua)      | WikiLingua |
| [phpaiola/ptt5-base-summ-xlsum](https://huggingface.co/phpaiola/ptt5-base-summ-xlsum)                | XL-Sum     |
| [phpaiola/ptt5-base-summ-temario](https://huggingface.co/phpaiola/ptt5-base-summ-temario)            | 1st phase: WikiLingua. 2nd phase: TeMario |
| [phpaiola/ptt5-base-summ-cstnews](https://huggingface.co/phpaiola/ptt5-base-summ-cstnews)            | 1st phase: WikiLingua. 2nd phase: CSTNews|

## Usage example
```python
# Tokenizer 
from transformers import T5Tokenizer

# PyTorch model 
from transformers import T5Model, T5ForConditionalGeneration

token_name = 'unicamp-dl/ptt5-base-portuguese-vocab'
model_name = 'phpaiola/ptt5-base-summ-xlsum'

tokenizer = T5Tokenizer.from_pretrained(token_name )
model_pt = T5ForConditionalGeneration.from_pretrained(model_name)

text = '''
“A tendência de queda da taxa de juros no Brasil é real, é visível”, disse Meirelles, que participou na capital americana de uma série de reuniões e encontros com banqueiros e investidores que aconteceram paralelamente às reuniões do Fundo Monetário Internacional (FMI) e do Banco Mundial (Bird) no fim de semana.
Para o presidente do BC, a atual política econômica do governo e a manutenção da taxa de inflação dentro da meta são fatores que garantem queda na taxa de juros a longo prazo.
“Mas é importante que nós não olhemos para isso apenas no curto prazo. Temos que olhar no médio e longo prazos”, disse Meirelles.
Para ele, o trabalho que o Banco Central tem feito para conter a inflação dentro da meta vai gerar queda gradual da taxa de juros.
BC do ano
Neste domingo, Meirelles participou da cerimônia de entrega do prêmio “Banco Central do ano”, oferecido pela revista The Banker à instituição que preside.
“Este é um sinal importante de reconhecimento do nosso trabalho, de que o Brasil está indo na direção correta”, disse ele.
Segundo Meirelles, o Banco Central do Brasil está sendo percebido como uma instituição comprometida com a meta de inflação.
“Isso tem um ganho importante, na medida em que os agentes formadores de preços começam a apostar que a inflação vai estar na meta, que isso é levado a sério no Brasil”, completou.
O presidente do Banco Central disse ainda que a crise política brasileira não foi um assunto de interesse prioritário dos investidores que encontrou no fim de semana.
'''

src_text = [text]
inputs = tokenizer.encode(text, max_length=512, truncation=True, return_tensors='pt')
summary_ids = model_pt.generate(inputs, max_length=256, min_length=32, num_beams=5, no_repeat_ngram_size=3, early_stopping=True)
summary = tokenizer.decode(summary_ids[0])
print(summary)
#<pad> O presidente do Banco Central, Henrique Meirelles, disse neste domingo, em Washington, que a taxa de juros no Brasil é real, mas que o Brasil está indo na direção correta.</s>

```

# Citation
Coming soon
