# Roteiro — `apresentacao3` (TRI, banco WIRS)

Apresentação de **no máximo 20 min**, com 23 slides. O roteiro mira **≈ 19:15** (≈ 17,5 min
de fala, mais as transições) e deixa 45 s de folga para imprevistos. As falas foram escritas
para ser ditas em ritmo normal (≈ 130 palavras por minuto). Não precisam ser decoradas
palavra por palavra, mas os **números citados batem com os slides** e devem ser mantidos.

O roteiro está em duas partes: a **Parte 1** vai até o slide 14 (validação cruzada) e a
**Parte 2** vai do slide 15 ao fim. A Parte 2 também está em `roteiro-parte2.html`, com o
gráfico ou a tabela de cada slide e os pontos principais destacados.

| Parte | Bloco | Slides | Tempo | Acumulado |
|---|---|---|---|---|
| 1 | Contexto, padrões, traço latente e modelos | 1–5 | 3:20 | 3:20 |
| 1 | Pressupostos e escolha dos itens | 6–9 | 4:45 | 8:05 |
| 1 | Calibração e escolha do modelo (com validação cruzada) | 10–14 | 4:25 | 12:30 |
| 2 | Parâmetros e informação | 15–16 | 1:45 | 14:15 |
| 2 | Estimação, descrição do traço e conclusões | 17–23 | 5:00 | 19:15 |

**Pontos de controle do tempo:** fim do slide 9 em ≈ 8:05; fim do slide 14 em ≈ 12:30;
fim do slide 20 em ≈ 17:00. Se estiver atrasado, os slides que aceitam versão curta (uma
frase) são o 16 (informação) e o 19 (distribuição).

O número do slide é o que aparece no canto inferior direito da apresentação (título = 1).
Os slides de seção (10 e 17) contam na numeração.

---

## Parte 1 — slides 1 a 14

### Slide 1 · Título · 0:20

> Bom dia. Somos o Giovanni e o João, e vamos apresentar a calibração de um traço latente
> a partir do banco WIRS, com Teoria de Resposta ao Item: pressupostos, escolha do modelo,
> estimação e descrição do traço.

### Slide 2 · O banco WIRS e os seis itens · 0:50

> O WIRS é um levantamento britânico de 1990 sobre relações de trabalho. A pergunta foi
> feita ao gestor de cada estabelecimento: na mudança mais recente envolvendo novas
> máquinas, houve consulta aos trabalhadores por algum destes canais?
>
> Cada canal é um item, que vale 1 se foi usado, do mais direto, a conversa individual
> (I1), ao mais formal, chamar dirigentes sindicais de fora (I6). Reunião de grupo é o mais
> comum, com 58%, e dirigentes externos o menos, com 15%. O recorte do pacote `ltm` tem
> 1005 estabelecimentos, trabalhadores não manuais, sem dados faltantes.

### Slide 3 · Os padrões de resposta · 0:40

> Cada linha é um padrão de resposta, com os seis dígitos na ordem I1 a I6. Dos 64
> possíveis aparecem 57, mas a amostra se concentra em poucos. Os quatro em vermelho somam
> 42%: só reunião de grupo, o mais comum, com 172; nenhum canal, com 132; só conversa
> individual, 65; e as duas sem outro canal, 55. Repare que nesses quatro nenhum canal
> coletivo foi usado: esses 42% vão reaparecer como o piso da escala.

### Slide 4 · O traço latente · 0:25

> O traço que queremos estimar é o **grau de institucionalização da consulta aos
> trabalhadores** diante de uma mudança tecnológica. Com θ baixo está o estabelecimento
> que, quando consulta, faz isso por canais diretos e informais; com θ alto, o que aciona
> estruturas coletivas, como comitês e sindicatos.

### Slide 5 · Modelos candidatos e pressupostos · 1:05

