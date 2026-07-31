# Repositório:
-https://github.com/LuanSouzasEtecVAV/Atividade-Wai-Aria

# Questão 1
## 1. Explique com suas palavras o que é o WAI-ARIA e qual é sua principal finalidade no desenvolvimento de páginas web. Em sua resposta, comente quem são os principais usuários beneficiados por esse recurso.
 O WAI-ARIA (Web Accessibility Initiative – Accessible Rich Internet Applications) é basicamente um conjunto de atributos que a gente pode adicionar no HTML pra ajudar os navegadores e 
 leitores de tela a entenderem melhor o que tá acontecendo numa página. Ou seja, ele funciona como uma caixa de ferramentas que ajuda o desenvolvedor a tornar a interface do site
 mais acessível para pessoas com algum tipo de deficiência, principalmente em partes dinâmicas cujo o HTML não seja capaz de passar as informações para outros leitores de tela.
 Por exemplo: quando a gente cria um menu que abre e fecha, uma aba, uma janela de aviso (modal) 
 ou qualquer coisa mais "dinâmica" feita com JavaScript, o navegador nem sempre sabe dizer pro usuário o que aquilo é ou em que estado aquilo está (se tá aberto, fechado, selecionado etc). 
 É aí que entra o WAI-ARIA: ele adiciona essa informação extra através de atributos como role, aria-label, aria-expanded, aria-hidden, entre outros.
 Então, resumindo, a principal finalidade do WAI-ARIA é deixar sites e aplicações mais acessíveis, garantindo que qualquer pessoa consiga entender e usar todas as funções da página, não 
 importa como ela interage com ela.

 # Questão 2 – Analisando o botão
 
```html
<button
    class="navbar-toggler"
    type="button"
    aria-controls="menuPrincipal"
    aria-expanded="false"
    aria-label="Abrir menu">
    Menu
</button>
```
 
## a) Qual é a função do atributo `aria-controls`?
 
Sua principal função é criar uma ligação entre dois elementos utilizando o ID e avisar qual elemento da página aquele botão está controlando. Neste exemplo (`aria-controls="menuPrincipal"`), 
o botão está dizendo que ele controla o elemento que tem `id="menuPrincipal"` (nesse caso, o menu que abre e fecha). Isso ajuda o leitor de tela a entender a relação entre o botão e o menu, 
mesmo que visualmente essa ligação já pareça óbvia pra quem enxerga.
 
## b) O que informa o atributo `aria-expanded`?

Ele informa se o elemento que está sendo controlado no momento (no caso, o menu) está aberto ou fechado. Neste exemplo, o valor `"false"` evidencia que o menu está fechado, o que significa
que, caso o botão seja apertado, o JavaScript irá mudar este valor para `"true"`. Isso é importante porque, sem esse atributo, quem usa leitor de tela não teria como saber se o menu já está
aberto ou não, já que o indivíduo não "vê" a tela mudando visualmente.
 
## c) Qual é a importância do atributo `aria-label` para usuários que utilizam leitores de tela?
 
O `aria-label` serve para dar um nome ou uma descrição pro elemento, que o leitor de tela vai falar ao usuário. Em um cenário onde o usuário possui algum problema de visão, ou quando
alguns elementos do site não são muito claros por si só, como botões sem texto ou apenas com ícones, essa ferramenta acaba se tornando muito útil e eficaz. Nesse caso específico, o botão 
até tem o texto "Menu" visível, então já daria pra entender algo. Mas o `aria-label="Abrir menu"` deixa a ação mais clara e específica pra quem usa leitor de tela — em vez de só 
ouvir "Menu, botão", a pessoa ouve "Abrir menu, botão", o que comunica melhor que aquilo é uma ação (abrir algo), e não só um rótulo estático.

# Questão 3 – Reflexão
 
## Por que o WAI-ARIA não substitui o HTML semântico
 
