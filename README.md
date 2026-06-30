# Trabalho - Processamento de Sinais I

<div align="center">

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/CEFET-RJ_logo.svg/320px-CEFET-RJ_logo.svg.png" width="120" alt="CEFET/RJ Logo"/>

# 📡 Trabalho — Processamento de Sinais I
### Modelagem e Análise de Arranjos de Sensores (Antenas)

[![CEFET/RJ](https://img.shields.io/badge/CEFET%2FRJ-Engenharia-1F3864?style=for-the-badge&logo=academia)](https://www.cefet-rj.br)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org)
[![Google Colab](https://img.shields.io/badge/Google-Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)](https://colab.research.google.com)

</div>

---

## 📋 Sumário

- [Sobre o Trabalho](#-sobre-o-trabalho)
- [Fundamentação Teórica](#-fundamentação-teórica)
- [Geometrias de Arranjos](#-geometrias-de-arranjos-implementadas)
- [Principais Análises e Resultados](#-principais-análises-e-resultados)
- [Estrutura do Repositório](#-estrutura-do-repositório)
- [Como Executar](#-como-executar)
- [Dependências](#-dependências)
- [Equipe e Referências](#-equipe-e-referências)

---

## 📖 Sobre o Trabalho

Este projeto prático faz parte da disciplina de **Processamento de Sinais I**, ministrada pelo Prof. Rafael S. Chaves. O objetivo principal é introduzir conceitos fundamentais de processamento espacial de sinais, explorando o *trade-off* básico em projetos de arranjos de antenas/sensores.

Foram desenvolvidas simulações computacionais para:
- Modelar geometrias complexas de arranjos (ULA, UCA, UPA e Cilíndrico).
- Calcular o vetor diretor (*steering vector*) e interpretar diagramas de radiação (*beampatterns*).
- Implementar técnicas básicas de *Beamforming* (Delay-and-Sum).
- Analisar recepção de sinais (DoA), ganhos espaciais, robustez a interferências e diretividade em ambientes tridimensionais.

---

## 📐 Fundamentação Teórica

O projeto é embasado nos conceitos da teoria clássica de antenas e processamento de sinais espaciais (referência: *C. A. Balanis*):

* **Onda Plana e Número de Onda:** Uma frente de onda incide com número de onda $k = 2\pi / \lambda$. O processamento ganha capacidade diretiva baseada no atraso de fase geométrica que a onda sofre ao atingir cada sensor.
* **Vetor Diretor (Steering Vector):** Representa a resposta de fase do arranjo em relação a uma direção de chegada específica $(\theta, \phi)$.  
  $$a(\theta,\phi) = \left[ e^{-j k \mathbf{r}_1^T \mathbf{u}}, e^{-j k \mathbf{r}_2^T \mathbf{u}}, \dots, e^{-j k \mathbf{r}_M^T \mathbf{u}} \right]^T$$
* **Array Factor e Beampattern:** Ao aplicarmos um vetor de pesos $w$ (neste projeto, adotamos pesos uniformes inicialmente), o diagrama de radiação normalizado (em dB) revela os lóbulos principais e os indesejados lóbulos secundários (vulnerabilidades a ruído).

---

## 🌐 Geometrias de Arranjos Implementadas

As funções geradoras das malhas de coordenadas estão implementadas e estruturadas para suportar variações paramétricas de número de sensores e espaçamento:

1. **ULA (Linear Uniforme):** Arranjo 1D. Base para conceitos como resolução inversamente proporcional a $M$.
2. **UCA (Circular Uniforme):** Arranjo 2D. Garante varredura de azimute em 360°, quebrando a restrição linear.
3. **UPA (Planar Uniforme):** Matriz 2D. Permite controle preciso em azimute e elevação, além de espalhar a energia dos lóbulos secundários bidimensionalmente.
4. **Arranjo Cilíndrico Uniforme:** Disposição em 3D, unindo as vantagens de varredura azimutal do UCA com a resolução em elevação dos anéis empilhados.

---

## 🔬 Principais Análises e Resultados

Através dos experimentos realizados nos cadernos de simulação (`Gráficos_PROCSIN.ipynb`), validamos fenômenos físicos críticos na engenharia de antenas:

| Fenômeno | Conclusões Matemáticas e Práticas |
|----------|-----------------------------------|
| **Resolução Espacial (HPBW) vs Sensores ($M$)** | A Largura de Feixe de Meia Potência (HPBW) diminui linearmente com o aumento do número de elementos. Pular de $M=4$ para $M=8$ no ULA estreita o feixe principal, melhorando o ganho direcional e a rejeição ao ruído lateral. |
| **Espaçamento ($d$) e Grating Lobes** | Se $d < \lambda/2$, desperdiçamos diretividade (feixe muito largo). Contudo, se ultrapassarmos a distância de Nyquist espacial ($d > \lambda/2$, ex: $1.2\lambda$), formam-se **Grating Lobes** (cópias do lóbulo principal que geram falsos positivos de detecção). |
| **Beam Broadening no ULA** | Para ângulos inclinados da frente de onda (ex: $60^\circ$), o feixe perde o foco e alarga. Ocorre devido à redução da "abertura efetiva" que a onda "enxerga" quando incide de lado. |
| **Ambiguidade Cônica** | Devido à sua natureza linear, o ULA não consegue distinguir se um sinal provém "de cima" ou "de baixo", gerando um cone de incerteza no *beampattern 3D*. Geometrias distribuídas como UPA e UCA quebram essa ambiguidade. |
| **Transmissão Direcional e Desalinhamento** | O teste do enlace (ULA transmissor vs. ULA receptor) aponta o impacto fatal de erros de apontamento em feixes estreitos (alto *misalignment loss*). Quanto maior a diretividade, maior a chance do link cair por um simples desvio em $\theta_R$. |

---

## 👥 Equipe

<table>
  <tr>
    <td align="center">
      <b>Jean Raposo Soares de Jesus</b><br/>
    </td>
    <td align="center">
      <b>Rony Nassar Boukai Mouawad</b>
    </td>
    <td align="center">
      <b>Fabio Luiz Cocco Favre da Silva</b>
    </td>
  </tr>
</table>

---

## 📁 Estrutura do Repositório

Organização exigida para reprodutibilidade e documentação técnica:

```text
Trabalho-PROCSIN/
│
├── 📓 Gráficos_PROCSIN.ipynb       # Notebook principal com análises e visualizações
├── 📁 src/                         # Scripts modulares Python
│   ├── generate_ula.py             # Função p/ arranjo linear
│   ├── generate_uca.py             # Função p/ arranjo circular
│   ├── generate_upa.py             # Função p/ arranjo planar
│   ├── generate_ucya.py            # Função p/ arranjo cilíndrico
│   ├── steering_vector.py          # Cálculo do vetor diretor
│   └── beampattern.py              # Cálculo e plot do Array Factor
│
├── 📁 data/                        # Dados gerados, matrizes exportadas
├── 📄 Trabalho___2026_1.pdf        # Documento oficial do roteiro (Prof. Rafael S. Chaves)
├── 📄 artigo_tecnico.pdf           # Relatório final e artigo formatado
└── 📄 README.md                    # Documentação principal
