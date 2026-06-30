# NetGuard Pro

Gerenciamento e segurança de rede em tempo real — monitore, proteja e otimize sua infraestrutura a partir de um único painel.

NetGuard Pro acompanha continuamente o desempenho dos seus servidores (CPU, memória, disco, latência, perda de pacotes), aciona failover automático quando algo falha, e protege sua rede com firewall configurável e detecção de ameaças.

---

## Sumário

- [Começando Rapidamente](#começando-rapidamente)
- [Funcionalidades Principais](#funcionalidades-principais)
- [Caso de Uso: Reduzindo Tempo de Inatividade com Failover](#caso-de-uso-reduzindo-tempo-de-inatividade-com-failover)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Para Desenvolvedores: Integração via API](#para-desenvolvedores-integração-via-api)
- [Como Contribuir](#como-contribuir)
- [Solução de Problemas Comuns](#solução-de-problemas-comuns)
- [Suporte](#suporte)
- [Licença](#licença)

---

## Começando Rapidamente

### Requisitos

- Linux Ubuntu 20.04+ ou Windows Server 2019+
- 8 GB de RAM (16 GB recomendado em produção)
- Docker instalado
- Acesso de saída na porta 443

### Instalação

```bash
git clone https://github.com/netguardpro/netguard-pro.git
cd netguard-pro
docker compose up -d
```

### Primeiro acesso

1. Abra `http://localhost:8080` no navegador.
2. Crie sua conta de administrador.
3. Adicione o primeiro servidor a ser monitorado (IP + credenciais de acesso).
4. Pronto — em poucos segundos as métricas começam a aparecer no painel.

> **Dica:** comece monitorando apenas 1-2 servidores críticos antes de adicionar toda a sua infraestrutura. Isso facilita validar alertas e regras de firewall sem ruído.

---

## Funcionalidades Principais

| Funcionalidade | O que ela faz |
| --- | --- |
| **Monitoramento em tempo real** | Acompanha CPU, memória, disco, latência e perda de pacotes por servidor |
| **Failover automático** | Redireciona tráfego para um serviço de contingência quando o primário falha |
| **Balanceamento de carga** | Distribui requisições entre servidores para evitar sobrecarga |
| **Firewall configurável** | Define regras de acesso por IP, porta ou serviço |
| **Detecção de ameaças** | Sinaliza atividades suspeitas com alertas priorizáveis |
| **Painel personalizável** | Cada equipe escolhe quais métricas aparecem em destaque |

---

## Caso de Uso: Reduzindo Tempo de Inatividade com Failover

**Cenário:** uma equipe de TI mantém um serviço de autenticação crítico rodando em um único servidor. Durante um pico de tráfego, o servidor primário começa a falhar.

**Com o NetGuard Pro:**

1. O sistema detecta a queda de desempenho via monitoramento contínuo (latência e taxa de erro acima do normal).
2. O failover automático redireciona as requisições para o servidor de contingência em segundos.
3. Um alerta é enviado à equipe, com o histórico de métricas que originou a transição.
4. A equipe usa o painel para confirmar que o serviço se estabilizou, sem precisar intervir manualmente.

**Resultado:** o tempo de inatividade passa de minutos para segundos, e a equipe ganha visibilidade do que causou o problema — sem precisar investigar logs manualmente.

---

## Estrutura do Projeto

```
netguard-pro/
├── api/              # Endpoints REST e lógica de autenticação
├── monitor/          # Coleta de métricas (CPU, memória, disco, rede)
├── failover/         # Lógica de detecção e transição automática
├── firewall/         # Motor de regras e validação
├── dashboard/        # Frontend do painel (React)
├── docs/             # Documentação técnica detalhada
├── tests/            # Testes automatizados
└── docker-compose.yml
```

Cada módulo tem seu próprio `README.md` com detalhes de implementação. Comece por `monitor/` e `api/` se for sua primeira contribuição — são os módulos mais bem documentados.

---

## Para Desenvolvedores: Integração via API

A API REST permite consultar métricas e gerenciar configurações programaticamente.

```bash
curl -X GET "https://api.netguardpro.com/v1/metrics?server=srv-01" \
  -H "Authorization: Bearer SEU_TOKEN_AQUI"
```

Resposta esperada:

```json
{
  "server": "srv-01",
  "cpu_usage": 68.4,
  "latency_ms": 112.3,
  "packet_loss": 0.4
}
```

Documentação completa de endpoints, autenticação e limites de requisição: [`docs/api.md`](docs/api.md).

---

## Como Contribuir

1. **Abra uma issue** descrevendo o bug ou a melhoria antes de começar a codificar — isso evita trabalho duplicado.
2. **Crie um branch** a partir de `main`: `feature/nome-da-funcionalidade` ou `fix/nome-do-bug`.
3. **Siga o padrão de código** do projeto: ESLint para o frontend (`dashboard/`), PEP 8 para os módulos em Python (`monitor/`, `failover/`).
4. **Escreva testes** para qualquer nova funcionalidade ou correção (`tests/`).
5. **Abra um Pull Request** com:
   - Descrição clara do que foi alterado e por quê
   - Referência à issue relacionada
   - Confirmação de que os testes passam (`docker compose run tests`)
6. Um mantenedor revisará o PR em até 3 dias úteis.

Guia completo de estilo de código: [`docs/contributing.md`](docs/contributing.md).

---

## Solução de Problemas Comuns

| Problema | Causa provável | O que fazer |
| --- | --- | --- |
| Painel lento sob alta carga | Uso de CPU elevado durante análises avançadas | Reduza a frequência de atualização do painel em `Configurações > Desempenho` |
| Configuração de firewall confusa | Curva de aprendizado da interface de regras | Use o assistente de configuração guiada em `Firewall > Novo Assistente` |
| Excesso de alertas de segurança | Eventos de baixa prioridade sendo notificados | Ajuste os níveis de severidade em `Alertas > Prioridades` |
| Atraso em transferências grandes de dados | Congestionamento de banda em picos de tráfego | Habilite priorização manual em `Largura de Banda > Regras` |

---

## Suporte

- **Documentação completa:** [`docs/`](docs/)
- **Central de Ajuda:** suporte.netguardpro.com
- **Reportar um bug:** abra uma issue neste repositório
- **Suporte técnico urgente:** suporte@netguardpro.com

---

## Licença

Este projeto é distribuído sob a licença MIT. Veja [`LICENSE`](LICENSE) para detalhes.
