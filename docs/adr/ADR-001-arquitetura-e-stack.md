# ADR-001 — Arquitetura monólito modular + SPA e stack

- **Situação:** aceita
- **Data:** <2026-10-27>
- **Participantes:** Ana Carolina Dias Nonato, Leticia Rodrigues de Andrade, Marina Soares Sberg, Tuany Alves Farias

## Contexto

O projeto Connexa será desenvolvido por uma equipe de 4 integrantes, durante um semestre, com prazo e carga de trabalho limitados. A arquitetura precisa organizar o sistema em módulos, facilitar a manutenção e permitir o desenvolvimento das funcionalidades sem adicionar complexidade desnecessária.

Também é necessário estabelecer fronteiras entre os módulos, evitando que um território de negócio acesse diretamente os dados internos de outro.

## Decisão

Adotar o estilo arquitetural monólito modular + SPA, com duas unidades de implantação: uma aplicação front-end SPA e um único back-end.

O back-end será desenvolvido com Java 21, Spring Boot 4.1 e Spring Modulith 2.1, organizado em módulos de negócio, com separação de responsabilidades e fronteiras bem definidas. O banco de dados adotado será o PostgreSQL 17, utilizando um schema por módulo.

O front-end será desenvolvido utilizando React 19 com TypeScript. A escolha de bibliotecas complementares será definida posteriormente pela equipe, conforme as necessidades de implementação.

## Alternativas consideradas

| Alternativa | Por que não foi escolhida |
Arquitetura de microsserviços | Para uma equipe de 4 integrantes, um semestre e uma carga de trabalho modesta, o custo de manter vários serviços e um broker não se justifica.

Monólito organizado somente em camadas | A separação em camadas não garante, por si só, que um território de negócio não acesse os dados internos de outro.

## Consequências

- **Positivas:** a arquitetura permite organizar o back-end por módulos de negócio, com fronteiras verificadas pelo Spring Modulith. Cada módulo será responsável pelos próprios dados, utilizando um schema específico no PostgreSQL. A separação entre SPA e back-end permite organizar a interface e a API de forma independente.
- **Negativas:** a equipe precisa respeitar as fronteiras entre os módulos e manter a organização do código. Como o back-end é uma única unidade de implantação, todos os módulos compartilham o mesmo processo de execução e implantação.
- **Como verificar:** executar o teste ArquiteturaModularTest para verificar as dependências entre os módulos, impedindo o uso de tipos internos de outros módulos e dependências circulares. No front-end, utilizar as regras de ESLint para impedir importações indevidas entre funcionalidades. Executar também o procedimento ./verificar para validar testes, lint e build.