> Os candidatos são os modelos logísticos para itens dicotômicos. Na fórmula geral, a do
> 3PL, *b* diz onde a curva está, *a* o quanto ela é íngreme e *c* é o piso. Aqui, *c* não é
> "acerto ao acaso", mas a chance de usar o canal mesmo com θ muito baixo. No `ltm`, D = 1.
>
> Restringindo parâmetros, temos uma sequência: o 1PL, com um único *a* comum a todos os
> itens; o 2PL, com um *a* por item; e o 3PL. Cada um é caso particular do seguinte, o que
> permite compará-los por razão de verossimilhança.
>
> Antes de calibrar, verificamos três pressupostos: **unidimensionalidade**, um único θ
> explica a associação entre os itens; **independência local**, dado θ, um item não informa
> sobre outro; e **monotonicidade**, a probabilidade de usar o canal cresce com θ.

### Slide 6 · Pressuposto 1 — unidimensionalidade · 1:15

> À esquerda estão as correlações tetracóricas, a medida de associação adequada para
> itens binários. Se um único traço explicasse tudo, todas seriam positivas. Não é o que
> acontece: I1 é negativa com I2 e com I4, e I2 quase não se associa a I3, I5 e I6.
>
> Na tabela estão os autovalores da matriz tetracórica, como na aula 2. Com os seis itens,
> dois passam de 1; sem I1, o segundo ainda fica no limite, em 1,02. Por isso, a última
> coluna traz a análise paralela do `ltm`, a função `unidimTest`: ela simula 200 bancos com
> um único traço e verifica se o segundo autovalor observado é maior do que o acaso
> produziria.
>
> O resultado é um funil. Com os seis itens, p ≤ 0,005; sem I1, ainda p = 0,015; só com
> I3 a I6 o p sobe para 0,67, e não há evidência de uma segunda dimensão.

### Slide 7 · Pressuposto 2 — independência local · 1:15

> Para a independência local, ajustamos o modelo de um traço e comparamos, para cada par
> de itens, a tabela 2×2 observada com a que o modelo prevê. À esquerda está o caso mais
> gritante, I1 com I2. Só 142 estabelecimentos usaram conversa individual e reunião de
> grupo ao mesmo tempo, e o modelo esperava 222. Ou seja, quem usa um canal tende a não
> usar o outro: é uma escolha entre canais, e não mais ou menos do mesmo traço.
>
> À direita está o resíduo (O − E)²/E de cada casela, calculado pela função `margins` do
> `ltm`, com a regra prática de 3,5. Com os seis itens, o par I1–I2 chega a 41,5 e 13 das
> 20 triplas passam da regra. Tirando I1, ainda sobra o par I2–I4, com 6,7. Só no conjunto
> I3 a I6 nenhum par e nenhuma tripla passa de 3,5.

### Slide 8 · Pressuposto 3 — monotonicidade · 1:25

> Antes de calibrar, aproximamos θ pelo número de **outros** canais usados e olhamos a
> proporção de uso de cada item à medida que esse número cresce. Num modelo acumulativo,
> como os da aula 1, essa curva precisa subir.
>
> I1, em vermelho, sobe até 50% e depois cai para 21%: quem mais institucionaliza volta a
> não usar a conversa individual. É um padrão de ponto ideal, que um modelo acumulativo não
> representa. I2, em laranja, é quase plana, em torno de 58%, quando a contagem inclui I1;
> sem I1 ela sobe, mas com discriminação baixa. I3 a I6 sobem.

**[clique na aba "Saída do `descript()`"]**

> A saída do `descript`, do script da aula, confirma. A correlação ponto-bisserial de cada
> item com os demais é −0,07 para I1 e 0,02 para I2, contra 0,26 a 0,40 nos demais. E o α
> de Cronbach, que é 0,41 com os seis itens, só aumenta quando se retira I1 (0,53) ou I2
> (0,48); retirar qualquer canal coletivo o reduz.

### Slide 9 · Decisão: o traço é medido por I3–I6 · 0:50

> Juntando tudo na tabela: com os seis itens, os três pressupostos falham. Sem I1, a
> monotonicidade passa, mas a unidimensionalidade e a independência local continuam
> violadas, sobretudo pelo par I2–I4. Com I3 a I6, nenhum dos três mostra violação.
>
> E isso faz sentido no contexto: I1 e I2 são canais diretos, sem representação dos
> trabalhadores. Quem usa um tende a não usar o outro, e eles se associam pouco aos
> canais coletivos. Então o traço é medido pelos quatro canais coletivos: comitê
> permanente, comitê ad hoc, sindicato interno e sindicato externo.

