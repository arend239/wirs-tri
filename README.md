# Calibração TRI do banco WIRS

Trabalho de avaliação da disciplina **MAT02012 — Tópicos Avançados em Estatística IV**
(Teoria de Resposta ao Item), UFRGS, 2026/2. Prof. Stela.

## Objetivo

Definir, calibrar e descrever um traço latente a partir dos seis itens dicotômicos do
banco **WIRS** (*Workplace Industrial Relations Survey*, 1990), distribuído no pacote
[`ltm`](https://cran.r-project.org/package=ltm) do R.

## Conteúdo

| Arquivo | Descrição |
|---|---|
| `apresentacao3.qmd` / `.html` | **Versão atual**: apresentação de até 20 min, com validação cruzada na escolha do modelo |
| `apresentacao2.qmd` / `.html` | Versão anterior de até 20 min |
| `apresentacao.qmd` / `.html` | Primeira versão, completa |
| `roteiro.md` | Roteiro de fala da `apresentacao3`, em duas partes (slides 1–14 e 15–23), com tempos e perguntas prováveis |
| `roteiro-parte2.html` | Parte 2 do roteiro em página visual, com as figuras e tabelas de cada slide |
| `dados/WIRS.csv` | Banco de dados (1005 estabelecimentos × 6 itens, separador `;`) |
| `dados/wirs_theta.csv` | θ estimados (EAP) e erros-padrão, gerados ao renderizar a apresentação |
| `instrucoes.md` | Enunciado da tarefa |
| `referencias/` | Artigos e exercícios que analisam o WIRS, incluindo Bartholomew (1998), o artigo-fonte; índice e resumo dos pressupostos verificados em `referencias/README.md` |

## Como renderizar

```bash
quarto render apresentacao3.qmd
```

Requisitos: R ≥ 4.3 com os pacotes `ltm`, `mirt`, `polycor`, `ggplot2`, `dplyr`, `tidyr`,
`patchwork`, `knitr` e `kableExtra`; Quarto ≥ 1.4.

```r
install.packages(c("ltm", "mirt", "polycor", "ggplot2", "dplyr", "tidyr",
                   "patchwork", "knitr", "kableExtra"))
```

## Referências

- Bartholomew, D. (1998). Scaling unobservable constructs in social science.
  *Applied Statistics*, 47, 1–13. (PDF em `referencias/`; a Tabela 1 do artigo é a
  distribuição de padrões de resposta reproduzida na apresentação.)
- Bartholomew, D., Steele, F., Moustaki, I. & Galbraith, J. (2002).
  *The Analysis and Interpretation of Multivariate Data for Social Scientists*. Chapman & Hall.
- Rizopoulos, D. (2006). `ltm`: An R package for latent variable modeling and item
  response theory analyses. *Journal of Statistical Software*, 17(5), 1–25.
- Rusch, T., Mair, P. & Hatzinger, R. (2013). *Psychometrics with R: A review of CRAN
  packages for item response theory*. Discussion Paper 2013/2, WU Wien.
  (Tutorial completo com o WIRS; PDF em `referencias/`.)
- Chalmers, R. P. (2012). `mirt`: A multidimensional item response theory package for
  the R environment. *Journal of Statistical Software*, 48(6), 1–29.
