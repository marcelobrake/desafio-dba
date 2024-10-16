
# Desafio Técnico: DBA - Parte 3

## Parte 3: Observabilidade e Monitoramento

### Tarefas:
1. **Configuração de Monitoramento**:
   - Escolha uma ferramenta de monitoramento para o MySQL (ex: **Prometheus + Grafana**, **CloudWatch**, **Percona Monitoring and Management**).
   - Configure a solução de monitoramento e documente o processo de instalação e configuração.

2. **Métricas Monitoradas**:
   - Monitorar métricas essenciais de performance, como:
     - Uso de CPU e Memória
     - Número de conexões ativas
     - InnoDB Buffer Pool Usage
     - Queries mais lentas (Slow Queries)
     - Deadlocks e Locks

3. **Alertas**:
   - Configure **três alertas** para métricas críticas:
     - Latência alta em queries (tempo de execução > 1 segundo).
     - Alto consumo de recursos (CPU > 80% por 10 minutos).
     - Baixo espaço de disco no armazenamento da instância.

---

### Entregáveis:
- Documentação do monitoramento e configuração dos alertas. (pode conter screenshots e/ou descrições de como foram feitas)
- Relatórios das métricas monitoradas. (pode conter dados fake, apenas para exibir a saída de dados)
