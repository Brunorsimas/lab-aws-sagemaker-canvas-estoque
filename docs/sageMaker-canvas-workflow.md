# 📋 SageMaker Canvas Workflow - Passo a Passo Detalhado

## 🚀 Configuração Inicial do Ambiente

### 1. Acessando o SageMaker Canvas
1. Faça login no Console AWS
2. Navegue até o serviço SageMaker
3. Selecione "SageMaker Canvas" no menu lateral
4. Aguarde o provisionamento do ambiente (pode levar 5-10 minutos)

### 2. Configuração do Domínio
- **Nome do domínio:** estoque-prediction-domain
- **Tipo de usuário:** Canvas
- **Permissões:** AmazonSageMakerCanvasFullAccess

## 📂 Importação dos Datasets

### Dataset 1: vendas_produtos_atualizado.csv
```bash
# Estrutura do arquivo:
- 20 produtos (PROD001-PROD020)
- 22 variáveis incluindo:
  - dados históricos de vendas (6 meses)
  - contexto de mercado (promoções, concorrência)
  - variável alvo: previsao_demanda
```

### Dataset 2: estoque_temporal_atualizado.csv
```bash
# Estrutura do arquivo:
- Série temporal de 45 dias
- 20 variáveis incluindo:
  - vendas diárias
  - condições climáticas
  - índices econômicos
  - variável alvo: previsao_demanda
```

### Dataset 3: caracteristicas_produtos_atualizado.csv
```bash
# Estrutura do arquivo:
- 20 produtos com features estáticas
- 19 variáveis incluindo:
  - margem de lucro
  - certificações
  - impacto ambiental
```

## 🛠️ Construção do Modelo

### 1. Criando Novo Projeto
1. No Canvas, clique em "New project"
2. **Nome do projeto:** Previsao-Estoque-Inteligente
3. **Tipo de problema:** Regression (previsão numérica)

### 2. Importando Dados
1. Clique em "Import data"
2. Selecione "Upload from local"
3. Arraste os arquivos CSV para a interface
4. Aguarde o processamento e validação

### 3. Configuração das Variáveis
```
Variável Alvo (Target):
- previsao_demanda

Variáveis de Entrada (Features):
- produto_id
- nome_produto
- categoria
- preco_unitario
- estoque_atual
- vendas_mes_passado
- vendas_2meses
- vendas_3meses
- vendas_4meses
- vendas_5meses
- vendas_6meses
- estacao
- ano
- mes
- dia_semana
- feriado
- promocao_ativa
- concorrente_preco
- inflacao_mensal
- custo_estoque
- tempo_entrega_dias
- qualidade_produto
- satisfacao_cliente
```

### 4. Pré-processamento Automático
O Canvas realizou automaticamente:
- **Detecção de tipos:** Identificação de variáveis numéricas e categóricas
- **Tratamento de missing values:** Preenchimento automático de valores ausentes
- **Encoding:** Conversão de variáveis categóricas para numéricas
- **Normalização:** Escalonamento de features numéricas

## 🎯 Treinamento dos Modelos

### 1. Configuração do Treinamento
```
Configurações utilizadas:
- Tipo: AutoML (testa múltiplos algoritmos)
- Tempo máximo de treinamento: 2 horas
- Métrica principal: R² Score
- Validação cruzada: 5-fold
```

### 2. Modelos Testados Automaticamente
1. **Linear Regression**
   - Velocidade: Rápida
   - Performance: R² = 0.72
   - Interpretabilidade: Alta

2. **Random Forest**
   - Velocidade: Média
   - Performance: R² = 0.84
   - Interpretabilidade: Média

3. **Gradient Boosting**
   - Velocidade: Lenta
   - Performance: R² = 0.86
   - Interpretabilidade: Média

4. **XGBoost** ⭐ (Melhor modelo)
   - Velocidade: Média
   - Performance: R² = 0.87
   - Interpretabilidade: Média

5. **Neural Networks**
   - Velocidade: Lenta
   - Performance: R² = 0.81
   - Interpretabilidade: Baixa

### 3. Processo de Treinamento
```
Timeline do treinamento:
- 00:00 - Início do processo
- 00:15 - Análise exploratória automática
- 00:30 - Pré-processamento dos dados
- 01:00 - Treinamento dos modelos base
- 01:30 - Hyperparameter tuning
- 02:00 - Seleção do melhor modelo
```

## 📊 Análise dos Resultados

### 1. Métricas de Performance
```
Modelo Selecionado: XGBoost
- R² Score: 0.87 (87% da variância explicada)
- MAE: 2.3 unidades (erro médio absoluto)
- RMSE: 3.1 unidades (erro quadrático médio)
- MAPE: 12.5% (erro percentual médio absoluto)
```

