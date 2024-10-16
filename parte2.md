
# Desafio Técnico: DBA - Parte 2

## Parte 2: Otimização de Performance

### Problema de Performance:
A aplicação web da EdTech está enfrentando problemas de lentidão nas queries que recuperam informações dos alunos e suas notas.

### Tarefas:
1. **Análise de Queries**:
   - Identifique as queries de pior performance utilizando as ferramentas nativas do MySQL, como o **EXPLAIN**.
   - Documente a análise do plano de execução das queries.

2. **Otimização**:
   - Identifique gargalos (falta de índices, joins ineficientes, etc.).
   - Adicione **índices** apropriados.
   - Descreva detalhadamente as mudanças feitas e o impacto em termos de performance (exemplo: redução de tempo de execução).

3. **Avaliação de Performance**:
   - Utilize ferramentas de benchmark para demonstrar a melhoria de performance após as otimizações. Sugestão: **sysbench** ou **MySQL Performance Schema**.

---

### Entregáveis:
- Relatório de otimização:
   - Queries otimizadas.
   - Análise dos planos de execução e índices criados.
   - Comparação de performance antes e depois (tempo de execução, recursos consumidos).

- Scripts SQL das otimizações realizadas.