### Slide 10 · Seção "Calibração dos itens I3–I6" · 0:05

> Vamos agora calibrar esses quatro itens.

### Slide 11 · Três modelos encaixados · 0:55

> Ajustamos os três modelos no `ltm`, com as funções do script da aula: `rasch` para o
> 1PL, `ltm` para o 2PL e `tpm` para o 3PL, todos por máxima verossimilhança marginal.
> Como cada modelo é caso particular do seguinte, a tabela traz AIC, BIC e o TRV contra o
> anterior. Os critérios não concordam: o BIC é menor no 1PL e o AIC é menor no 3PL.
>
> À direita estão os pisos que o 3PL estimou. O *c* fica praticamente em zero em I3, I5 e
> I6. Só o comitê ad hoc, I4, tem piso, de 16%, e repare no erro-padrão da sua
> discriminação: 19,8, para uma estimativa de 7,8.

### Slide 12 · Qual modelo escolher? · 1:10

> Primeiro, o BIC favorece o 1PL. Mas o TRV rejeita a discriminação comum, com p = 0,002,
> e no 2PL o *a* vai de 0,98 a 1,97. Além disso, o 1PL deixa 3 das 4 triplas de itens com
> resíduo acima de 3,5: ele não reproduz bem as associações.
>
> Segundo, o TRV e o AIC favorecem o 3PL. Mas, como vimos, só I4 ganha piso, de 0,16, e o
> seu *a* fica indeterminado: 7,8 com erro-padrão de 19,8. E, mesmo sem essa instabilidade,
> o TRV contra o 3PL não segue a qui-quadrado usual: como *c* ≥ 0, a hipótese *c* = 0 está
> na fronteira do espaço paramétrico, como mostram Brown, Templin e Cohen, de 2015.
>
> Por isso o 2PL parece o preferível, mas até aqui sem uma justificativa sólida. Para
> sustentar a escolha, usamos validação cruzada.

### Slide 13 · Apoiando a escolha por validação cruzada (3PL) · 1:05

> Primeiro, a estabilidade do 3PL. Dividimos os 1005 estabelecimentos em 10 partes,
> ajustamos o modelo com nove delas e repetimos o sorteio 10 vezes: são 100 ajustes. Em
> cada um, guardamos a maior discriminação estimada.
>
> O histograma mostra essas discriminações em escala log, e a linha vermelha é o corte que
> adotamos, 10. Em 35% dos ajustes o 3PL passou desse corte, e em 86% passou de 5. Nenhum
> ajuste deixou de convergir e nenhum piso passou de 0,5: o problema é só a discriminação,
> e em 94% desses casos é a de I4. É o que o ajuste completo já mostrava, um *a* de 7,8 com
> erro-padrão de 19,8 e pisos perto de zero nos outros itens. Com base nessa instabilidade,
> descartamos o 3PL.

### Slide 14 · Apoiando a escolha por validação cruzada (1PL × 2PL) · 1:10

> Entre o 1PL e o 2PL, a pergunta é qual prevê melhor dados que não foram usados no
> ajuste. Nas mesmas 100 divisões, cada modelo é ajustado com nove partes e avaliado na
> probabilidade que dá ao padrão de resposta de cada estabelecimento da parte de fora. O
> log-loss é menos o log dessa probabilidade, e o Brier, o erro quadrático; nos dois,
> menor é melhor.
>
> O 2PL tem log-loss e Brier um pouco menores: os três parâmetros a mais não são
> sobreajuste. Mas a diferença é pequena: o teste de Nadeau–Bengio, um teste t corrigido
> para a sobreposição entre os folds, dá p = 0,335.
>
> A decisão, então: adotamos o 2PL, porque o TRV rejeita discriminações iguais, a
> validação cruzada não indica sobreajuste e o 3PL é instável com 4 itens. O 1PL, porém,
> também seria uma escolha razoável.

**[passagem para a Parte 2]**

---

## Parte 2 — slides 15 a 23

*Material visual desta parte, com os gráficos e tabelas de cada slide:
`roteiro-parte2.html`.*

