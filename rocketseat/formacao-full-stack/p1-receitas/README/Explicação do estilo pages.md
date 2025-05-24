# Explicação do estilo `#pages` no arquivo [[11. OST/courses-projects-made/rocketseat/formacao-full-stack/p1-receitas/assets/style.css|style]]
Vamos **explicar cada linha** desse código CSS como se estivéssemos desmontando um brinquedo peça por peça:

---

```css
#page {
  width: 800px;
  padding: 24px;
  background-color: #f0e8c2;
  border-radius: 24px;
  margin: 48px auto 4px;
  box-sizing: border-box;
}
```

Esse seletor `#page` está aplicando estilos a um elemento com `id="page"` no HTML.

---

## 🧩 Linha por linha

### `width: 800px;`

- Define a **largura fixa** do elemento como 800 pixels.
    
- Isso quer dizer que o elemento sempre terá exatamente 800px de largura, independentemente do tamanho da tela.
    

---

### `padding: 24px;`

- Cria um **espaço interno** de 24 pixels em todos os lados (top, right, bottom, left).
    
- Isso significa que o conteúdo dentro da `#page` não vai encostar diretamente nas bordas.
    

---

### `background-color: #f0e8c2;`

- Define a **cor de fundo** como um tom bege claro.
    
- Esse valor hexadecimal representa a cor visual do bloco.
    

---

### `border-radius: 24px;`

- Deixa as **bordas arredondadas** com raio de 24 pixels.
    
- Isso dá um visual suave, arredondado, nas pontas do bloco.
    

---

### `margin: 48px auto 4px;`

- Define a **margem externa**, ou seja, o espaço entre o elemento e os outros elementos ao redor:
    
    - **48px em cima**
        
    - **`auto` nas laterais** → centraliza horizontalmente (quando o `width` está definido!)
        
    - **4px embaixo**
        

💡 Esse é um truque clássico para **centralizar blocos na tela**.

---

### `box-sizing: border-box;`

- Altera a forma como o navegador calcula o tamanho do elemento.
    
- Com `border-box`, o `padding` **não aumenta** o tamanho total do elemento.
    

🔍 Exemplo:  
Se você tem `width: 800px` e `padding: 24px` com `box-sizing: border-box`, a largura **continua 800px no total**, e o conteúdo se ajusta dentro disso.  
Sem `border-box`, o total seria `800 + 24 + 24 = 848px`.

---

## ✅ Resultado visual final:

Esse bloco `#page`:

- Tem largura fixa e centralizada
    
- É espaçoso por dentro (`padding`)
    
- Tem um fundo bege claro
    
- Bordas arredondadas
    
- Fica centralizado na tela com um bom espaço em cima
    

---

Se quiser, posso fazer uma versão responsiva disso, ou explicar como ele se comporta em telas menores. Deseja?