# rust_roam

**rust_roam** é um explorador de diretórios em Rust que mostra o tamanho de pastas e arquivos de forma rápida e organizada. Ele exibe o conteúdo em forma de árvore, com cores para diferenciar diretórios, arquivos e tamanhos, facilitando a visualização do espaço ocupado em seu sistema.

---

## Recursos

* Exibe o tamanho de diretórios e arquivos em formato humano-legível (B, KB, MB, GB, TB).
* Gera árvore hierárquica ordenada por tamanho.
* Diretórios são processados em **multithread** para velocidade máxima.
* Diferencia diretórios e arquivos com cores no terminal:

  * Diretórios: **amarelo**
  * Arquivos: **laranja/vermelho**
  * Tamanhos: **ciano**
  * Root folder: **verde**
* Funciona em Windows, Linux e macOS.

---

## Instalação

1. Clone o repositório:

```bash
git clone https://github.com/eusebioleite/rust_roam.git
cd rust_roam
```

2. Compile o projeto em modo release para máxima performance:

```bash
cargo build --release
```

3. O binário estará em `target/release/rust_roam`.

---

## Uso

### Mostrar o tamanho de um diretório

```bash
./rust_roam -d "C:\Users\Eusébio\Documents"
```

Exemplo de saída:

```
C:\Users\Eusébio\Documents -> 15.3GB
```

### Mostrar árvore de diretórios

```bash
./rust_roam -t "C:\Users\Eusébio\Documents"
```

Exemplo de saída:

```
C:\Users\User\Documents -> 15.3GB
├── ProjectA 8.2GB
├── ProjectB 4.5GB
├── Notes 2.1GB
└── todo.txt 512.0KB
```

---

## Observações

* Apenas o tamanho de diretórios e arquivos **do diretório atual** é mostrado, sem descer para subdiretórios.
* Processamento multithread permite escanear grandes diretórios quase instantaneamente.

---

## Licença

Apache License © Eusébio Leite