### Slide 15 · Parâmetros calibrados (2PL) · 1:00

> Estes são os parâmetros do 2PL, ordenados pela dificuldade. O *b* é o valor de θ em que
> a probabilidade de usar o canal é 50%: são os pontos no gráfico. Todos os *b* são
> positivos: um estabelecimento médio, com θ = 0, usa cada canal coletivo com
> probabilidade entre 9% e 28%.
>
> Pela dificuldade, a ordem é sindicato interno, comitê permanente, comitê ad hoc e, por
> último, dirigentes sindicais externos, o canal mais "caro".
>
> O *a* é a inclinação. Sindicato interno e comitê permanente, com *a* perto de 2, são os
> que melhor separam estabelecimentos de baixa e alta institucionalização. O comitê ad hoc,
> com *a* perto de 1, é o menos discriminativo, e é o item que mostrou piso no 3PL.

### Slide 16 · Informação e precisão da escala · 0:45

> Como na aula 2, a informação do item é *a*²·P·(1 − P), e a do teste é a soma. À esquerda,
> sindicato interno e comitê permanente dominam, porque têm os maiores *a*. À direita estão
> a informação do teste, com máximo em θ = 0,71, e o erro-padrão, que é 1 sobre a raiz da
> informação.
>
> Pela função `information`, 80% da informação está acima de θ = 0. A escala distingue bem
> estabelecimentos de institucionalização média e alta, e mal os da parte baixa, onde o
> erro cresce rapidamente.

*Versão curta, se estiver atrasado:* "80% da informação está acima de θ = 0: a escala
mede bem a parte média e alta do traço e mal a parte baixa."

### Slide 17 · Seção "Estimação do traço latente" · 0:05

> Agora, a estimação do traço.

### Slide 18 · Estimação por EAP · 0:55

> Estimamos θ por EAP, a média a posteriori da aula 5. O motivo é prático: 424
> estabelecimentos, 42%, não usaram nenhum dos quatro canais, e 40 usaram todos. Nesses
> padrões a máxima verossimilhança vai a menos ou a mais infinito. O EAP combina a
> verossimilhança com a priori normal padrão, é finito para todo padrão e traz o
> desvio-padrão a posteriori como erro-padrão. O padrão do `factor.scores` no script da
> aula, o EB, que é a moda a posteriori, dá praticamente o mesmo resultado.
>
> Um detalhe importante: com quatro itens binários há só 16 padrões possíveis, então o θ
> estimado assume só 16 valores.

### Slide 19 · Distribuição do traço estimado · 0:45

> A média dos θ estimados é praticamente zero, como esperado, porque a escala foi fixada
> com θ ~ N(0, 1), e o desvio-padrão é 0,73. A distribuição é assimétrica à direita: 42%
> estão no piso, em −0,70, a mediana é −0,21 e a cauda vai até 1,72, que são os 40
> estabelecimentos com os quatro canais.
>
> Embaixo estão os itens na mesma escala; é o mapa item–pessoa. Todos os itens ficam acima
> da maior parte dos estabelecimentos: na prática, a escala separa bem quem
> institucionaliza a consulta.

*Versão curta:* "A distribuição é assimétrica à direita, com 42% no piso, e todos os
itens ficam acima da maior parte dos estabelecimentos."

### Slide 20 · Precisão de cada estimativa · 1:00

> O gráfico mostra, para cada um dos 16 padrões, θ estimado mais ou menos dois
> erros-padrão. O erro vai de 0,59 a 0,75, grande para uma escala de desvio-padrão 1, e os
> intervalos se sobrepõem bastante.
>
> A confiabilidade empírica, a variância dos θ estimados sobre a variância total, é 0,54.
> É baixa: as referências usuais são 0,70 em pesquisa e 0,90 para decisões individuais. O
> desvio-padrão dos θ estimados, 0,73, menor que 1, é o encolhimento do EAP: cada
> estimativa é puxada para a média da a priori.
>
> Na prática, a escala serve para comparar médias de grupos de estabelecimentos, em que o
> erro se dilui, e não para classificar um estabelecimento isolado.

### Slide 21 · Descrição do traço estimado · 1:05

