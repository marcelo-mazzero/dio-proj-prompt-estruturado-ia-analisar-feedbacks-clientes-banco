# Extraindo Insights do Feedback de Clientes Bancários com o uso de Prompt Engineering

> **Projeto prático desenvolvido por Marcelo Mazzero para o [Bootcamp da DIO & Bradesco sobre GenAI, Dados e Cibersegurança](https://www.dio.me/bootcamp/bradesco-dados-ciberseguranca-genai)**

> Este documento consolida a estruturação em três etapas para construção de um prompt analítico eficiente, seguro e acionável para o setor bancário.

---

## 1. Etapa 1

Definir claramente o que a Inteligência Artificial deve produzir, a quem se destina a entrega e qual decisão de negócio ela deve fundamentar.

### Declaração de Intenção
* **Escopo e Objetivo:** Quero que a IA analise comentários espontâneos e avaliações de clientes coletados após interações nos canais de atendimento digital e pós-uso de serviços financeiros para identificar gargalos operacionais críticos, fricções de usabilidade e oportunidades prioritárias de melhoria na jornada do usuário.
* **Público e Aplicação:** O resultado será utilizado conjuntamente pelo Comitê de Produtos Digitais e pela equipe de Customer Experience (CX) para apoiar o direcionamento de investimentos de roadmap, correções de bugs em ambiente produtivo e treinamento de equipes de suporte.
* **Formato de Entrega:** A entrega deve conter um resumo executivo sintetizado, uma matriz estruturada em tabela (com tema, sentimento, trecho de evidência anonimizado, impacto no cliente e recomendação prática) e um plano de priorização imediata.
* **Critério de Sucesso:** O resultado será considerado excelente se apresentar rigor lógico, for 100% ancorado nos dados fornecidos (sem alucinações), categorizar com precisão o nível de urgência e apresentar recomendações objetivas e viáveis de implementação.

---


## 2. Etapa 2

Fornecer delimitações operacionais, detalhar a composição dos dados e estabelecer diretrizes estritas de segurança da informação e governança (LGPD).

### Especificações Técnicas e Restrições
* **Contexto de Negócio:** Análise voltada para o ecossistema bancário digital (aplicativo mobile, transferências Pix, gestão de faturas de cartão de crédito, onboarding/abertura de conta e suporte via assistente virtual/chat humano).
* **Estrutura dos Dados Disponíveis:**
  * `ID_Feedback`: Identificador alfanumérico único.
  * `Data_Hora`: Carimbo temporal da interação.
  * `Canal`: Canal de origem (App Store, Google Play, Chat App, Reclame Aqui, SAC).
  * `Jornada_Mencionada`: Área temática relatada (ex.: Pix, Cartões, Login, Biometria).
  * `Nota_CSAT`: Nota de satisfação declarada de 1 a 5.
  * `Comentario_Cliente`: Texto livre digitado pelo usuário.
* **Critérios de Análise e Classificação:**
  * **Tema / Subtema:** Categorização da causa-raiz.
  * **Sentimento:** Positivo, Neutro, Negativo ou Crítico.
  * **Nível de Urgência:** Baixa, Média, Alta (risco operacional, bloqueio financeiro imediato ou falha de segurança percebida).
  * **Taxa de Atrito:** Grau de impacto na retenção e confiança na instituição financeira.
* **Cuidados, Salvaguardas e Restrições:**
  1. **Privacidade e LGPD:** Não exponha nem transcreva quaisquer dados pessoais ou sensíveis (PII) eventualmente presentes no texto (como nomes, CPFs, e-mails, telefones ou números de agência/conta). Mascare-os obrigatoriamente no padrão `[DADO OCULTADO]`.
  2. **Fidelidade aos Dados:** Trabalhe exclusivamente com os feedbacks contidos na amostra. Não suponha volumes estatísticos, não extrapole percentuais e não crie relatos fictícios.
  3. **Reconhecimento de Limitações:** Diante de comentários ambíguos, truncados ou inconclusivos, sinalize expressamente a restrição sob o status de "Dados Insuficientes para Conclusão".
  4. **Tom de Voz:** Estilo analítico, executivo, direto, impessoal e estritamente orientado à tomada de decisão estratégica.

---


## 3. Etapa 3

Unificar intenção, contexto, estrutura de dados, diretrizes de análise, formato de saída e restrições de segurança em um prompt executável pronto para utilização.

```markdown
Atue como Analista Sênior de Customer Experience (CX) e Inteligência de Operações Bancárias.

Sua tarefa é analisar uma base de comentários e feedbacks de clientes bancários para identificar dores críticas, falhas operacionais em canais digitais, motivos de atrito recorrentes e oportunidades estratégicas de otimização de jornada.

Contexto:
Este diagnóstico será submetido diretamente à liderança de Produtos Digitais e Operações para direcionar o backlog técnico de correção de bugs, revisão de fluxos no aplicativo e capacitação de agentes de suporte. O foco central é transformar manifestações não estruturadas em inteligência acionável e fundamentada.

Dados Fornecidos:
Você receberá registros compostos por: [ID_Feedback], [Data_Hora], [Canal], [Jornada_Mencionada], [Nota_CSAT] e [Comentario_Cliente].

Diretrizes de Análise:
1. Classifique cada feedback por Tema Principal, Sentimento (Positivo, Neutro, Negativo, Crítico) e Urgência (Baixa, Média, Alta).
2. Identifique os três maiores gargalos recorrentes que prejudicam a experiência do usuário.
3. Extraia evidências textuais curtas e representativas para comprovar cada apontamento.
4. Formule recomendações corretivas e preventivas viáveis para os times responsáveis.

Formato Obrigatório da Resposta:
1. Resumo Executivo: Visão geral da saúde da jornada em no máximo 5 linhas, destacando o tom predominante dos usuários.
2. Tabela Analítica:
   | Tema | Urgência | Sentimento Predominante | Evidência Típica (Trecho Curto) | Causa-Raiz Provável | Ação Recomendada |
3. Top 3 Prioridades Imediatas: Três frentes ordenadas pelo maior potencial de redução de atrito e impacto no cliente.
4. Limitações Identificadas: Apontamento de lacunas ou ambiguidades detectadas no conjunto de dados.

Restrições Absolutas:
- Análise estritamente factual: utilize única e exclusivamente os feedbacks fornecidos; não infira dados não declarados nem alucine causas.
- Proteção de dados (LGPD): censure imediatamente qualquer CPF, nome, e-mail, telefone, chave Pix ou dados de conta/cartão utilizando [DADO OCULTADO].
- Respeite o limite dos dados: havendo ruído ou falta de clareza em qualquer registro, marque explicitamente como 'Inconclusivo por falta de dados'.
- Mantenha linguagem formal, executiva, precisa e livre de jargões desnecessários.
```

## 4. Aviso

Este repositório é apenas para fins de estudo pessoal.

---


Desenvolvido por **Marcelo Mazzero** em setembro/2026.
