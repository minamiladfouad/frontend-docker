# Use an official Nginx image as the base image
FROM nginx:latest

# Recieve args from docker compose file
    ARG DOMAIN_CER
    ARG DOMAIN_KEY
    ARG SRV_DOMAIN

    ENV DOMAIN_CER=$DOMAIN_CER
    ENV DOMAIN_KEY=$DOMAIN_KEY
    ENV SRV_DOMAIN=$SRV_DOMAIN

# debug info
    Run echo "Debug nginx_frontend  ---- DOMAIN_CER=${DOMAIN_CER}"
    Run echo "Debug nginx_frontend  ---- DOMAIN_KEY=${DOMAIN_KEY}"
    Run echo "Debug nginx_frontend  ---- SRV_DOMAIN=${SRV_DOMAIN}"

# Copy certificate
    # no need to copy - linked as volume
    # COPY ./${DOMAIN_CER} /etc/nginx/${DOMAIN_CER}
    # COPY ./${DOMAIN_KEY} /etc/nginx/${DOMAIN_KEY}

# Copy ngnix.conf to tmp file
    COPY ./nginx.conf /etc/nginx/nginx.conf.tmp
    # replace all env vars by its values
    RUN envsubst '$DOMAIN_CER $DOMAIN_KEY $SRV_DOMAIN' \
        < /etc/nginx/nginx.conf.tmp \
        > /etc/nginx/nginx.conf

# Expose port 80 443 to allow external access to the web server
EXPOSE 80 443
CMD ["nginx", "-g", "daemon off;"]
