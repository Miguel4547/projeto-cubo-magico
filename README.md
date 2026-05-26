# Relatório de Projeto: Cubo Mágico 3D Interativo
**Disciplina:** Programação 3D  
**Instituição:** Universidade Católica de Pernambuco (UNICAP)  
**Professor:** Pedro Ximenes  

---

## 1. Introdução e Objetivo do Projeto
O objetivo deste trabalho foi desenvolver um protótipo funcional e interativo de um **Cubo Mágico 3D (3x3x3)** rodando diretamente no navegador através da biblioteca **Three.js**. O projeto visa consolidar os conceitos de transformações geométricas tridimensionais (translação, rotação e escala), manipulação de matrizes de cena, e gerenciamento de escopo por hierarquia de objetos (nós pais e filhos).

## 2. Requisitos Implementados
Conforme as diretrizes e os requisitos mínimos exigidos para o projeto, foram desenvolvidas as seguintes funcionalidades:
- **Malha de Cubinhos:** Renderização de um grid de 27 cubinhos individuais de dimensões $0.95 \times 0.95 \times 0.95$ para gerar o espaçamento estético correto entre os blocos.
- **Cores Oficiais:** Mapeamento de materiais (`MeshStandardMaterial`) utilizando o padrão de cores oficiais de cubos mágicos (Branco, Amarelo, Verde, Laranja, Azul e Vermelho).
- **Controle de Câmera (OrbitControls):** Integração da biblioteca de órbita do Three.js para permitir que o usuário use o mouse para rotacionar a câmera ao redor do objeto e aplicar zoom dinâmico.
- **Rotação de Duas Faces:** Mapeamento e rotação interativa completa da **Face Superior (Up)** por meio da tecla `U` (ou botão na tela) e da **Face Frontal (Front)** por meio da tecla `F` (ou botão na tela).

---

## 3. Metodologia de Desenvolvimento e Uso de Inteligência Artificial

No início do desenvolvimento, utilizamos a Inteligência Artificial (ChatGPT) para auxiliar na criação da estrutura base do cenário tridimensional, geração do loop de renderização e posicionamento inicial dos 27 blocos no espaço cartesiano ($X, Y, Z$). 

### Registro do Processo de Desenvolvimento:
Abaixo consta o registro da estrutura de código inicialmente sugerida pela Inteligência Artificial:

![Captura de Tela do ChatGPT auxiliando no código do projeto](./Midia.jpg)

*Nota: Para que a imagem apareça corretamente no GitHub, salve a foto que você me enviou com o nome exato de `Midia.jpg` dentro da mesma pasta do repositório onde está este arquivo README.*

---

## 4. Desafios Encontrados e Soluções (A Lógica do Cubo)

Apesar de a inteligência artificial ter ajudado na estrutura inicial do grid de blocos, o código gerado por ela apresentava um erro grave: **os cubinhos giravam apenas em torno de seus próprios eixos locais**, fazendo com que o cubo mágico se "desmanchasse" visualmente ao invés de rotacionar a face como um bloco sólido. 

Para resolver essa limitação técnica, aplicamos a **Dica de Implementação** fornecida nos slides de aula da UNICAP:

1. **Agrupamento Temporário via `THREE.Group`:** Criamos um grupo geométrico vazio posicionado no centro do cenário sempre que uma rotação é solicitada.
2. **Filtragem por Posição Global (`.getWorldPosition()`):** Como as coordenadas locais dos blocos se alteram a cada movimento, o código varre os 27 cubinhos capturando suas posições exatas no mundo tridimensional, identificando quais pertencem à face que deve girar (ex: onde o $Y$ global arredondado é igual a $1$).
3. **Ancoragem Dinâmica com `.attach()`:** Em vez de usar o método `.add()`, utilizamos o `.attach()`. Esse método transfere os cubinhos da cena principal para o grupo calculando as matrizes de transformação nos bastidores, permitindo que a animação suave de 90 graus ($\pi/2$ radianos) ocorra ao redor do eixo correto.
4. **Devolução para a Cena Principal:** Após o término da animação, os blocos são reancorados de volta à cena global utilizando `scene.attach(c)`, gravando de forma permanente as suas novas posições físicas para que o próximo movimento ocorra sem bugs.

## 5. Conclusão
O projeto atingiu com sucesso todos os objetivos propostos pelo plano de ensino. A utilização mista de assistentes baseados em IA combinada com a engenharia reversa e a aplicação prática de escopo e hierarquias de transformação 3D ensinadas em sala de aula permitiram a entrega de um sistema limpo, performático e visualmente preciso.
