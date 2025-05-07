# Base oficial do Keycloak
FROM quay.io/keycloak/keycloak:26.2.3

# RUN /opt/keycloak/bin/kc.sh build
# COPY conf/keycloak.conf /opt/keycloak/conf/

# (Opcional) Adicione configurações personalizadas:
# - Plugins: COPY plugins/*.jar /opt/keycloak/providers/
# - Temas: COPY themes/ /opt/keycloak/themes/

# Defina variáveis de ambiente padrão (não sensíveis!)
ENV KC_HEALTH_ENABLED=true
ENV KC_METRICS_ENABLED=true

# Comando padrão (sobrescrito pelo docker-compose)
CMD ["start-dev"]