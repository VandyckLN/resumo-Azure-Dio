# Comparação entre modelos de preços: DTU vs vCore

| Característica        | Modelo DTU                                                                          | Modelo vCore                                                       |
| --------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| **Descrição**         | Unidade de Transferência de Dados - combina CPU, memória e I/O em uma única unidade | Virtual Core - separa recursos computacionais (CPU/memória) de I/O |
| **Melhor para**       | Cargas de trabalho simples, previsíveis                                             | Cargas de trabalho complexas, necessidades específicas de recursos |
| **Escalabilidade**    | Pacotes fixos de recursos                                                           | Escala independente de CPU e memória                               |
| **Níveis**            | Básico, Standard, Premium                                                           | Uso Geral, Comercialmente Crítico, Hiperescala, Sem Servidor       |
| **Transparência**     | Medida abstrata de recursos                                                         | Medida mais clara (cores virtuais)                                 |
| **Custo**             | Geralmente mais econômico para bancos menores                                       | Mais opções para otimização de custos                              |
| **Licenças híbridas** | Não disponível                                                                      | Desconto para licenças SQL Server existentes                       |
| **Administração**     | Mais simples                                                                        | Mais flexível, mais opções                                         |

## Quando escolher cada modelo:

### Escolha DTU quando:

- Precisar de uma abordagem simples, sem complexidade
- Tiver orçamento limitado para bancos de dados menores
- Não precisar escalar recursos específicos independentemente

### Escolha vCore quando:

- Precisar de controle granular sobre recursos
- Tiver licenças SQL Server existentes (benefício híbrido)
- Necessitar de recursos de computação específicos
- Precisar do modelo Sem Servidor para cargas de trabalho intermitentes
