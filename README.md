# DevBoost PIX Gateway

**Pare de perder dias integrando PIX. Entregue em horas.**

> Sistema completo, self-hosted, pronto para produção — você instala, configura e já está gerando cobranças PIX reais.

---

## O problema que isso resolve

Integrar PIX diretamente com os bancos é trabalhoso: OAuth2, mTLS, certificados digitais, CSR, ambientes de sandbox, formatos diferentes por banco, tratamento de erros, cache de token, renovação automática...

Tudo isso consome dias de desenvolvimento — às vezes semanas — antes de você cobrar o primeiro centavo do cliente.

O **DevBoost PIX Gateway** já tem tudo isso resolvido e testado em produção. Você recebe o código-fonte completo, instala no servidor do cliente em minutos e começa a integrar pelo endpoint REST imediatamente.

---

## Screenshots

| Dashboard | Configurar Bancos |
|---|---|
| ![Dashboard](gateway-pi-dashboard.png) | ![Configurar](gateway-pi-configurar.png) |

| Teste de Conexão em Tempo Real | Testar PIX — QR Code Real |
|---|---|
| ![Testar Conexão](gateway-pi-teste-conexao.png) | ![Testar PIX](gateway-pi-teste-pix.png) |

| Histórico de Transações | Documentação da API Integrada |
|---|---|
| ![Transações](gateway-pi-transacoes.png) | ![Documentação](gateway-pi-documentacao.png) |

---

## Bancos suportados

| Banco | Status | Autenticação |
|---|---|---|
| **Itaú Unibanco** | ✅ Produção | OAuth2 + mTLS |
| **Santander** | ✅ Produção | OAuth2 + mTLS |
| **Sicredi** | ✅ Produção | OAuth2 + mTLS |
| **Bradesco** | 🔧 Em breve | — |

---

## O que você NÃO vai precisar implementar do zero

- Fluxo OAuth2 com renovação automática de token ✅
- mTLS com certificados digitais por banco ✅
- Geração de TxID, QR Code e Pix Copia e Cola ✅
- Cache de token para evitar chamadas desnecessárias ao banco ✅
- Upload e gerenciamento de certificados digitais ✅
- Diferenças de API entre Itaú, Santander e Sicredi ✅
- Tratamento de erros, retentativas e logs ✅

---

## O que está incluído

- **Painel de Administração** (React + Tailwind) — configure credenciais, faça upload de certificados e monitore tudo via browser, sem mexer em arquivo de config
- **API PIX completa** — endpoints REST para gerar, consultar e cancelar cobranças
- **Teste de conexão em tempo real** — terminal interativo que autentica com o banco e valida certificados antes de ir para produção, sem precisar subir código de teste
- **Documentação da API integrada** — exemplos em cURL, JavaScript e PHP prontos para copiar
- **Guias de configuração por banco** — passo a passo para obter credenciais no portal de cada banco (Itaú, Santander, Sicredi)
- **Histórico de transações** — consulte todas as cobranças geradas, filtradas por banco e status
- **Docker incluso** — sobe o ambiente completo com `docker-compose up` para desenvolver localmente
- **Código-fonte 100% seu** — sem ofuscação, sem licença de runtime, sem dependência de servidor externo

---

## Como funciona

```
Seu sistema  →  POST /api_pix/endpoints/gerar_pix.php
                  ↓
            PIX Gateway (seu servidor)
                  ↓
            API do banco (Itaú, Santander, Sicredi...)
                  ↓
            QR Code + Copia e Cola retornados
```

Uma única chamada HTTP com `banco_codigo`, `valor` e `descricao`. O gateway cuida de tudo: autenticação OAuth2, renovação de token, mTLS com o certificado certo, geração do txid e retorno do QR Code — sem você precisar saber como cada banco funciona por baixo.

---

## Exemplo de integração

```bash
curl -X POST https://seudominio.com/api_pix/endpoints/gerar_pix.php \
  -H "Content-Type: application/json" \
  -H "X-API-Key: SUA_API_KEY" \
  -d '{
    "banco_codigo": "itau",
    "valor": 150.00,
    "descricao": "Pedido #12345"
  }'
```

```json
{
  "sucesso": true,
  "mensagem": "PIX gerado com sucesso",
  "dados": {
    "txid": "ABC123...",
    "valor": 150.00,
    "qr_code_base64": "iVBORw0KGgo...",
    "pix_copia_cola": "00020101021226...",
    "status": "ATIVA",
    "expiracao": "2026-05-07T15:30:00-03:00"
  }
}
```

---

## Requisitos do servidor

- PHP 7.4+ com extensões: `openssl`, `pdo_mysql`, `curl`
- MySQL 5.7+ ou MariaDB 10.3+
- Apache ou Nginx (vhost incluso)
- Certificados mTLS fornecidos pelo portal do seu banco

Ou simplesmente use o **Docker incluso** — zero configuração manual.

---

## O que você NÃO paga mais

| Custo eliminado | Estimativa mensal |
|---|---|
| Taxa por transação (2~3%) | Variável — proporcional ao seu faturamento |
| Plano de gateway (PagSeguro, Pagar.me etc.) | R$ 0 a R$ 500+/mês |
| Dependência de terceiros para ficar no ar | Priceless |

---

## Para quem é

✅ **Desenvolvedor PHP** que quer entregar integração PIX em horas, não em dias  
✅ **Freelancer ou agência** que atende múltiplos clientes com contas em bancos diferentes  
✅ **SaaS ou e-commerce** que quer eliminar a taxa por transação de gateways de terceiros  
✅ **Empresa** que precisa de controle total sobre o fluxo de pagamento PIX

---

## Licença

Licença vitalícia — pague uma vez, use para sempre, em quantos projetos quiser.  
Código-fonte completo entregue sem restrições de runtime ou assinatura.

---

## O que você ganha de verdade

Não é só código. É o tempo que você **não vai gastar** lendo documentação de API de banco, depurando erro de certificado mTLS, descobrindo por que o token expirou ou entendendo por que o Sicredi tem um fluxo diferente do Itaú.

Isso está resolvido. Você chega, configura as credenciais no painel, faz o upload do certificado, testa a conexão e começa a integrar.

---

*DevBoost — ferramentas para desenvolvedores que precisam de produção, não de promessa.*
