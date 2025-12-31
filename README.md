# 🧠 OPS: Módulo Quiz da Meada (Especialista Cartorário)

## 📋 Visão Geral
Este pacote contém a configuração especializada do protocolo **ExpertOps** para a função de **Especialista Cartorário (Modo Oitiva)**. O objetivo principal é operacionalizar o "Quiz da Meada" e a "Minuta de Declarações" dentro do ecossistema do Charlie_BOT, focando na jurisdição do **05º Distrito Policial de Jundiaí/SP**.

A arquitetura segue um modelo de **Sobreposição (Overlay)**, onde regras específicas refinam e substituem as diretrizes genéricas para atender à necessidade de agilidade e renderização em tela do operador policial.

---

## 📂 Estrutura do Pacote

### 1. Base Operacional
* **Arquivo:** `ExpertOps_Adaptive_Consultant_Mode_v2_1.json`
* **Função:** Define o núcleo do agente ("ExpertOps Adaptive Consultant"). Estabelece as regras de ingestão de dados, políticas de citação e o objetivo macro de converter solicitações ambíguas em entregáveis precisos.
* **Política Padrão:** Originalmente define a saída como `json_only` (apenas JSON), que é sobrescrita pelos overlays abaixo.

### 2. Overlay de Especialização (v2)
* **Arquivo:** `overlay_especialista_cartorario_quiz_da_meada_v2.json`
* **Função:** Aplica a persona de **Senior/Principal** na área Legal/Polícia Judiciária.
* **Diretrizes Específicas:**
    * **Jurisdição:** BR-SP-Jundiaí-05DP.
    * **Limites:** Vedada a invenção de fatos (neutralidade absoluta).
    * **Mudança Crítica:** Remove a trava de "apenas JSON", permitindo `conversational_screen_render` para facilitar a leitura durante oitivas.

### 3. Protocolo de Retificação de Saída (v3)
* **Arquivo:** `Overlay_retifica_saida.txt`
* **Função:** Atualização de interface crítica (v3).
* **Definição:** Força a renderização do **Quiz da Meada** como uma **lista numerada (1 a 7)** em Markdown/Texto corrido, abandonando blocos de código para interação direta. Garante que o JSON permaneça apenas como camada de dados oculta (buffer), enquanto a interface com o operador é fluida.

---

## ⚙️ Regras de Negócio e Comportamento

### Fluxo de Oitiva
1.  **Entrada:** O sistema recebe o Boletim de Ocorrência (BO) ou relato inicial.
2.  **Processamento:** O `ExpertOps` analisa lacunas fáticas com base na materialidade (TGC).
3.  **Saída (Quiz):** Gera 7 questões estratégicas numeradas, renderizadas diretamente no chat (sem formatação de código).
4.  **Minuta:** Após as respostas, converte os dados em texto corrido fluído para o termo de declaração.

### Políticas de Anti-Alucinação (Boundaries)
Conforme definido no Overlay v2:
* **Lacunas:** Devem ser marcadas explicitamente como "não informado" ou questionadas no Quiz.
* **Voz:** Técnica, objetiva e neutra ("Declarante afirma...", "Vítima relata...").
* **Estilo:** Proibido uso de tabelas complexas para esta função; prioridade para texto narrativo.

---

## 🚀 Como Implementar
Ao carregar este módulo no agente (Gemini/Charlie_BOT), a ordem de precedência lógica é:
1.  Carregar `ExpertOps...v2_1.json` para estabelecer a base.
2.  Aplicar `overlay...v2.json` para definir o contexto cartorário.
3.  Aplicar `Overlay_retifica_saida.txt` para garantir a formatação visual correta.

**Status da Versão:** v3.0 (Adaptive Consultant + Cartorário Overlay v2 + Render Fix)
**Responsável:** 05º DP Jundiaí - Setor de Inteligência Cartorária

```
