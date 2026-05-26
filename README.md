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

## 3. Declaração do Uso de Inteligência Artificial (Conforme Instruções)

Em conformidade com as diretrizes da disciplina apresentadas em sala, declaramos que ferramentas de Inteligência Artificial (Generativa) foram utilizadas estritamente como assistentes de co-pilotagem no início do projeto.

- **O que a IA gerou:** A estrutura inicial do cenário (Scene, Camera, Renderer), a iluminação básica e o loop de renderização, além do laço de repetição (`for`) para posicionar matematicamente os 27 cubinhos no espaço.
- **Onde a IA falhou (e a nossa intervenção):** O código original proposto pela IA não tratava o escopo de rotação de forma global. Ao tentar girar uma face, os cubinhos rotacionavam individualmente em seus próprios eixos centrais, desestruturando o cubo mágico. 

Para solucionar o bug do código gerado pela IA e cumprir os requisitos da especificação, realizamos a engenharia reversa do código e aplicamos os conceitos de hierarquia de nós estudados em aula: implementamos manualmente a lógica de agrupamento temporário com `THREE.Group` e a reancoragem de matrizes com `.attach()`, garantindo o funcionamento perfeito e consistente das rotações das faces Superior e Frontal.

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
