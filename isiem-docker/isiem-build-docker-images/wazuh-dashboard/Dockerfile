# Wazuh Docker Copyright (C) 2017, Wazuh Inc. (License GPLv2)
FROM amazonlinux:2023 AS builder

ARG WAZUH_VERSION
ARG WAZUH_TAG_REVISION
ARG WAZUH_UI_REVISION
ARG INSTALL_DIR=/usr/share/wazuh-dashboard

# Update and install dependencies
RUN yum install curl-minimal libcap openssl -y

COPY config/check_repository.sh /
RUN chmod 775 /check_repository.sh && \
    source /check_repository.sh

RUN yum install wazuh-dashboard-${WAZUH_VERSION}-${WAZUH_TAG_REVISION} -y && \
    yum clean all

# Rename wazuh index patterns to isiem
RUN sed -i "s/'wazuh-alerts-'/'isiem-alerts-'/g; \
            s/'wazuh-alerts-\*'/'isiem-alerts-*'/g; \
            s/'wazuh-monitoring-'/'isiem-monitoring-'/g; \
            s/'wazuh-monitoring-\*'/'isiem-monitoring-*'/g; \
            s/'wazuh-states-/'isiem-states-/g; \
            s/'wazuh-alerts-4\.x-'/'isiem-alerts-4.x-'/g; \
            s/'wazuh-statistics-'/'isiem-statistics-'/g; \
            s/dataSet: 'wazuh-alerts'/dataSet: 'isiem-alerts'/g; \
            s/WAZUH_STATISTICS_DEFAULT_PREFIX = exports.WAZUH_STATISTICS_DEFAULT_PREFIX = 'wazuh'/WAZUH_STATISTICS_DEFAULT_PREFIX = exports.WAZUH_STATISTICS_DEFAULT_PREFIX = 'isiem'/g" \
      /usr/share/wazuh-dashboard/plugins/wazuh/common/constants.js && \
    sed -i 's/wazuh-alerts/isiem-alerts/g; s/wazuh-monitoring/isiem-monitoring/g; s/wazuh-states-/isiem-states-/g; s/wazuh-statistics-/isiem-statistics-/g' \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/start/cron-scheduler/scheduler-handler.js && \
    sed -i 's/wazuh-alerts/isiem-alerts/g; s/wazuh-monitoring/isiem-monitoring/g; s/wazuh-states-/isiem-states-/g; s/wazuh-statistics-/isiem-statistics-/g' \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/start/monitoring/index.js && \
    sed -i 's/wazuh-alerts/isiem-alerts/g; s/wazuh-monitoring/isiem-monitoring/g; s/wazuh-states-/isiem-states-/g; s/wazuh-statistics-/isiem-statistics-/g' \
      /usr/share/wazuh-dashboard/plugins/wazuh/target/public/wazuh.chunk.2.js && \
    sed -i 's/wazuh-alerts/isiem-alerts/g; s/wazuh-monitoring/isiem-monitoring/g; s/wazuh-states-/isiem-states-/g; s/wazuh-statistics-/isiem-statistics-/g' \
      /usr/share/wazuh-dashboard/plugins/wazuh/target/public/wazuh.plugin.js

# Fix sample-data dataset files to prevent wazuh-states-* index patterns from being recreated
RUN sed -i 's/wazuh-states-/isiem-states-/g; s/wazuh-alerts/isiem-alerts/g; s/wazuh-archives/isiem-archives/g; s/wazuh-monitoring/isiem-monitoring/g; s/wazuh-statistics/isiem-statistics/g' \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-hardware/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-hardware/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-system/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-system/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-vulnerabilities/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-vulnerabilities/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-groups/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-groups/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-packages/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-packages/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-ports/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-ports/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-processes/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-processes/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-users/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-users/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-networks/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-networks/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-interfaces/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-interfaces/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-protocols/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-protocols/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-services/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-services/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-hotfixes/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-hotfixes/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-browser-extensions/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-inventory-browser-extensions/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-fim-files/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-fim-files/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-fim-registries/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/states-fim-registries/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/wazuh-alerts/template.json \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/wazuh-alerts/main.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/dataset/shared-utils.js \
      /usr/share/wazuh-dashboard/plugins/wazuh/server/lib/sample-data/index.js

# Create and set permissions to data directories
RUN mkdir -p $INSTALL_DIR/data/wazuh && chmod -R 775 $INSTALL_DIR/data/wazuh
RUN mkdir -p $INSTALL_DIR/data/wazuh/config && chmod -R 775 $INSTALL_DIR/data/wazuh/config
RUN mkdir -p $INSTALL_DIR/data/wazuh/logs && chmod -R 775 $INSTALL_DIR/data/wazuh/logs
COPY config/wazuh.yml $INSTALL_DIR/data/wazuh/config/
RUN setcap 'cap_net_bind_service=-ep' /usr/share/wazuh-dashboard/node/bin/node
RUN setcap 'cap_net_bind_service=-ep' /usr/share/wazuh-dashboard/node/fallback/bin/node

# Generate certificates
COPY config/config.sh .
COPY config/config.yml /
RUN bash config.sh

################################################################################
# Build stage 1 (the current Wazuh dashboard image):
#
# Copy wazuh-dashboard from stage 0
# Add entrypoint
# Add wazuh_app_config
################################################################################
FROM amazonlinux:2023

ENV USER="wazuh-dashboard" \
    GROUP="wazuh-dashboard" \
    NAME="wazuh-dashboard" \
    INSTALL_DIR="/usr/share/wazuh-dashboard"

ENV PATTERN="" \
    CHECKS_PATTERN="" \
    CHECKS_TEMPLATE="" \
    CHECKS_API="" \
    CHECKS_SETUP="" \
    APP_TIMEOUT="" \
    API_SELECTOR="" \
    IP_SELECTOR="" \
    IP_IGNORE="" \
    WAZUH_MONITORING_ENABLED="" \
    WAZUH_MONITORING_FREQUENCY="" \
    WAZUH_MONITORING_SHARDS="" \
    WAZUH_MONITORING_REPLICAS=""

RUN yum install shadow-utils -y

RUN getent group $GROUP || groupadd -r -g 1000 $GROUP
RUN useradd --system \
            --uid 1000 \
            --no-create-home \
            --home-dir $INSTALL_DIR \
            --gid $GROUP \
            --shell /sbin/nologin \
            --comment "$USER user" \
            $USER

COPY config/entrypoint.sh /
COPY config/wazuh_app_config.sh /
RUN chmod 700 /entrypoint.sh
RUN chmod 700 /wazuh_app_config.sh
RUN chown 1000:1000 /*.sh

COPY --from=builder --chown=1000:1000 $INSTALL_DIR $INSTALL_DIR

RUN mkdir -p /usr/share/wazuh-dashboard/plugins/wazuh/public/assets/custom
RUN chown 1000:1000 /usr/share/wazuh-dashboard/plugins/wazuh/public/assets/custom

WORKDIR $INSTALL_DIR
USER wazuh-dashboard

EXPOSE 443

ENTRYPOINT [ "/entrypoint.sh" ]
