# Implementar Animação Suave nos Acordeões com Tailwind

Vamos substituir a troca brusca de visibilidade (`display: none` <-> `block`) por uma transição suave de altura usando Grid CSS e utilitários do Tailwind.

## 1. Atualizar Estrutura HTML (`index.html`)
Adicionaremos classes do Tailwind para controlar a animação baseada no estado da classe `active`.

- **Container Pai (`.section-container`)**:
  - Adicionar a classe `group`. Isso permite estilizar os elementos filhos com base na presença da classe `active` neste elemento pai.

- **Conteúdo do Acordeão (`.accordion-content`)**:
  - Remover dependência de estilos externos.
  - Adicionar classes para animação de grid: `grid grid-rows-[0fr] transition-[grid-template-rows] duration-500 ease-in-out`.
  - Adicionar o estado ativo via utilitário de grupo: `group-[.active]:grid-rows-[1fr]`.
  - **Nota**: A `div` interna do conteúdo já possui `overflow-hidden`, o que é essencial para essa técnica funcionar. Adicionaremos `min-h-0` para garantir a compatibilidade.

## 2. Limpar CSS Legado (`style.css`)
Removeremos as regras que conflitam com a nova animação.

- Remover `.accordion-content { display: none; ... }`
- Remover `.active .accordion-content { display: block; }`
- Manter apenas a rotação do ícone (`.active .fa-chevron-down`), que também pode ser movida para o Tailwind se desejar, mas funcionará bem no CSS atual.

## Resultado Esperado
Ao clicar no título, a classe `active` será adicionada pelo JS existente. O Tailwind detectará essa classe no grupo e transicionará o `grid-rows` de `0fr` (altura zero) para `1fr` (altura automática), criando um efeito de deslizamento suave.
