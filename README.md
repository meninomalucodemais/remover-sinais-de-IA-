# remover-sinais-de-ia

Skill para o Claude que revisa ou reescreve textos em português do Brasil e tira deles os padrões típicos de texto gerado por IA.

## O que a skill faz

Você entrega um texto (ou pede um texto novo) e a skill orienta o Claude a encontrar os vícios de escrita mais comuns dos modelos de linguagem e corrigi-los. Ela trata clichês de abertura, ênfase inflada, tom de folheto, atribuições vagas, construções repetitivas como "não é X, é Y", formatação markdown fora de lugar e outros sinais listados mais abaixo.

Serve para quem escreve ou revisa texto com frequência e usa IA em alguma etapa:

- professores que preparam material de aula ou corrigem redações;
- estudantes revisando os próprios trabalhos;
- redatores e jornalistas;
- criadores de conteúdo para blogs, newsletters e redes sociais.

## Por que existe

Texto escrito com ajuda de IA costuma ser reconhecido rápido. As mesmas expressões aparecem em todo lugar ("desempenha um papel crucial", "vale ressaltar que", "no mundo acelerado de hoje"), os parágrafos têm o mesmo formato e quase nada é concreto.

Trocar palavras por sinônimos não resolve. Quase todo sinal de IA é sintoma de texto vazio: a frase afirma que algo é importante em vez de mostrar por quê. Por isso a skill troca o enfeite por informação específica, como um nome, um número, uma data, uma fonte ou um exemplo. Quando não existe fato para colocar no lugar, a frase sai.

## Como funciona

1. Entende o contexto: gênero do texto (e-mail, artigo, aula, post, redação), público, registro e voz do autor. Se houver uma amostra escrita pelo próprio autor, imita o ritmo, o vocabulário e a pontuação dela.
2. Audita o texto contra as 12 categorias de sinais e anota cada ocorrência.
3. Reescreve corrigindo a causa, que geralmente é falta de conteúdo, e não só a superfície.
4. Faz uma segunda auditoria no resultado para conferir que a reescrita não trocou um padrão por outro (sair "crucial" e entrar "fundamental" não adianta).
5. Entrega o texto limpo. A lista do que mudou só vem se você pedir.

## As 12 categorias de sinais

| # | Categoria | Exemplos | Correção |
|---|-----------|----------|----------|
| 1 | Ênfase inflada em importância | "desempenha um papel crucial", "marco", "legado duradouro" | Trocar por fato verificável: o que mudou, quando e para quem |
| 2 | Tom promocional | "rico patrimônio cultural", "de tirar o fôlego", "imperdível" | Descrição neutra e concreta |
| 3 | Gerúndio comentador no fim da frase | "..., destacando a importância de X" | Apagar o trecho ou virar frase própria com informação real |
| 4 | Atribuição vaga | "especialistas apontam", "estudos mostram" | Nomear autor, instituição e ano, ou remover a afirmação |
| 5 | Vocabulário típico de IA | "mergulhar em", "tapeçaria", "multifacetado", "Vale ressaltar que" | Usar a palavra comum ou cortar |
| 6 | Aberturas e fechos de chatbot | "Claro! Aqui está", "No mundo acelerado de hoje", "Espero que ajude" | Começar direto no assunto e parar quando a informação acaba |
| 7 | Disclaimers e frases sobre o processo | "Como modelo de linguagem...", "com base nas informações fornecidas" | Remover; se falta informação, dizer uma vez o que falta |
| 8 | Construções repetitivas | "não é X, é Y", regra dos três, pergunta retórica seguida de resposta, frase de efeito solta | Afirmar direto e usar o número real de itens |
| 9 | Ritmo e estrutura uniformes | frases do mesmo tamanho, excesso de "e", "a realização da implementação da melhoria" | Misturar frases curtas e longas, usar verbos no lugar de nominalizações |
| 10 | Formatação indevida | markdown em e-mail ou redação, negrito em todo item, emojis decorativos, títulos em Title Case | Adequar ao meio; texto corrido por padrão, lista só quando o conteúdo é lista |
| 11 | Pontuação, caracteres e referências | travessão como pausa automática, aspas misturadas, caracteres invisíveis, links com `utm_source=chatgpt.com`, citações inventadas | Pontuação no estilo do autor, remover caracteres invisíveis, verificar cada fonte |
| 12 | Conteúdo e postura | "por um lado... por outro" em tudo, "o futuro é promissor", emoção inventada | Especificidade: ao menos um dado concreto por parágrafo |

