# Usar Ubuntu 18.04 (LTS) como base. Importante la versión 18.04 para evitar incompatibilidades de versiones superiores de python3
FROM ubuntu:18.04

# Evitar que se soliciten interacciones durante la construcción
ENV DEBIAN_FRONTEND=noninteractive

EXPOSE 25

VOLUME ["/var/log", "/var/spool/postfix"]

# Actualizar e instalar paquetes necesarios
RUN apt-get update && \
    apt-get install -y telnet dnsutils vim python3.6 python3-pip postfix sasl2-bin libsasl2-modules mailutils && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Instalar chaperone usando pip. 
# Importante instalar estas versiones porque hay incompatibilidades con las python3.6 en las versiones recientes
RUN python3.6 -m pip install chaperone==0.3.9 PyYAML==5.2 voluptuous==0.11.7

# Copiar la configuración de chaperone y el script setup.sh
RUN mkdir -p /etc/chaperone.d
COPY chaperone.conf /etc/chaperone.d/chaperone.conf

# Copiar resolv.conf al chroot de Postfix
RUN mkdir -p /var/spool/postfix/etc && cp /etc/resolv.conf /var/spool/postfix/etc/

COPY setup.sh /setup.sh
RUN chmod +x /setup.sh

ENTRYPOINT ["/usr/local/bin/chaperone"]