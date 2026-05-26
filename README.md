# Projeto Cubo Mágico 3D

Projeto prático desenvolvido para a disciplina de Programação 3D na Universidade Católica de Pernambuco (UNICAP).

## Requisitos Implementados
- **Cubo 3x3x3:** Construído de forma dinâmica com um grid de 27 cubinhos.
- **Cores Oficiais:** Aplicação correta de materiais com as 6 cores do padrão internacional de cubos mágicos.
- **Controle de Câmera:** Implementação da biblioteca `OrbitControls` permitindo órbita, rotação e zoom da câmera através da interação com o mouse.
- **Rotação de Faces Interativa:** Rotação suave das faces Superior (tecla U) e Frontal (tecla F).
- **Agrupamento Temporário:** Uso da lógica recomendada com `THREE.Group` e os métodos `.attach()` para garantir a consistência das coordenadas globais após cada movimento.
