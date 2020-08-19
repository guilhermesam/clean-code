## Índice
- [Introdução](#introdução)
- [Capítulo 1: Código Limpo](#capítulo-1-código-limpo)
	- [O Código](#o-código)
	- [Código Ruim](#código-ruim)
	- [O Custo de Ter um Código Confuso](#o-custo-de-ter-um-código-confuso)
	- [O Principal Dilema](#o-principal-dilema)
	- [A Arte do Código Limpo](#a-arte-do-código-limpo)
	- [O que é um Código Limpo](#o-que-é-um-código-limpo)

## Introdução

"The only valid measurement of code quality: WTFs / minute."

A perfeição se encontra nos pequenos detalhes, mesmo no nome da mais isolada variável presente no código. Existe uma abordagem muito interessante, de origem japonesa, chamada Manutenção Produtiva Total (da sigla em inglês TPM ), onde o foco é a manutenção ao invés da produção em massa, baseada em um conjunto de princípios demoninado 5S:

- Seiri ("ordenar"): Saber onde estão as coisas, por exemplo, aplicar nomes significativos nas variáveis para facilitar sua localização e identificação mais tarde;

- Seiton ("sistematizar"): Um pedaço de código deve estar exatamente onde o autor ou quem está lendo espera encontrá-lo. Caso não esteja, é necessário que seja refatorado;

- Seiso ("polir"): Manter o local de trabalho limpo e organizado, não apenas os diretórios do projeto, mas o próprio local físico de trabalho, seja o quarto, o escritório, etc. No escopo de desenvolvimento, isso também significa deixar o código o mais limpo possível e livre de trechos desnecessários, como comentários com desejos futuros ou informações sobre o passado;

- Seiketsu ("padronização"): A concordância da equipe acerca da manutenção do workspace limpo e organizado;

- Shutsuke ("autodisciplina"): Disciplina para aceitar e seguir as práticas (e eventuais mudanças) e estar disposto à mudança.

	Existem duas "portas": a do good code e a do bad code. E atravessar uma
delas é reflexo da habilidade profissional, esteja ela presente ou ausente. Existem duas vertentes para se obter habilidade profissional: conhecimento e trabalho. É necessário não apenas adquirir o conhecimento teórico acerca de princípios, modelos, padrões, heurísticas, etc., mas também destrinchar esse conhecimento em um cenário prático, através do esforço e trabalho duro.
	É importante destacar que este livro não é trivial, como diz o próprio
autor, "não é um livro fácil e simples, que você pode ler num avião e terminar antes de aterrisar...". O caminho, como citado anteriormente, não é composto apenas da teoria, mas sim, de puro trabalho duro, por isso, é necessário muita prática acompanhada da leitura.
	O livro é dividido em três partes: na primeira, existem diversos
capítulos abordando a teoria sobre o código limpo, como princípios, padrões e práticas, além de muitas demonstrações de código; na segunda, o aprendizado será mais trabalhoso, pois serão abordados conceitos práticos de limpeza de código e o leitor será convidado a resolver diversos exercícios; a terceira, conforme descrita pelo autor como uma lista de "odores", abordará diversas heurísticas sobre identificação de focos para refatoração de código, ou seja, um "odor", em que tentaremos compreender nossas reações quando estivermos lendo ou alterando esse código.

## Capítulo 1: Código Limpo
	
### O Código

Algumas pessoas dizem que um dia a programação como conhecemos será extinta, ou seja, que todo código seria gerado automaticamente pelas máquinas de acordo com determinadas especificações e modelos, e não mais escrito manualmente. Confesso que eu mesmo também pensava assim até bem pouco tempo atrás, porém, nós nunca estaremos livre da programação em codificação, já que eles representam os detalhes dos requisitos. Especificar requisitos de modo que uma máquina consiga compreendê-los é programar, e a especificação é o código, e isso nunca irá mudar.

Esperar que, um dia, as máquinas alcancem um nível de comunicação com linguagem natural tão perfeita a ponto de uma simples especificação ser suficiente para gerar um programa executável perfeito e livre de inconsistências é como um matemático esperar que a matemática evolua tanto a ponto da formalidade da definição ser desnecessária. Isso jamais acontecerá, pois até mesmo os humanos, com toda sua criatividade e capacidade de adaptação e compreensão das "entrelinhas", não são capazes de criar sistemas de software que atendam de forma bem-sucedida aos requisitos confusos que os seus clientes por vezes definiram.

### Código Ruim

Um código confuso ou mal escrito pode facilmente levar uma empresa à ruína, devido ao fato de que se torna cada vez mais difícil mantê-lo para suportar mudanças e atualizações. Não devemos ser procrastinadores ou preguiçosos; por mais que o código funcione num primeiro momento, mantê-lo limpo e polido é algo tão importante quanto o funcionamento perfeito. Percorrer um código ruim é como atravessar um caminho tortuoso repleto de armadilhas invisíveis do olhar, procuramos alguma dica ou instrução, mas a cada passo dado, nos encontramos mais e mais perdidos, porém, ainda assim, nunca é tarde demais para corrigí-lo ou limpá-lo.

### O Custo de Ter um Código Confuso

Como dito anteriormente, um código ruim pode facilmente levar uma empresa, independemente do seu porte, ao declínio. Os efeitos de se utilizar um código mal escrito por muito tempo, ignorando a ameaça, é uma verdadeira bola de neve: talvez no começo, ainda seja possível de se trabalhar, porém, com o passar do tempo e o crescimento do tamanho do projeto, a "bagunça" poderá crescer exponencialmente a ponto de se tornar impossível sua correção, ou seja, não haverá solução alguma. Ao cair em tal problema, alguns resultados são esperados, como a redução da produtividade da equipe, visto que, além de implementar novas funcionalidades, ainda será necessário criar uma harmonia entre o código antigo e o código que irá implementar tais mudanças, trabalho esse que terá uma variância de complexidade de acordo com a qualidade do código. 

Além disso, um código mal escrito ainda afeta a integração de novos membros ao projeto, que se encontrarão, como descrito anteriormente, no mesmo caminho tortuoso repleto de armadilhas, e sofrerão do mesmo problema de redução de produtividade do resto da equipe.

No final de tudo, o que geralmente é uma "explosão". O código está tão ruim, sujo e bagunçado que o trabalho torna-se insustentável. Surge a necessidade de uma reformulação no projeto, literalmente começar do 0 com novas diretrizes, mudanças a serem aplicadas, etc. Porém, o sistema atual não pode ser apenas descartado; a equipe responsável pelo novo sistema precisa que este seja, no mínimo, igual ao antigo, além de se manter atualizada em tudo que ocorre no antigo. Este processo que mais se assemelha a uma corrida pode levar de semanas até vários anos, e durante todo esse tempo, é comum que boa parte da equipe tenha se desmantelado, e os responsáveis pelo novo sistema exigem uma nova reformulação, pois a manutenção do código se tornou novamente insustentável.

O ponto é que muitos desenvolvedores atribuem a culpa pelo fracasso do código a diversos fatores, sejam eles clientes insuportáveis, gestores extremamente exigentes com prazos e requisitos, alterações muito impactantes no plano original, etc. É importante que o desenvolvedor do código assuma um papel de não apenas um mero escritor de código, mas sim uma voz ativa na empresa, que consiga dar sua opinião acerca de requisitos e prazos, que consiga auxiliar o gerente na construção do plano e no respeito a esse. A necessidade do mercado é por **resolvedores de problemas**, não por criadores ou meros identificadores. 

### O Principal Dilema

Todo desenvolvedor com alguma experiência consegue identificar as bagunças antigas feitas e o impacto que elas podem causar no rendimento, porém, vários deles cometem alguns pequenos "delitos" utilizando um código bagunçado quando o prazo aperta, acarretando em mais tempo perdido no futuro para corrigir o estrago que aquela bagunça causou. O que acontece de verdade é que a solução para um problema nunca é um "malabarismo" ou a popular gambiarra; A desorganização e a bagunça se acumularão e a redução da produtividade será instantânea e proporcional ao nível da bagunça. Por isso, a melhor solução é sempre manter o **código limpo**.

### A Arte do Código Limpo

Escrever um código é como pintar uma obra de arte (realmente alguns códigos são dignos de serem emoldurados e colocados acima da lareira como objeto de inveja para visitas). Uma pergunta bastante válida, a essa altura, é: como escrever um código limpo? Semelhante a uma obra de arte, é fácil reconhecer quando uma foi bem pintada, se for o caso de uma paisagem, com boas técnicas de iluminação, sombreamento, proporções, paleta de cores, etc. Porém, conseguir identificar a presença dessas características não nos torna bons pintores. O mesmo serve para o código. Ter a capacidade de escrever um código limpo significa dominar um conjunto de pequenas e delicadas técnicas e, principalmente, possuir **sensibilidade ao código**. Essa sensiblidade permite que o programador visualize possíveis soluções e rotas a serem seguidas para sair de um código confuso e transformá-lo em uma obra prima.

### O que é um Código Limpo ?

Antes de propriamente definir como escrever um código limpo, é necessário definir **o que é um código limpo**. O fato é que esta definição é um tanto quanto nebulosa; eis algumas definições de famosos programadores da história:

> "Gosto do meu código elegante e eficiente. A lógica deve ser direta para dificultar o encobrimento de bugs, as dependências mínimas para facilitar a manutenção, o tratamento de erro completo de acordo com uma estratégia clara e o desempenho próximo do mais eficiente de modo a não incitar as pessoas a tornarem o código confuso com otimizações sorrateiras. O código limpo **faz bem apenas uma coisa**."
		
> **Bjarne Stroustrup, criador da linguagem C++**
		
É interessante destacarmos a palavra "elegante" empregada por Bjarne. Em outras palavras, um código limpo deve ser harmonioso, charmoso, leve, cuja leitura deve ser natural e de fácil compreensão, semelhante a ouvir uma música ou admirar uma obra de arte. É interessante o destaque na palavra incitar: de fato, em um código confuso e desorganizado, a tentativa de correção por parte de outras pessoas além da que originalmente escreveu o código somente tende a piorá-lo, gerando uma bola de neve. Outro ponto que merece destaque é a conclusão da sentença: o código limpo deve fazer apenas uma coisa, ou seja, em uma estrutura funcional, por exemplo, cada função deve ser responsável por fazer uma única coisa, evitando duplicidade, ambiguidade e sobrecarga de responsabilidade. Cada componente do código deve ter uma única tarefa bem delimitada.

> "Um código limpo é simples e direto. Ele é tão legível quanto uma prosa bem escrita. Ele jamais torna confuso o objetivo do desenvolvedor, em vez disso, ele está repleto de abstrações claras e linhas de controle objetivas."

> **Grady Booch, autor do livro Object Oriented Analysis and Design with Applications**

Grady destaca a questão da legibilidade do código, ou seja, a capacidade deste de ser autoexplicativo e de fácil entendimento. Entram nesse aspecto o questionamento do uso de comentários: é de fato muito melhor um código autoexplicativo, com lógica bem definida do que 1000 linhas de comentários poluídos. Ler um código deve ser como ler uma prosa, ou quem sabe como ler uma história, onde exista uma "introdução", ou seja, uma delimitação do problema a ser solucionado, um "desenvolvimento" com a lógica construída e um final com a revelação dos "mistérios" solucionados por aquele código.

> "Além de seu criador, um desenvolvedor pode ter e melhorar um código limpo. Ele tem testes de unidade e de aceitação, nomes significativos; ele oferece apenas uma maneira, e não várias, de se fazer uma tarefa; possui poucas dependências, as quais são explicitamente declaradas e oferecem um API mínimo e claro. O código deve ser inteligível já que, dependendo da linguagem, nem toda informação necessária pode ser expressa no código em si."

> **O "grande" Dave Thomas, fundador da OTI e pai da estratégia Eclipse**
