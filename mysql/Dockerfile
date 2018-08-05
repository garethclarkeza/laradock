ARG MYSQL_VERSION=latest
FROM mysql:${MYSQL_VERSION}

LABEL maintainer="Mahmoud Zalt <mahmoud@zalt.me>"

#####################################
# Set Timezone
#####################################

RUN usermod -u 1000 mysql 
    # hack to allow access to vbox shared windows volume
#    && groupadd -g 998 vboxsf \
#    && usermod -a -G vboxsf mysql


ARG TZ=UTC
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && chown -R mysql:root /var/lib/mysql/

COPY my.cnf /etc/mysql/conf.d/my.cnf

# FOR SOME REASON MATTER WHAT I DID, THE max_allowed_packet SETTING WAS NEVER BEING IMPLEMENTED FROM THE CONFIG
# SO NOW EXPRESSLY ADDING IT ON STARTUP
CMD ["mysqld", "--max_allowed_packet=128M"]

EXPOSE 3306
