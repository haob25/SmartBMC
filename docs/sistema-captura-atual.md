# SmartBMC - Sistema de Captura Atual
**Timestamp:** 2025-09-23 20:30:00 UTC  
**Versão:** 4.2.1  
**Status:** PRODUÇÃO ATIVA  

## INFRAESTRUTURA ATUAL

### Servidor Principal (AWS SP)
- **IP:** 56.125.127.143
- **Instância:** i-0061f98b7d7ff5203
- **Conta AWS:** 565386896996
- **SSH Alias:** sshwe
- **Região:** São Paulo

### Base de Dados
- **MongoDB:** smartbmc_final
- **Registros:** 10.5M+ (crescendo)
- **Captura Rate:** ~2.000/minuto
- **Collections:**
  - `traffic_unknown_correct`: Tráfego não identificado
  - `traffic_known_correct`: Tráfego com email identificado

## SERVIÇOS EM EXECUÇÃO

### 1. Sistema de Captura Principal
```bash
# Processo: capture_service.py
PID: 7817
CPU: 2.5%
RAM: 30MB
Status: Auto-restart configurado
Comando: /usr/bin/python3 /root/smartbmc_production/definitivo/capture_service.py
```

### 2. Sistema de Tracking
```bash
# Processo: app.js
PID: 1866
CPU: 0.3%
RAM: 58MB
Comando: node /root/smartbmc_production/tracking_system/app.js
```

### 3. Monitor do Sistema
```bash
# Processo: smartbmc_monitor_final.py
PID: 2682
CPU: 0.1%
RAM: 26MB
Comando: /usr/bin/python3 /root/smartbmc_monitor_final.py
```

## ARQUITETURA DE CAPTURA

### Fluxo de Dados
1. **Pixel/Tracking** → Coleta inicial
2. **Redis Bloom Filter** → Deduplicação (320M+ hashes)
3. **MongoDB** → Armazenamento persistente
4. **Classificação** → Conhecido vs Desconhecido

### Métricas de Performance (Últimos 15 dias)
- **Total Capturado:** 32.234.780 registros
- **Taxa Identificação:** 0.404%
- **Emails Únicos:** 44.413
- **Crescimento:** +60.9% semana 2 vs semana 1

## COMANDOS DE VERIFICAÇÃO

### Status em Tempo Real
```bash
# Captura no último minuto
mongosh smartbmc_final --eval "
var m=new Date(Date.now()-60000); 
print('Capturados último minuto: ' + 
db.traffic_unknown_correct.countDocuments({processed_at:{\$gte:m}}))
"

# Emails identificados hoje
mongosh smartbmc_final --eval "
var hoje = new Date();
hoje.setHours(0,0,0,0);
print('Emails identificados hoje: ' + 
db.traffic_known_correct.countDocuments({processed_at:{\$gte:hoje}}))
"
```

### Health Check
```bash
# Verificar serviços
ps aux | grep -E 'app.js|capture_service|monitor' | grep -v grep

# Verificar logs
tail -f /var/log/smartbmc_monitor.log
```

## CONFIGURAÇÕES

### MongoDB Indexes
- `processed_at_1`: Index por timestamp
- `email_1`: Index por email (quando conhecido)
- `session_hash_1`: Index por sessão

### Rate Limiting
- **Coleta:** 2.000 registros/minuto
- **Processamento:** Assíncrono via queue
- **Bloom Filter:** O(1) lookup

## PRÓXIMAS ATUALIZAÇÕES

### Melhorias Planejadas
- [ ] Aumento para 5.000 registros/minuto
- [ ] Integração com sistema de retargeting
- [ ] Dashboard de métricas em tempo real
- [ ] Backup automatizado para S3

### Dependências
- MongoDB 7.0+
- Redis 7.0+
- Python 3.9+
- Node.js 18+

---
**Mantido por:** Sistema SmartBMC  
**Última Verificação:** 2025-09-23 20:17:00 UTC