O HTML semântico já possui uma acessibilidade embutida por padrão. Por exemplo: quando temos um `<button>` no programa, o navegador já entende que aquilo é algo clicável, mesmo sem 
adicionar nada ao código. As tags HTML semânticas (`<button>`, `<nav>`, `<main>`) já vêm de fábrica prontas para funcionar. O `<button>`, por exemplo, mesmo sem adicionar nenhuma 
linha a mais de código, já é capaz de:
- Ser apertado e funcionar;
- Ser lido pelo leitor de tela sem erro;
- Ser ativado pelo 'Enter' ou pelo 'Espaço' no teclado;
- Ser selecionado pela tecla Tab.
Em outras palavras, o HTML semântico já atribui ás acessibilidades de fábrica, além de fazer os elementos funcionarem, seja pelo teclado ou pelo mouse.

Já o WAI-ARIA é só uma ferramenta que não possui nenhum tipo de comportamento sozinho. Ele apenas adiciona informação (semântica extra) para que as tecnologias assistivas entendam 
melhor o que está na tela. Ele não faz um elemento virar clicável, não adiciona navegação por teclado e não muda nada visualmente. No caso de um botão, por exemplo, ele só faria o 
leitor de tela entender aquilo como "botão" e ler o nome dele, mas não faria esse elemento necessariamente funcionar como um botão de verdade, com clique, foco pelo teclado e ativação
pelo Enter ou Espaço.
 
## Exemplo para matar a dúvida
 
Se você pegar uma `<div>` (que normalmente não faz nada especial) e colocar `role="button"` nela, o leitor de tela vai falar "botão" quando o usuário passar por ali. Mas isso é só a 
etiqueta. Na prática, essa `<div>` ainda não vai reagir ao clique do mouse nem ao Enter do teclado. você teria que programar tudo isso manualmente em JavaScript, coisa que o `<button>` 
de verdade já faz sozinho.
 
## Situação prática: o botão do menu
 
Imagina que, em vez de usar a tag `<button>`, um desenvolvedor decidisse criar o botão do menu assim, usando uma `<div>` no lugar:
 
```html
<div class="navbar-toggler" onclick="abrirMenu()">
    Menu
</div>
```
 
Visualmente isso até funciona: a `<div>` tem uma classe CSS que deixa ela parecendo um botão, e o clique do mouse chama a função `abrirMenu()` normalmente.
 
O problema surge quando o usuário decide utilizar o teclado ou o leitor de tela:
- Uma `<div>` não recebe foco pelo Tab automaticamente, então quem navega só pelo teclado nem consegue chegar até ela;
- Mesmo se conseguisse chegar, apertar Enter ou Espaço não ativaria o `onclick`, porque `<div>` não tem esse comportamento nativo;
- E o leitor de tela, ao passar por ali, não anuncia nada, ele só vê um texto "Menu" qualquer, sem indicar que aquilo é um elemento clicável.
Pra "consertar" essa `<div>` e fazer ela se comportar como um botão de verdade pra tecnologias assistivas, seria necessário adicionar vários atributos WAI-ARIA nela:
 
```html
<div class="navbar-toggler" 
     role="button" 
     tabindex="0" 
     aria-controls="menuPrincipal" 
     aria-expanded="false"
     onclick="abrirMenu()">
    Menu
</div>
```
 
- `role="button"` avisa o leitor de tela que aquilo é um botão;
- `tabindex="0"` faz o elemento poder receber foco pelo Tab;
- `aria-controls` e `aria-expanded` informam o que ele controla e o estado atual.
Mesmo assim, ainda faltaria programar em JavaScript a ativação pelo 'Enter' ou pelo 'Espaço', porque isso não vem de graça com `role="button"`, diferente do `<button>` de verdade.
 
## Conclusão
 
Por isso, neste caso, o certo seria simplesmente usar a tag `<button>` desde o início, pois ela já resolveria tudo isso sozinha, sem precisar de nenhum atributo ARIA extra. 
O WAI-ARIA só se torna realmente necessário em casos onde, por alguma limitação (design muito customizado, componente muito específico, etc.), não é possível usar a tag semântica
nativa, e aí o desenvolvedor precisa recriar manualmente tudo aquilo que o HTML semântico já ofereceria de graça.