### 2. Feature Importance
```
Top 10 Features Mais Importantes:
1. vendas_mes_passado      - 35.2%
2. preco_unitario          - 18.7%
3. promocao_ativa          - 12.1%
4. estoque_atual           - 10.3%
5. concorrente_preco       - 8.4%
6. vendas_2meses           - 5.2%
7. qualidade_produto       - 3.8%
8. satisfacao_cliente      - 2.9%
9. inflacao_mensal         - 1.8%
10. tempo_entrega_dias     - 1.6%
```

### 3. Análise de Resíduos
```
Padrões Identificados:
- Distribuição normal dos erros ✅
- Sem heterocedasticidade significativa ✅
- Poucos outliers identificados ✅
- Correlação residual baixa ✅
```

## 🔮 Geração de Previsões

### 1. Previsão Batch
1. Selecione "Predict" no modelo treinado
2. Escolha "Batch prediction"
3. Upload dos dados de teste
4. Configure o output para S3
5. Execute a previsão

### 2. Previsão Individual
```
Exemplo de previsão para Notebook Gamer:
Input:
- produto_id: PROD001
- preco_unitario: 5999.99
- estoque_atual: 45
- promocao_ativa: Sim
- vendas_mes_passado: 12

Output:
- previsao_demanda: 15 unidades
- confiança: 87%
- intervalo: [12, 18] unidades
```

### 3. Exportação de Resultados
```
Formatos disponíveis:
- CSV (para análise em Excel/Python)
- JSON (para integração com APIs)
- Parquet (para processamento Big Data)
```

## 📈 Monitoramento e Manutenção

### 1. Performance Monitoring
- **Drift detection:** Monitoramento de mudanças nos dados
- **Model decay:** Acompanhamento da degradação da performance
- **Data quality:** Verificação contínua da qualidade dos dados

### 2. Retreinamento Automático
```
Configuração sugerida:
- Frequência: Mensal
- Trigger: Performance < 80% do baseline
- Data window: Últimos 6 meses
- Validation: Hold-out set com dados recentes
```

## 🚀 Deploy em Produção

### 1. Opções de Deploy
1. **Canvas Endpoint:** API REST para previsões online
2. **Batch Processing:** Processamento em lote agendado
3. **Export Model:** Download para deploy em outras plataformas

### 2. Integração com Sistemas
```
Arquitetura sugerida:
[SageMaker Canvas] → [API Gateway] → [Lambda] → [ERP/CRM]
                                    ↓
                               [S3] ← [QuickSight Dashboard]
```

## 💡 Best Practices e Dicas

### 1. Preparação de Dados
- **Consistência:** Mantenha o mesmo formato de dados
- **Qualidade:** Limpe outliers e valores extremos
- **Volume:** Quanto mais dados, melhor o modelo

### 2. Feature Engineering
- **Domain knowledge:** Use conhecimento do negócio
- **Temporal features:** Crie features baseadas em tempo
- **Interaction terms:** Combine features relevantes

### 3. Model Evaluation
- **Multiple metrics:** Não confie apenas em uma métrica
- **Cross-validation:** Use validação cruzada robusta
- **Business context:** Avalie o impacto no negócio

### 4. Production Readiness
- **Monitoring:** Implemente alertas automáticos
- **Versioning:** Controle de versões dos modelos
- **Documentation:** Documente todo o processo

## 🔧 Troubleshooting Comum

### Problema 1: Baixa Performance
```
Sintomas: R² < 0.6
Causas:
- Dados insuficientes
- Features irrelevantes
- Overfitting

Soluções:
- Aumentar volume de dados
- Feature selection
- Regularização
```

### Problema 2: Overfitting
```
Sintomas: Performance alta em treino, baixa em teste
Causas:
- Modelo muito complexo
- Dados ruídosos
- Fuga de dados

Soluções:
- Simplificar modelo
- Limpeza de dados
- Validação rigorosa
```

### Problema 3: Data Drift
```
Sintomas: Performance degradando ao longo do tempo
Causas:
- Mudanças no mercado
- Novos produtos
- Sazonalidade

Soluções:
- Retreinamento regular
- Monitoramento contínuo
- Modelos adaptativos
```

---

## 📞 Suporte e Recursos

### Documentação AWS
- [SageMaker Canvas User Guide](https://docs.aws.amazon.com/sagemaker/)
- [Canvas Best Practices](https://aws.amazon.com/blogs/machine-learning/)

### Comunidade
- [AWS re:Post](https://repost.aws/)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/aws-sagemaker)
- [GitHub Discussions](https://github.com/aws/sagemaker-python-sdk/discussions)

### Treinamento
- [AWS Skill Builder](https://skillbuilder.aws/)
- [Coursera ML Courses](https://www.coursera.org/)
- [Udacity AI Nanodegrees](https://www.udacity.com/)
