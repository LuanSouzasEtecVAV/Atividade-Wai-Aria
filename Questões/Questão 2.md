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