> Agrupamos os estabelecimentos pelo número de canais coletivos usados, com θ na escala
> 50 ± 10, só para evitar números negativos.
>
> 42% não acionaram nenhuma estrutura coletiva e ficam em 43 pontos: 292 consultaram só por
> canais diretos e 132 por nenhum canal. É o polo baixo que definimos no início. 30% usaram
> um canal, quase sempre o sindicato interno; 15% usaram dois; só 13% chegam a três ou
> quatro.
>
> O θ estimado ordena primeiro pelo número de canais (as faixas não se sobrepõem) e,
> dentro do mesmo número, pelo peso *a* de cada canal: só sindicato interno dá 52 pontos, e
> só comitê ad hoc dá 48. É o mesmo escore bruto com estimativas diferentes, como na aula
> 3, embora essa diferença fique dentro do erro-padrão.

### Slide 22 · Conclusões · 1:00

> Para concluir: o traço é o grau de institucionalização da consulta aos trabalhadores, e
> é medido pelos quatro canais coletivos, os únicos sem violação dos pressupostos. O
> modelo é o 2PL: vence o 1PL pelo TRV e pelo ajuste, e o 3PL só melhora I4, com um
> parâmetro que os dados não determinam. O traço estimado é assimétrico, com 42% no piso,
> e ordena os estabelecimentos pelo número e pelo peso dos canais coletivos.
>
> As limitações: confiabilidade baixa, de 0,54, e só 16 valores possíveis, então a escala
> serve para comparar grupos; pouca informação na parte baixa; o desvio em I4; itens e
> modelo escolhidos com os mesmos dados; e os canais diretos, que seguem outra lógica.

### Slide 23 · Obrigado · 0:10

> Obrigado. Ficamos à disposição para perguntas.

---

## Perguntas prováveis

Sugestão de quem responde: quem apresentou a **Parte 1** fica com dados, pressupostos e
escolha do modelo (P1–P9); quem apresentou a **Parte 2**, com parâmetros, estimação e
descrição (P10–P17).

### Parte 1 — dados, pressupostos e escolha do modelo

**P1. Por que não manter I2? Ele é o único canal "fácil" e cobriria a parte baixa da
escala.**
Ele não cobre. Com *a* = 0,42, a informação de I2 é no máximo *a*²/4 ≈ 0,04 em qualquer θ.
A confiabilidade fica igual (0,545 com I2 e 0,538 sem ele), e os θ estimados das duas
versões têm correlação de 0,99. Em troca, I2 traz a dependência local com I4 (resíduo 6,7)
e uma segunda dimensão na análise paralela. No 2PL de I2–I6, o padrão "nenhum canal" fica
com θ = −0,82 e o padrão "só reunião de grupo" com −0,59, uma diferença bem menor que o
erro-padrão de cada um (≈ 0,73–0,76).

**P2. O p da análise paralela depende da semente?**
Sim: é um p de Monte Carlo, com B = 200 bancos simulados, e o menor valor possível é
1/201 ≈ 0,005 (por isso "p ≤ 0,005"). Com outras sementes, I1–I6 fica sempre no mínimo
(o 2º autovalor observado, 1,13, nunca é alcançado pelos simulados, que não passam de
0,73). I2–I6 varia entre 0,01 e 0,05, sempre abaixo de 0,05 mas perto do limite; por isso,
para I2, o argumento principal é a dependência com I4 e o *a* baixo. I3–I6 fica entre 0,59
e 0,68.

**P3. De onde vem a regra de 3,5 para os resíduos?**
É a regra prática da documentação do `ltm` (Rizopoulos, 2006), que marca com `***` os
resíduos (O − E)²/E acima de 3,5. A ideia é a mesma das correlações residuais ≈ 0 da aula
2: o modelo deve reproduzir a associação entre pares (e triplas) de itens.

**P4. Por que correlação tetracórica e não Pearson?**
Com itens 0/1, a correlação de Pearson (phi) é limitada pelas proporções de cada item e
subestima a associação. A tetracórica estima a correlação entre as variáveis normais
latentes por trás das respostas, como na aula 2 (no script da aula, `psych::tetrachoric`;
aqui, `polycor`, que faz o mesmo cálculo).

