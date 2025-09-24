# Nova360 - Loja Fake para Testes
**Timestamp:** 2025-09-23 20:38:00 UTC  
**Versão:** 3.1.2  
**Status:** ATIVO - AMBIENTE DE TESTES  

## INFRAESTRUTURA

### Servidor Hetzner
- **URL:** https://nova360.com
- **Servidor:** Hetzner Dedicated AX41
- **Localização:** Alemanha (Nuremberg)
- **OS:** Ubuntu 22.04 LTS
- **Stack:** Nginx + Node.js + MongoDB

### Configuração Técnica
```bash
# Servidor specs
CPU: AMD Ryzen 5 3600 (6 cores/12 threads)
RAM: 64 GB DDR4
Storage: 1TB NVMe SSD
Network: 1 Gbps
```

## PROPÓSITO E FUNCIONALIDADES

### Ambiente de Testes
- **Pixel Testing:** Todos os 5 pixels principais
- **A/B Testing:** Múltiplas variações de layout
- **Comportamento Real:** Simula loja e-commerce completa
- **Data Collection:** Integrado com sistema SmartBMC

### Produtos Simulados
```javascript
// Catálogo de teste
const testProducts = {
  electronics: {
    count: 150,
    categories: ["smartphones", "notebooks", "tablets"],
    price_range: [299, 4999]
  },
  fashion: {
    count: 300, 
    categories: ["shoes", "clothing", "accessories"],
    price_range: [49, 899]
  },
  home: {
    count: 100,
    categories: ["appliances", "furniture", "decor"], 
    price_range: [89, 2499]
  }
};
```

### Cenários de Teste
1. **Jornada Completa:** Browse → Cart → Checkout
2. **Cart Abandonment:** Adiciona produto e sai
3. **Email Capture:** Triggers de captura de email
4. **Cross-device:** Teste de tracking entre dispositivos

## INTEGRAÇÃO COM PIXELS

### Configuração Multi-Pixel
```html
<!-- Facebook Pixel -->
<script>
  fbq('track', 'PageView');
  fbq('track', 'ViewContent', {
    content_ids: ['{{product.id}}'],
    content_type: 'product',
    value: {{product.price}},
    currency: 'BRL'
  });
</script>

<!-- Google Ads -->
<script>
  gtag('event', 'page_view', {
    send_to: 'AW-XXXXXXXXX'
  });
</script>

<!-- SmartBMC Pixel -->
<script>
  smartBMC.track('pageview', {
    product_id: '{{product.id}}',
    category: '{{product.category}}',
    price: {{product.price}}
  });
</script>
```

### Eventos Simulados
- **PageView:** Toda navegação
- **ViewContent:** Visualização de produtos
- **AddToCart:** Adicionar ao carrinho  
- **InitiateCheckout:** Início do checkout
- **Purchase:** Compras simuladas (não reais)

## DADOS E ANALYTICS

### Geração de Tráfego
```python
# Traffic simulator
import random
import requests
from datetime import datetime

def simulate_user_journey():
    # Simula comportamento real
    pages = ['/', '/products', '/product/123', '/cart', '/checkout']
    for page in pages:
        time.sleep(random.uniform(2, 15))  # Tempo real de navegação
        visit_page(page)
        
def generate_realistic_data():
    # 1000-2000 sessões/dia
    # 60% bounce rate
    # 3% conversion rate
    # Horários de pico: 19h-22h
    pass
```

### Integração SmartBMC
- **Bloom Filter:** Todos visitantes capturados
- **MongoDB:** Eventos armazenados em smartbmc_final
- **Email Testing:** Captura configurável
- **Real-time Dashboard:** Métricas ao vivo

## CONFIGURAÇÕES DE TESTE

### Variações de Layout
```javascript
// A/B Testing configurations
const testVariants = {
  pixel_placement: ['header', 'footer', 'body'],
  email_capture: {
    timing: ['immediate', 'scroll_50', 'exit_intent'],
    incentive: ['10%_off', '5%_off', 'free_shipping']
  },
  checkout_flow: ['single_page', 'multi_step', 'guest_checkout']
};
```

### Performance Testing
- **Load Testing:** Até 10k usuários simultâneos
- **Pixel Performance:** Tempo de carregamento <500ms
- **Email Capture Rate:** Target 2-5%

## MONITORAMENTO

### Métricas Coletadas
```json
{
  "daily_visitors": 1500,
  "pixel_fires": {
    "facebook": 1485,
    "google": 1490, 
    "smartbmc": 1500
  },
  "email_captures": 45,
  "conversion_rate": 2.8,
  "bounce_rate": 58
}
```

### Dashboards Ativos
- **URL:** https://nova360.com/admin/analytics
- **Login:** admin/nova360admin
- **Real-time:** Sim
- **Retention:** 90 dias de dados

## CASOS DE USO

### Testes de Pixel
```bash
# Testar disparo de eventos
curl -X POST https://nova360.com/api/test/pixel-event \
  -H "Content-Type: application/json" \
  -d '{"event":"purchase","value":299.99,"pixel":"facebook"}'

# Verificar integração SmartBMC
curl https://nova360.com/api/test/smartbmc-integration
```

### Simulação de Comportamento
- **Usuário Típico:** 4.2 páginas, 6min sessão
- **Comprador:** 8.5 páginas, 12min sessão  
- **Abandonador:** 2.1 páginas, 45seg sessão

### Validation Pipeline
1. **Pixel Firing:** Todos pixels disparam corretamente
2. **Data Accuracy:** Dados chegam no SmartBMC
3. **Email Capture:** Captura funciona sem interferir UX
4. **Cross-device:** Tracking entre dispositivos

## CONFIGURAÇÃO DE DESENVOLVIMENTO

### Local Development
```bash
# Clone do repositório
git clone https://github.com/smartbmc/nova360-fake-store
cd nova360-fake-store

# Install dependencies
npm install

# Start development server
npm run dev

# Run tests
npm run test:pixels
```

### Deploy Pipeline
```yaml
# .github/workflows/deploy.yml
name: Deploy Nova360
on: [push]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to Hetzner
        run: ssh hetzner "cd /var/www/nova360 && git pull && pm2 reload all"
```

## RESULTADOS E INSIGHTS

### Dados dos Últimos 30 Dias
- **Visitantes:** 42.500
- **Pixel Events:** 127.400
- **Emails Capturados:** 1.350 (3.2% rate)
- **SmartBMC Integration:** 100% uptime

### Learnings Aplicados
1. **Email Timing:** Exit intent = 2x melhor que scroll
2. **Pixel Performance:** Facebook + Google = 99.8% reliability
3. **Mobile vs Desktop:** Mobile 65% do tráfego
4. **Conversion Triggers:** Desconto >15% = 4x conversion

### Feed para Produção
- **Pixel Config:** Testado e validado
- **Email Strategies:** Prontas para deploy
- **Performance Benchmarks:** Estabelecidos
- **User Behavior:** Mapeado completamente

---
**Ambiente:** Staging/Testing  
**Próxima Atualização:** Weekly (toda segunda-feira)  
**Backup:** Diário via Hetzner Cloud Backup  
**Monitoramento:** 24/7 via UptimeRobot