<div align="center">

# Slide Stories TypeScript

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)

</div>

## Sobre

Recriação do carrossel de **stories** (estilo Instagram/WhatsApp) em TypeScript puro, orientado a objetos, desenvolvido durante o curso de **TypeScript da Origamid**. Avança automaticamente entre imagens e vídeo, com barra de progresso por item, pausa ao segurar e navegação manual entre slides.

## O que aprendi / O que pratiquei

- **Classes e tipagem de propriedades do DOM**: a classe `Slide` guarda `Element`, `Element[]` e `HTMLElement[] | null` como propriedades tipadas, e usa `instanceof HTMLVideoElement` para tratar vídeo de forma diferente de imagem sem recorrer a `any`.
- **Classe auxiliar para controlar tempo (`Timeout`)**: em vez de usar `setTimeout`/`clearTimeout` soltos, encapsulei a lógica em uma classe que sabe pausar e continuar a contagem de onde parou (`pause`/`continue`), calculando o tempo restante com `Date.now()`.
- **Optional chaining (`?.`)**: usado o tempo todo (`this.timeout?.clear()`, `this.thumb?.classList.add(...)`) porque várias propriedades podem ser `null` antes da inicialização, e o TypeScript obriga a tratar esse caso.
- **Members privados (`private`)**: `addControls` e `addThumbItems` são privados por só fazerem sentido dentro do `init()` da própria classe, deixando a API pública da classe (`show`, `next`, `prev`, `pause`, `continue`) mais enxuta.
- **Persistência simples com `localStorage`**: o slide atual é salvo a cada troca, então recarregar a página volta pro mesmo story em vez de reiniciar do zero.
- **Vídeo como um tipo de slide**: em vez de tratar vídeo com um tempo fixo como as imagens, o `autoVideo` escuta o evento `playing` e usa a duração real do vídeo (`video.duration * 1000`) para disparar o avanço automático.
- **Compilação TypeScript direta (sem bundler)**: `tsconfig.json` configurado com `rootDir`/`outDir` para compilar `src/*.ts` em `dist/*.js`, que é importado como módulo ES nativo direto no `index.html`, sem Vite, Webpack ou build tool.

## Como rodar

```bash
# Clone o repositório
git clone https://github.com/niusdev/slide-stories-typescript.git

# Entre na pasta do projeto
cd slide-stories-typescript

# Instale as dependências (TypeScript)
npm install

# Compile o TypeScript
npx tsc
```

> O projeto não usa bundler nem servidor de desenvolvimento. Depois de compilar, basta abrir o `index.html` no navegador (ou usar uma extensão como o Live Server do VS Code). Para recompilar automaticamente a cada mudança, rode `npx tsc --watch`.

## Estrutura do projeto

```
src/
├── Slide.ts      # Classe principal: controla exibição, navegação e pausa dos slides
├── Timeout.ts    # Classe utilitária para pausar/continuar um setTimeout
└── script.ts     # Ponto de entrada: pega os elementos do DOM e inicia o Slide

assets/           # Imagens e vídeo usados no carrossel
dist/             # Saída compilada do TypeScript (gerada pelo tsc)
```

## Autor

Feito por **Vinícius Gomes Damascena**

[![GitHub](https://img.shields.io/badge/GitHub-niusdev-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/niusdev)