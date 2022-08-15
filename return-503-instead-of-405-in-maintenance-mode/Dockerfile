FROM nginx:latest

COPY nginx.conf /etc/nginx
COPY default.conf /etc/nginx/conf.d
COPY maintenance_mode.conf /etc/nginx/conf.d

RUN mkdir -p /var/www/html/maintenance
COPY index.html /var/www/html/maintenance

# Set maintenance mode
#RUN mkdir -p /var/tmp/nginx
#RUN touch /var/tmp/nginx/maintenance
