# Calibração TRI do banco WIRS

Trabalho de avaliação da disciplina **MAT02012 — Tópicos Avançados em Estatística IV**
(Teoria de Resposta ao Item), UFRGS, 2026/2. Prof. Fernando Hepp Pulgati.

## Objetivo

Definir, calibrar e descrever um traço latente a partir dos seis itens dicotômicos do
banco **WIRS** (*Workplace Industrial Relations Survey*, 1990), distribuído no pacote
[`ltm`](https://cran.r-project.org/package=ltm) do R.

## Conteúdo

| Arquivo | Descrição |
|---|---|
| `apresentacao.qmd` | Apresentação Quarto/revealjs (fonte, R + `knitr`) |
| `apresentacao.html` | Apresentação renderizada |
| `dados/WIRS.csv` | Banco de dados (1005 estabelecimentos × 6 itens, separador `;`) |
| `instrucoes.md` | Enunciado da tarefa |

## Como renderizar

```bash
quarto render apresentacao.qmd
```

Requisitos: R ≥ 4.3 com os pacotes `ltm`, `mirt`, `ggplot2`, `dplyr`, `tidyr`,
`patchwork`, `knitr` e `kableExtra`; Quarto ≥ 1.4.

```r
install.packages(c("ltm", "mirt", "ggplot2", "dplyr", "tidyr",
                   "patchwork", "knitr", "kableExtra"))
```

## Referências

- Bartholomew, D. (1998). Scaling unobservable constructs in social science.
  *Applied Statistics*, 47, 1–13.
- Bartholomew, D., Steele, F., Moustaki, I. & Galbraith, J. (2002).
  *The Analysis and Interpretation of Multivariate Data for Social Scientists*. Chapman & Hall.
- Rizopoulos, D. (2006). `ltm`: An R package for latent variable modeling and item
  response theory analyses. *Journal of Statistical Software*, 17(5), 1–25.
- Chalmers, R. P. (2012). `mirt`: A multidimensional item response theory package for
  the R environment. *Journal of Statistical Software*, 48(6), 1–29.
