# Referências sobre o banco WIRS

Trabalhos que analisam os seis itens de consulta do WIRS (1990) com modelos de traço
latente, levantados em 12/10/2026. Busca feita em inglês e português: fora destas,
o WIRS só aparece como exemplo na documentação do `ltm`, e não foi encontrado trabalho em
português nem repositório/RPubs de terceiros.

| Arquivo | Referência | Analisa pressupostos? |
|---|---|---|
| `bartholomew-1998-scaling-unobservable-constructs.pdf` | Bartholomew (1998), *Applied Statistics* 47, 1–13 — seção 6.2 | Sim: independência local e dimensionalidade via resíduos nas margens |
| `rusch-mair-hatzinger-2013-psychometrics-with-r.pdf` | Rusch, Mair & Hatzinger (2013), WU Discussion Paper 2013/2 — seção 4 | Sim, a análise mais completa |
| `rusch-2017-imps-ex5-tri-nao-parametrica.html` | Rusch (2017), Exercício 5 do curso de TRI em R (IMPS 2017) | Sim: monotonicidade, não interseção, escalabilidade |
| `rusch-2017-imps-ex6-tri-multidimensional.html` | Rusch (2017), Exercício 6 (IMPS 2017) | Sim: dimensionalidade |
| `rizopoulos-2006-jss-ltm.pdf` | Rizopoulos (2006), *JSS* 17(5) | Não usa o WIRS; descreve `GoF.rasch`, `margins`, `unidimTest` |
| `ltm-1.2-0-manual-cran.pdf` | Manual do `ltm` 1.2-0 (CRAN) | `?WIRS` e exemplos com WIRS em `?ltm` |

## O que cada uma verifica

### Bartholomew (1998), seção 6.2

- **Ajuste global** do modelo logit-probit de 1 fator: G² = 269,4 e χ² = 264,2 com 32 g.l.
  O modelo é "decisivamente rejeitado".
- **Independência local e dimensionalidade** pelos resíduos (O − E)²/E nas margens de
  2 e 3 vias (o mesmo diagnóstico de `margins()` no `ltm`):
  - 1 fator: a maior discrepância é o par **itens 1 × 2** (Tabela 4). Menos firmas
    usam as duas formas do que o modelo prevê; mais firmas seguem a lógica "uma ou outra".
  - 2 fatores: χ² = 133,6 com 24 g.l. Todos os resíduos de 2 vias ficam ≤ 0,44, mas os
    de 3 vias falham em **todas as triplas que contêm o item 1**.
- Decisão: retira o item 1 ("contato informal, inerentemente impreciso") e reajusta
  o modelo de 2 fatores (G² = 35,1 com 13 g.l.).

### Rusch, Mair & Hatzinger (2013), seção 4: tutorial completo

1. **Rasch (`eRm::RM`)**: o T10 não paramétrico de Ponocny (invariância entre subgrupos
   cortados na mediana) e o Tpbis (discriminação do item 1 contra os itens 2–6) dão os
   dois p ≈ 0. Também `LRtest` + `plotGOF` e o mapa de infit (`plotPWmap`).
2. **2PL e 3PL (`ltm`, `tpm`)**: os TRV favorecem o 3PL (Rasch → 2PL: 178,4 com 5 g.l.;
   2PL → 3PL: 26,3 com 6 g.l.). Mesmo assim, `item.fit(threePL)` rejeita todos os itens.
   O 3PL dá a₂ = 23,2 e a₄ = 15,1, um provável artefato de separação.
3. **Mokken (`mokken`)**, usado como condição necessária para a TRI paramétrica:
   - `coefH`: H = 0,154, abaixo de "fraco". H_ij negativos entre os itens 1, 2 e 4, e
     nenhum H_i ≥ 0,3. Conclusão dos autores: unidimensionalidade e/ou independência local
     provavelmente violadas.
   - `check.monotonicity`: o item 1 viola a monotonicidade.
   - `check.restscore`, `check.pmatrix` e `check.iio` (não interseção, ordenação invariante
     dos itens): muitas violações, sempre envolvendo o item 1.
   - Kernel smoothing (`KernSmoothIRT::ksIRT`): CCI do item 1 claramente não monótona.
4. **Dimensionalidade (`aisp`, algoritmo genético)**: item 1 não escalável; escalas
   {3, 5, 6} e {2, 4}.
5. **3PL bidimensional (`mirt`)** nos itens 2–6: ajuste bom. Uma dimensão é a consulta a
   grupos e comitês da empresa (2, 4); a outra é a consulta a sindicatos e comitês
   conjuntos (3, 5, 6). A consulta informal individual (item 1) "é uma classe à parte".

### Rusch (2017), exercícios IMPS 2017

Mesma linha do artigo acima, com código e saídas completas:
- **Ex. 5**: 4PL unidimensional no `mirt` (S-X² rejeita os 6 itens, também após FDR) e o
  mesmo Mokken (`check.restscore`, `check.pmatrix`, `check.monotonicity`, `coefH`). Depois,
  modelo spline (`itemtype="spline"`) e kernel smoothing: o item 1 tem CCI de ponto ideal.
- **Ex. 6**: dimensionalidade por PCA do espaço dos itens (`ksIRT`) e `aisp`. Modelos de
  2 fatores 2PL/3PL/4PL nos itens 2–6 (o 3PL vence: G² = 21,4 com 12 g.l., RMSEA 0,028).
  Depois, modelos confirmatórios com o item 1 em especificação de ponto ideal ou nominal,
  comparados por `M2()`, e modelos com efeito não linear do traço.

## Citada, mas sem PDF aberto

- Rizopoulos, D. & Moustaki, I. (2008). Generalized latent variable models with
  non-linear effects. *British Journal of Mathematical and Statistical Psychology*, 61,
  415–438. É a base de `ltm(WIRS ~ z1 * z2)`. Página: <https://researchonline.lse.ac.uk/id/eprint/5421>.
- Bartholomew, D., Steele, F., Moustaki, I. & Galbraith, J. (2002). *The Analysis and
  Interpretation of Multivariate Data for Social Scientists*. Chapman & Hall.

## Fontes online

- Rusch et al. (2013): <https://doi.org/10.57938/5763adfe-df36-4de9-8bb6-6979991d0424>
- Exercícios: <https://statmath.wu.ac.at/people/trusch/IMPS2017/Exercises/solutions/>
- Rizopoulos (2006): <https://www.jstatsoft.org/article/view/v017i05>
- Manual `ltm`: <https://cran.r-project.org/package=ltm>
