# Retarget - Sistema de Microserviços
**Timestamp:** 2025-09-23 20:35:00 UTC  
**Versão:** 1.0.0-beta  
**Status:** DESENVOLVIMENTO ATIVO  

## ARQUITETURA MICROSERVIÇOS

### Container Stack
```yaml
version: '3.8'
services:
  pixel-manager:
    image: smartbmc/pixel-manager:latest
    ports: ["3001:3001"]
    env: ["PIXEL_CONFIG=multi"]
    
  email-capture:
    image: smartbmc/email-capture:latest  
    ports: ["3002:3002"]
    depends_on: ["redis", "mongodb"]
    
  audience-builder:
    image: smartbmc/audience-builder:latest
    ports: ["3003:3003"]
    
  campaign-manager:
    image: smartbmc/campaign-manager:latest
    ports: ["3004:3004"]
```

### Microserviços Planejados

#### 1. Pixel Manager Service
- **Responsabilidade:** Gerenciar múltiplos pixels
- **Pixels Suportados:** Facebook, Google Ads, TikTok, Pinterest, SmartBMC
- **Containers:** Docker + Kubernetes ready
- **API:** REST + GraphQL

#### 2. Email Capture Service
- **Estratégia:** Progressive disclosure
- **Triggers:** Cart abandonment, exit intent, scroll depth
- **Integration:** Bloom filter + MongoDB
- **Rate:** Controlado por AI Council

#### 3. Audience Builder Service
- **Segmentação:** Behavioral + demographic
- **Real-time:** WebSocket connections
- **ML Pipeline:** TensorFlow Serving
- **Export:** Facebook/Google audiences

#### 4. Campaign Manager Service  
- **Multi-channel:** Email + Social + Display
- **A/B Testing:** Built-in
- **Attribution:** Cross-device tracking
- **ROI Tracking:** Real-time

## INFRAESTRUTURA CONTAINER

### Desenvolvimento
- **Local:** Docker Compose
- **Registry:** AWS ECR
- **Orchestration:** Kubernetes (planejado)
- **CI/CD:** GitHub Actions

### Servidor Hetzner (Staging)
```bash
# Containers ativos
docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"

# Logs dos serviços
docker logs pixel-manager-staging
docker logs email-capture-staging
```

### Servidor AWS (Produção)
- **EKS Cluster:** smartbmc-prod
- **Load Balancer:** Application LB
- **Monitoring:** CloudWatch + Prometheus

## CONFIGURAÇÃO MULTI-PIXEL

### Pixel Configuration
```javascript
// Configuração do lojista
const pixelConfig = {
  facebook: {
    enabled: true,
    pixel_id: "123456789",
    events: ["PageView", "AddToCart", "Purchase"]
  },
  google_ads: {
    enabled: true,
    conversion_id: "AW-987654321",
    events: ["page_view", "add_to_cart", "purchase"]
  },
  smartbmc: {
    enabled: true, // Sempre ativo
    capture_email: false, // Ativar quando ready
    bloom_integration: true
  }
};
```

### Deployment Strategy
1. **Blue-Green:** Zero downtime
2. **Feature Flags:** Gradual rollout  
3. **Health Checks:** Automated
4. **Rollback:** Automático se error rate >5%

## INTEGRAÇÃO COM SISTEMA PRINCIPAL

### Data Flow
```
Pixel Event → Microservice → Redis Queue → MongoDB → AI Council Decision
```

### Shared Resources
- **MongoDB:** smartbmc_final database
- **Redis:** Bloom filter + sessions
- **Kafka:** Event streaming (planejado)

## APIs E ENDPOINTS

### Pixel Manager API
```
POST /api/v1/pixel/track
GET  /api/v1/pixel/config/{store_id}
PUT  /api/v1/pixel/config/{store_id}
```

### Email Capture API  
```
POST /api/v1/capture/email
GET  /api/v1/capture/stats/{store_id}  
POST /api/v1/capture/test
```

### Audience Builder API
```
POST /api/v1/audience/create
GET  /api/v1/audience/{audience_id}
POST /api/v1/audience/export/{platform}
```

## MÉTRICAS E MONITORING

### Performance Targets
- **Latency:** <100ms (p95)
- **Throughput:** 10k req/s per service
- **Uptime:** 99.9%
- **Error Rate:** <0.1%

### Dashboards
- **Grafana:** http://56.125.127.143:3000/retarget
- **Prometheus:** Métricas personalizadas
- **Jaeger:** Distributed tracing

## CONFIGURAÇÃO DE DESENVOLVIMENTO

### Local Setup
```bash
# Clone repo
git clone https://github.com/smartbmc/retarget-microservices
cd retarget-microservices

# Start development stack
docker-compose -f docker-compose.dev.yml up -d

# Check services
curl http://localhost:3001/health
curl http://localhost:3002/health
```

### Testing
```bash
# Unit tests
npm test

# Integration tests  
npm run test:integration

# Load tests
npm run test:load
```

## ROADMAP

### Fase 1 (Atual) - MVP
- [x] Pixel Manager básico
- [x] Docker containers
- [ ] Email capture service
- [ ] Basic dashboard

### Fase 2 - Produção
- [ ] Kubernetes deployment
- [ ] Advanced segmentation  
- [ ] A/B testing framework
- [ ] Multi-tenant support

### Fase 3 - Scale
- [ ] Machine Learning integration
- [ ] Real-time personalization
- [ ] Advanced analytics
- [ ] Enterprise features

## DECISÕES DO AI COUNCIL

### Aprovadas
- **Arquitetura microserviços:** 8/9 votos
- **Docker containers:** 9/9 votos  
- **Multi-pixel approach:** 7/9 votos

### Pendentes
- **Kubernetes vs Docker Swarm:** Em votação
- **ML Pipeline integration:** Aguardando análise
- **Real-time vs Batch processing:** Discussão ativa

---
**Equipe Desenvolvimento:** SmartBMC Core Team  
**Próximo Deploy:** 2025-10-01 (Staging)  
**Produção Target:** 2025-11-01