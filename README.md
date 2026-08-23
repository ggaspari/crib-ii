# CRIB-II — Calculadora de Risco Clínico Neonatal

Calculadora client-side (HTML/JS puro, sem dependências de build) para o
score CRIB-II (Clinical Risk Index for Babies II).

- Pontuação conforme Parry G, Tucker J, Tarnow-Mordi W; UK Neonatal Staffing
  Study Collaborative Group. CRIB II: an update of the Clinical Risk Index for
  Babies score. Lancet. 2003;361(9371):1789–91.
- Escore = pontos da tabela peso × idade gestacional (específica por sexo) +
  temperatura à admissão + excesso de base, variando de 0 a 27.
- Mortalidade prevista pela fórmula logística original (Logit = −6,476 + 0,45 ×
  CRIB-II).
- A tabela peso × IG foi transcrita diretamente da tabela de referência estática
  da calculadora da SFAR (sfar.org/scores2/crib22.php) — **não** do JavaScript
  interativo daquela página, que tem pelo menos dois defeitos:
  - Várias combinações de peso muito baixo com determinada idade gestacional
    (ex.: peso <751 g com IG=32 sem., <501 g com IG=29–31 sem.) não são
    cobertas por nenhuma faixa do código e o campo de pontos permanece zerado
    por padrão, subestimando o escore.
  - Um erro de copy-paste na função de cálculo feminino: a condição para peso
    ≥1251 g com IG=29 semanas checa e define as variáveis do formulário
    **masculino** por engano, então nunca é acionada durante o cálculo
    feminino — zerando indevidamente essa combinação, que está dentro da
    faixa normal da tabela.

  Esta calculadora evita ambos os defeitos calculando diretamente pela tabela
  publicada; combinações fora da tabela (células em branco na fonte original)
  são sinalizadas explicitamente como não calculáveis, em vez de zeradas.
- A idade gestacional é limitada a 22–32 semanas, faixa coberta pela tabela de
  referência original — o CRIB-II destina-se sobretudo a recém-nascidos de
  muito baixo peso/extremo prematuros.
- Três temas alternáveis (botão no cabeçalho, ciclo escuro → claro → alto contraste),
  com preferência salva no navegador. O alto contraste elimina tons de cinza do texto
  e das bordas (tudo preto/branco puro, com bordas mais grossas), pensado para telas
  ruins de terminal hospitalar e para baixa visão.

## Uso

Acesse **https://ggaspari.github.io/crib-ii/**.

Alternativamente, baixe o `index.html` e abra localmente na sua instituição
para acesso off-line — não requer servidor nem instalação.

## Calculadora relacionada

[SNAPPE-II](https://ggaspari.github.io/snappe-ii/) — mesma proposta (client-side,
sem dependências), para o score SNAPPE-II.

## Aviso

Ferramenta de apoio clínico. Não substitui julgamento médico nem validação
local. Não coleta, armazena ou transmite dados — todo cálculo ocorre
localmente no navegador.

## Licença

Distribuído sob a [licença MIT](LICENSE) — uso, cópia e modificação livres,
sem garantia de qualquer tipo (inclusive de adequação a uso clínico real).