Sobre o travessão: ele já não é um indício confiável, porque modelos mais novos usam menos. A skill evita o travessão como pausa automática, mas mantém quando o texto original do autor usa.

## Exemplo

Antes:

> No mundo acelerado de hoje, a educação desempenha um papel crucial na formação de cidadãos. Não se trata apenas de transmitir conteúdo, mas de fomentar o pensamento crítico, a criatividade e a colaboração, refletindo o compromisso com um futuro promissor. Em suma, investir em educação é investir no amanhã.

Depois, com um dado fornecido pelo usuário:

> Na escola onde leciono, o 9º ano passou a resolver problemas de lançamento de projéteis com medições feitas por eles mesmos. As notas na prova subiram pouco, mas o número de perguntas em sala dobrou.

Saíram a abertura de clichê, o paralelismo negativo, a tríade, o gerúndio comentador e o fecho moral. Entrou um fato que só quem estava na sala conhece.

## Regras que a skill segue

- Preserva o significado, os fatos e a intenção do texto original.
- Não inventa dados. Quando falta informação concreta, marca o lugar com `[inserir dado]`.
- Mantém o registro pedido. Formal continua formal; humanizar não significa ficar coloquial.
- Não encena erros de digitação nem gírias forçadas para parecer humano, porque isso é outro tipo de artifício.
- Mantém uma lista de três itens quando os três são reais e necessários.

Antes de entregar, a skill roda um checklist de 10 itens que repete esses critérios (abertura, fechamento, vocabulário, construções, gerúndio, atribuições, formatação, ritmo, dado concreto e voz do autor).

## Instalação e uso

Este repositório traz a documentação da skill. O arquivo da skill fica em `remover-sinais-de-ia/SKILL.md`.

1. Copie a pasta `remover-sinais-de-ia/`, com o `SKILL.md` dentro, para o diretório de skills do Claude.
   - No Claude Code, o diretório pessoal é `~/.claude/skills/`. Para usar só em um projeto, coloque em `.claude/skills/` dentro dele.
   - No Claude.ai, compacte a pasta em um arquivo `.zip` e envie em Configurações, na área de skills.
2. Peça ao Claude para usar a skill pelo nome, por exemplo: "Use a skill remover-sinais-de-ia para revisar este texto". Ela também é acionada quando você pede para humanizar um texto ou escrever sem cara de IA.

Para obter um resultado melhor, informe o gênero do texto e o público, e cole uma amostra de algo que você mesmo escreveu.

## Limitações

- Não há garantia de que o texto passe em detectores de IA. Eles analisam o documento inteiro, e não só os sinais listados aqui.
- Os padrões mudam conforme os modelos evoluem. O travessão é um exemplo: já foi considerado sinal forte e hoje não é mais. A lista precisa de revisão periódica.
- Nenhum sinal isolado prova que um texto foi escrito por IA. O que chama atenção é o acúmulo e a repetição.
- O objetivo é melhorar a qualidade do texto, e não esconder o uso de IA. Em escolas, universidades e empresas com regras sobre o assunto, a responsabilidade de declarar o uso continua sendo de quem assina o texto.

## Fontes e créditos

- Wikipédia, [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) (WP:AISIGNS), versão em inglês. É um guia descritivo, e não um conjunto de regras.
- Pangram, [9 sinais de texto gerado por IA, comprovados por dados](https://www.pangram.com/pt/signs-of-ai-writing). Análise de frequência de markdown, expressões típicas, travessões, listas, tríades, caracteres unicode e emojis.
- Fast Company Brasil, [Esqueça o travessão: esses sinais entregam se um texto foi feito por IA](https://fastcompanybrasil.com/ia/esqueca-o-travessao-esses-sinais-entregam-se-um-texto-foi-feito-por-ia/), sobre o relatório da The Economist (pouca pontuação, excesso de "e", vocabulário rebuscado, "não é X, é Y", regra dos três, estrutura uniforme e prolixidade).

## Licença

Distribuído sob a licença MIT. Veja o arquivo [LICENSE](LICENSE).