**P5. Se o TRV e o AIC preferem o 3PL, por que não usá-lo?**
O ganho do 3PL é real, mas está todo em um item: *c* ≈ 0 em I3, I5 e I6, e só I4 ganha um
piso de 16% (EP 0,02). O problema é o *a* de I4, que os dados não determinam: 7,8 com EP
de 19,8 na partida padrão e 33,2 com outra partida, com a mesma log-verossimilhança
(−2079,3). A validação cruzada confirma: em 35% dos 100 ajustes a maior discriminação passa
de 10, e em 94% desses casos é a de I4. Testamos também um 2PL com piso só em I4: ele se
ajusta bem (G² com p = 0,56) e tem AIC e BIC menores que o 2PL, mas o *a* de I4 continua
indeterminado (EP ≈ 54), e a ordem dos θ estimados praticamente não muda (Spearman 0,999).
Como não dá para reportar um *a* calibrado para I4 nesse modelo, ficamos com o 2PL e
declaramos o piso como limitação.

**P6. O slide 12 diz que o TRV contra o 3PL "não segue a qui-quadrado". Então o p correto
favorece ou desfavorece o 3PL?**
Favorece. Com *c* ≥ 0, a hipótese *c* = 0 está na fronteira, e a distribuição do TRV sob
H₀ passa a ser uma mistura de qui-quadrados, com cauda mais leve que a qui-quadrado usual.
O p que reportamos (0,02) é, portanto, **conservador**: o correto seria ainda menor (Brown,
Templin e Cohen, 2015). Ou seja, esse ponto não é argumento contra o 3PL; ele só mostra que
o p do TRV não é exato. O que descarta o 3PL é a instabilidade do *a* de I4.

**P7. O BIC prefere o 1PL, e o slide 14 diz que ele é "uma escolha razoável". Então por
que não o 1PL?**
O 1PL não reproduz as associações: deixa 3 das 4 triplas com resíduo acima de 3,5, o teste
por bootstrap do próprio `ltm` (`GoF.rasch`) rejeita (p ≈ 0,005), e o TRV rejeita a
discriminação comum (p = 0,002). Mas a diferença **em magnitude** é pequena: na validação
cruzada o 2PL ganha só 0,0041 de log-loss por estabelecimento (p = 0,335). E as escalas
quase coincidem: no 1PL o θ estimado depende só do número de canais (5 valores possíveis);
no 2PL a ordem também é primeiro pelo número de canais e só desempata pelo *a* (slide 21).
A correlação entre os θ estimados dos dois modelos é 0,99. Por isso adotamos o 2PL, mas o
1PL é uma alternativa defensável.

**P8. O que é o teste de Nadeau–Bengio e por que não um teste t comum?**
Nas 100 divisões, os conjuntos de treino se sobrepõem (cada par compartilha boa parte dos
dados), então as 100 diferenças de log-loss não são independentes, e um teste t comum
subestimaria a variância. Nadeau e Bengio (2003) corrigem a variância pelo fator
(1/J + n_teste/n_treino) = (1/100 + 1/9), o que dá t = 0,97 com 99 gl e p = 0,335.

**P9. Um ganho de 0,0041 no log-loss não é desprezível? E o corte de discriminação em 10
não é arbitrário?**
O ganho é pequeno, mas é o esperado: o AIC antecipa um ganho fora da amostra de
(TRV − 2 × 3 parâmetros) / 2n = (15,06 − 6) / 2010 ≈ 0,0045 por estabelecimento, quase o
que observamos. Para ter escala, o log-loss dos dois modelos (≈ 2,08) está muito perto do
limite dado pelas próprias frequências observadas dos 16 padrões (2,07) e longe de um
modelo que desse a mesma probabilidade a todos (log 16 = 2,77). Quanto ao corte, ele é uma
decisão do analista, e por isso a tabela do slide 13 mostra outros valores (≥ 5: 86%;
≥ 20: 3%). O ponto não é o corte em si, mas a dispersão: de uma amostra para outra, a maior
discriminação do 3PL vai de cerca de 3,5 a mais de 20 (no 2PL, nenhum *a* passa de 2), o
que concorda com o EP de 19,8 no ajuste completo.

