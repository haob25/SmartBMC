# OfertasBMC - Sistema Agregador de Ofertas
**Timestamp:** 2025-09-23 20:42:00 UTC  
**Versão:** 2.3.1  
**Status:** DESENVOLVIMENTO - REATIVAÇÃO  

## INFRAESTRUTURA

### Domínio e Branding
- **URL:** https://ofertasbmc.com.br
- **Status:** Marca reconhecida no mercado brasileiro
- **Base de Usuários:** 520k emails (120k ativos + 400k históricos)
- **Reputação:** Estabelecida desde 2018

### Servidor e Stack
- **Hosting:** A definir (AWS vs Hetzner)
- **Stack Planejada:** Node.js + React + MongoDB
- **CDN:** CloudFlare para performance global
- **Search Engine:** Elasticsearch para busca rápida

## ESTRATÉGIA DE MONETIZAÇÃO

### Modelo de Receita
```javascript
const revenueStreams = {
  affiliate_commission: {
    source: ["AWIN", "CJ Affiliate", "Amazon", "AliExpress"],
    target: "70% da receita",
    commission_rate: "3-8%"
  },
  email_marketing: {
    audience: 520000,
    engagement_target: "15-20%",
    campaigns_per_week: 4
  },
  premium_subscriptions: {
    price: "R$ 29.90/mês",
    target_subscribers: 500,
    revenue_target: "R$ 15k/mês"
  }
};
```

### Projeção de Receita (6 meses)
- **Mês 1-2:** R$ 10-15k (reativação)
- **Mês 3-4:** R$ 30-50k (crescimento orgânico)
- **Mês 5-6:** R$ 80-120k (otimização completa)

## ARQUITETURA DE SISTEMA

### SKU Universal
```json
{
  "sku_universal": "IPHONE-15-PRO-256-BLK",
  "product_name": "iPhone 15 Pro Max 256GB Preto",
  "category": "smartphones",
  "brand": "Apple",
  "stores": [
    {
      "store": "magazineluiza",
      "sku_store": "ML-IP15PM256B",
      "price": 6999.00,
      "url": "https://magazineluiza.com.br/...",
      "last_updated": "2025-09-23T20:30:00Z"
    },
    {
      "store": "amazon",
      "sku_store": "B0C1J8N9XY",
      "price": 7299.00,
      "url": "https://amazon.com.br/...",
      "affiliate_link": "https://amzn.to/3xyz..."
    }
  ],
  "best_price": {
    "store": "magazineluiza",
    "price": 6999.00,
    "savings": 300.00
  },
  "price_alerts": 156,
  "trending_score": 8.7
}
```

### Microserviços Integrados
- **Price Monitor:** Scraping + API feeds
- **Alert System:** Email + WhatsApp + SMS
- **User Management:** Cadastros + segmentação
- **Analytics:** Comportamento + performance

## FUNCIONALIDADES PRINCIPAIS

### 1. Comparador de Preços
- **Busca Universal:** SKU único para múltiplas lojas
- **Histórico de Preços:** Gráficos de variação
- **Alerta de Queda:** Notifications push + email
- **Mobile First:** PWA responsivo

### 2. Sistema de Alertas
```python
# Alert triggers
alert_types = {
    "price_drop": {
        "threshold": "10% ou R$ 50",
        "delivery": ["email", "whatsapp", "push"],
        "frequency": "imediato"
    },
    "stock_alert": {
        "trigger": "produto volta ao estoque",
        "delivery": ["email", "sms"]
    },
    "best_deal": {
        "trigger": "menor preço histórico",
        "priority": "alta"
    }
}
```

### 3. Curadoria de Ofertas
- **Editorial:** Top 10 ofertas do dia
- **Trending:** Produtos mais buscados
- **Seasonal:** Black Friday, Natal, Dia das Mães
- **Categories:** Eletrônicos, Moda, Casa, Esportes

## INTEGRAÇÃO COM SMARTBMC

### Data Pipeline
```
SmartBMC (320M hashes) → OfertasBMC → Email Personalizado
```

### Personalização Avançada
- **Behavioral Targeting:** Produtos vistos em outras lojas
- **Cross-device:** Sincronização entre dispositivos
- **Predictive:** Machine learning para sugestões