### Parte 2 — parâmetros, estimação e descrição

**P10. Então o 2PL se ajusta ou não?**
Quase. Ele reproduz todos os pares e triplas (maior resíduo de 2,71), e o `item.fit` do
`ltm` com p-valores de Monte Carlo não rejeita nenhum item (p entre 0,22 e 0,66). Mas o G²
contra o saturado dá 16,6 com 7 gl (p = 0,02), o mesmo valor publicado na análise
original do banco. O desvio vem de I4 (só comitê ad hoc: 83 observados contra 71
esperados; o S-X² do `mirt` para I4 também dá p = 0,01) e, em magnitude, é pequeno
(RMSEA calculado a partir do G² ≈ 0,04).

**P11. Por que EAP e não o padrão do `factor.scores` (EB)?**
Os dois são bayesianos (aula 5): o EB do `ltm` é a moda a posteriori (MAP), e o EAP é a
média. A correlação entre eles é > 0,999. Preferimos o EAP porque ele traz o desvio-padrão
a posteriori como erro-padrão e minimiza o erro quadrático médio a posteriori.

**P12. A curva de erro-padrão do slide 16 dá valores maiores que os EP do slide 20. Por
quê?**
A curva é 1/√I(θ), o erro-padrão **assintótico da máxima verossimilhança** (aula 2): em
θ = −0,70, por exemplo, I = 0,67 e EP = 1,22. O EP do EAP é o desvio-padrão a posteriori,
que incorpora a priori N(0, 1) e por isso é menor (0,75 nesse mesmo ponto). É o mesmo
encolhimento que faz DP(θ̂) = 0,73.

**P13. Por que a confiabilidade é igual a DP(θ̂)²?**
Para o EAP, Var(θ̂) + média(EP²) ≈ Var(θ) = 1 (lei da variância total). Então a
confiabilidade empírica Var(θ̂) / [Var(θ̂) + média(EP²)] ≈ Var(θ̂) = 0,73² ≈ 0,54: a parte
da variância do traço que os 4 itens capturam.

**P14. Se θ̂ ordena pelo número de canais, para que TRI? Bastaria somar.**
Com estes 4 itens, a ordem dos θ̂ é de fato a do escore bruto, que desempata só pelos
pesos *a*. Mas é a TRI que permite saber isso e dizer mais: ela verifica os pressupostos
(foi assim que descobrimos que I1 e I2 não medem o mesmo traço), dá o significado de cada
item na escala (*b* e *a*), quantifica a precisão de cada estimativa e onde a escala mede
bem (informação) e coloca os estabelecimentos numa métrica que não depende deste conjunto
específico de itens.

**P15. E DIF (aula 6), modelos politômicos (aula 4) ou CAT (aula 5)?**
O WIRS do `ltm` tem só os seis itens, sem variável de grupo, então não há grupo
focal/referência para testar DIF (os outros recortes da pesquisa, como trabalhadores
manuais, não vêm no pacote). Os itens são dicotômicos, então os modelos politômicos não se
aplicam. Um banco de 4 itens também é pequeno demais para um CAT.

**P16. Por que todos os *b* são positivos? A escala não deveria estar centrada?**
Quem fica centrado em zero é θ, por convenção (θ ~ N(0, 1) fixa a escala). Os *b* dizem
onde cada canal "liga", e todos ficam acima de zero porque nenhum canal coletivo é usado
pela maioria dos estabelecimentos: o mais comum, o sindicato interno, aparece em 36% da
amostra. É isso que deixa 42% no piso e concentra a informação acima de θ = 0.

**P17. Esse resultado bate com a literatura sobre o banco?**
Sim (Bartholomew, 1998). A análise original também descartou o item 1 e propôs os itens
3–6 como escala de "consulta formal". As discriminações do 2PL que obtivemos (1,78; 0,98;
1,97; 1,37) coincidem com as publicadas (1,77; 0,98; 1,97; 1,37), assim como o G² = 16,6
com 7 gl e os erros-padrão a posteriori de 0,59 a 0,75. A mesma fonte ajusta um modelo de
classes latentes aos 6 itens e precisa de 5 classes para um ajuste adequado; o traço
contínuo é preferível por parcimônia.