### Email Marketing
```javascript
// Segmentação inteligente
const emailSegments = {
  hot_leads: {
    criteria: "visited_target_products_last_7_days",
    size: 50000,
    conversion_rate: "8-12%"
  },
  price_sensitive: {
    criteria: "clicked_discount_above_30%",
    size: 120000,
    conversion_rate: "4-6%"
  },
  category_focused: {
    criteria: "electronics_buyers",
    size: 80000,
    conversion_rate: "6-8%"
  }
};
```

## STACK TECNOLÓGICA

### Frontend
- **Framework:** Next.js 14 + TypeScript
- **UI Library:** Tailwind CSS + Headless UI
- **State Management:** Zustand
- **PWA:** Service Workers + Push notifications

### Backend
- **API:** Node.js + Fastify
- **Database:** MongoDB (compartilhado com SmartBMC)
- **Cache:** Redis (Bloom filter integration)
- **Search:** Elasticsearch + Algolia

### DevOps
- **Containerization:** Docker + Kubernetes
- **CI/CD:** GitHub Actions
- **Monitoring:** DataDog + Sentry
- **CDN:** CloudFlare + AWS CloudFront

## ESTRATÉGIA DE REATIVAÇÃO

### Fase 1 - Soft Launch (Mês 1)
```bash
# Reativar 50k emails mais engajados
target_audience = hot_leads[0:50000]
campaign_frequency = "2x por semana"
content_focus = "top 5 ofertas verificadas"
```

### Fase 2 - Scale Up (Mês 2-3)
- **Audience:** 150k emails
- **Frequency:** Daily digest
- **Features:** Alertas personalizados
- **Content:** 50+ produtos monitorados

### Fase 3 - Full Operation (Mês 4+)  
- **Audience:** 400k+ emails
- **Organic Traffic:** SEO + social media
- **Premium Features:** Subscription model
- **B2B:** API para outras empresas

## MÉTRICAS E KPIs

### Performance Targets
```json
{
  "email_marketing": {
    "open_rate": "20-25%",
    "click_rate": "4-6%", 
    "conversion_rate": "1-2%",
    "unsubscribe_rate": "<0.5%"
  },
  "website": {
    "monthly_visitors": "500k+",
    "bounce_rate": "<40%",
    "session_duration": "3+ minutes",
    "pages_per_session": "4+"
  },
  "business": {
    "monthly_revenue": "R$ 100k+",
    "customer_acquisition_cost": "<R$ 25",
    "lifetime_value": "R$ 150+",
    "roi": "5-10x"
  }
}
```

### Analytics Integration
- **Google Analytics 4:** Comportamento completo
- **Mixpanel:** Events tracking
- **Hotjar:** Heatmaps + recordings
- **Custom Dashboard:** Métricas de negócio

## COMPLIANCE E SEGURANÇA

### LGPD Compliance
- **Consent Management:** Cookie banner + preferences
- **Data Retention:** 24 meses para inativos
- **Right to Delete:** Automatizado via API
- **Privacy Policy:** Atualizada e transparente

### Segurança
- **SSL:** Let's Encrypt + Cloudflare
- **Authentication:** JWT + 2FA opcional
- **Rate Limiting:** Por IP e usuário
- **Data Encryption:** Em trânsito e repouso

## ROADMAP DE DESENVOLVIMENTO

### Q4 2025
- [x] Documentação completa
- [ ] MVP frontend (4 semanas)
- [ ] API básica (3 semanas)
- [ ] Integração SmartBMC (2 semanas)
- [ ] Soft launch (50k emails)

### Q1 2026
- [ ] Mobile app (iOS/Android)
- [ ] API pública para parceiros
- [ ] Machine Learning recommendations
- [ ] Expansão para 20+ lojas

### Q2 2026
- [ ] Premium subscriptions
- [ ] WhatsApp integration
- [ ] Voice search (Alexa/Google)
- [ ] International expansion

---
**Owner:** SmartBMC Team  
**Stakeholders:** Email list + business partners  
**Budget:** R$ 50-100k desenvolvimento inicial  
**Launch Target:** 2025-12-01